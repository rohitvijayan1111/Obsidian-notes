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




# [1249. Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)

## The approach i used
what i did was i used a variable open to indicate if there is any opening paranthesis that is encountered before and is not closed yet.

and an stack to store the processed elements

when ) is encountered we check if open!=0 , if so we continue(not add the closing) else we go back until (  is encountered and and add these back  into one single element

so add the end of the iteration of the string , if open>0 that means those parenthesis should be added, so we exclude them add them to the stack

```
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        stack=[]
        open=0
        n=len(s)
        #When to exclude
            # -> when there is only ) and no ( in the paren 
            # -> When there is only ( and we havent found )              
        for i in range(n):
            if(s[i]=='('):
                open+=1
                stack.append("(")
            elif(s[i]==')'):
                if(open==0):
                    continue
                else:
                    st=""
                    while(stack and stack[-1]!='('):
                        st=stack.pop()+st
                    st=stack.pop()+st+")"
                    open-=1
                    stack.append(st)
            else:
                stack.append(s[i])
        
        while(open!=0):
            st=""
            while(stack and stack[-1]!='('):
                st=stack.pop()+st
            stack.pop()                  
            open-=1
            stack.append(st)

        res=""
        while(stack):
            res=stack.pop()+res

        return res
```
## TC and SC
 TC-> at worst case could be o(n^2)
 space->o(n)

## Optimized one

we do a simple balancing parenthesis check to find which and all parenthesis are invalid , and add to a set, and exlude those index when printing

```
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        n = len(s)
        to_remove = set()  # indices of parentheses to remove
        stack = []

        # First pass: left to right, handle unmatched ')'
        for i in range(n):
            if s[i] == '(':
                stack.append(i)
            elif s[i] == ')':
                if stack:
                    stack.pop()  # matched with an earlier '('
                else:
                    to_remove.add(i)  # unmatched ')'

        # Second pass: remaining unmatched '(' in the stack
        to_remove.update(stack)

        # Build the result skipping the indices in to_remove
        res = []
        for i in range(n):
            if i not in to_remove:
                res.append(s[i])

        return ''.join(res)

```



