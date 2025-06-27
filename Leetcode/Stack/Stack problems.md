### General Insights
1. It is not must that we need to include all the elements of the string in it (IT MAY BE ENOUGH TO STORE THE PARANTHESIS IN THE STACK) AND LATER PROCESS THE STRING


# [1106. Parsing A Boolean Expression](https://leetcode.com/problems/parsing-a-boolean-expression/)

```
class Solution:
    def parseBoolExpr(self, expression: str) -> bool:
        def parse(index):
            if expression[index] == 't':
                return True, index + 1
            if expression[index] == 'f':
                return False, index + 1
            
            op = expression[index]  # '!', '&', '|'
            index += 2  # skip operator and the opening '('
            results = []
            
            while expression[index] != ')':
                if expression[index] == ',':
                    index += 1  # skip commas
                else:
                    val, index = parse(index)
                    results.append(val)
            
            index += 1  # skip the closing ')'
            
            if op == '!':
                return (not results[0]), index
            elif op == '&':
                return all(results), index
            elif op == '|':
                return any(results), index
        
        result, _ = parse(0)
        return result
```


OR 

```
class Solution:
    def parseBoolExpr(self, expression: str) -> bool:
	        stack = []
        for ch in expression:
            if ch == ',':
                continue
            elif ch in 'tf':
                stack.append(ch == 't')
            elif ch in '&|!':
                stack.append(ch)
            elif ch == ')':
                operands = []
                # Pop until we find an operator
                while stack[-1] != '(':
                    operands.append(stack.pop())
                stack.pop()  # pop '('
                operator = stack.pop()
                
                if operator == '&':
                    stack.append(all(operands))
                elif operator == '|':
                    stack.append(any(operands))
                elif operator == '!':
                    stack.append(not operands[0])
            else:
                # For '(' just push to stack
                stack.append(ch)
        return stack[0]
```