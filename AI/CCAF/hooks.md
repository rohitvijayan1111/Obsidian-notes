![[Pasted image 20261115130209.png]]

![[Pasted image 20261115131303.png]]


You've got it right, and my snippet was misleading. **You never call a hook yourself.** You register it, and the framework calls it automatically at that point in the loop. My example showed the hook's _logic_ as a plain function and left out the registration, so it looked like something you'd have to invoke manually.

How it works depends on where you're running the agent.

## 1. Claude Code and the Agent SDK: the framework calls it

They own the agentic loop. You **register** a hook for an event plus a **matcher**, and they call it before or after every matching tool call. You don't write the loop, and you don't call the hook.

**Claude Code** registers hooks in `settings.json`:

```json
{
  "hooks": {
    "PreToolUse": [
      { "matcher": "Bash",
        "hooks": [{ "type": "command", "command": "./check_bash.sh" }] }
    ]
  }
}
```

Every time Claude tries to use Bash, Claude Code runs `check_bash.sh` first, automatically. Exit code 2 blocks the call.

**Agent SDK** registers a callback (field names here are illustrative):

```python
async def block_big_refunds(input_data, tool_use_id, context):
    if input_data["tool_input"]["amount"] > 500:
        return {"hookSpecificOutput": {
            "hookEventName": "PreToolUse",
            "permissionDecision": "deny",
            "permissionDecisionReason": "Over $500, escalate to human"}}
    return {}

options = ClaudeAgentOptions(
    hooks={"PreToolUse": [HookMatcher(matcher="issue_refund",
                                      hooks=[block_big_refunds])]}
)
```

You hand the function to the SDK. **The SDK calls it** whenever Claude requests `issue_refund`.

```
Claude: tool_use(issue_refund)
   → SDK sees PreToolUse is registered for "issue_refund"
   → SDK calls your function          ← automatic
   → deny? Tool skipped, reason sent to Claude
   → allow? Tool runs
```

## 2. The raw Messages API: no hooks exist

With the plain API, **you** write the loop, and the API has no hook system. "Hooks" are then just checks you place in your own code before or after running a tool:

```python
for block in resp.content:
    if block.type == "tool_use":
        verdict = pre_tool_check(block.name, block.input)   # your "PreToolUse"
        if verdict["decision"] == "deny":
            results.append({"type": "tool_result", "tool_use_id": block.id,
                            "content": verdict["reason"], "is_error": True})
            continue
        out = run_tool(block.name, block.input)
        out = post_tool_clean(block.name, out)               # your "PostToolUse"
        results.append({"type": "tool_result", "tool_use_id": block.id,
                        "content": out})
```

The idea is the same: deterministic code between Claude's request and the tool actually running. The only difference is that you wired it into the loop yourself.

## Summary

|Environment|Who owns the loop|How hooks run|
|---|---|---|
|Claude Code|Claude Code|Registered in `settings.json` and **called automatically**|
|Agent SDK|The SDK|Registered as callbacks and **called automatically**|
|Raw Messages API|You|No hook system. You put the checks in your own loop.|

**For the exam:** the key property of a hook is that **the model can't skip it**. That holds because it isn't the model's decision to call it. The harness, whether that's Claude Code, the SDK or your own loop, runs it every time.


### 1.3 The hook events you should know

These are the main events in Claude Code and the Agent SDK:

| Hook                 | When it fires                          | Typical use                                                                       |
| -------------------- | -------------------------------------- | --------------------------------------------------------------------------------- |
| **PreToolUse**       | Before a tool runs                     | Block policy violations, validate inputs, enforce prerequisites                   |
| **PostToolUse**      | After a tool runs                      | Normalize or clean results, redact sensitive data, log, run a formatter or linter |
| **UserPromptSubmit** | When the user sends a message          | Add context, filter or validate input                                             |
| **Stop**             | When the main agent is about to finish | Check the work really is done (for example, tests pass), or force it to continue  |
| **SubagentStop**     | When a subagent finishes               | Validate a subagent’s output                                                      |
| **SessionStart**     | When a session begins                  | Load context or setup                                                             |
| **PreCompact**       | Before context compaction              | Save important state before it gets summarized                                    |
| **Notification**     | When the agent sends a notification    | Alerts                                                                            |