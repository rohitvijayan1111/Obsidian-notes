
Console.WriteLine
Console.ReadKey()



in c#,once the variable has been declared, its type can't be changed only the value can(should be of the declared type)

- a variable can't be redeclared in the scope

string -> double quotes

Declaration 
initialization 
init at declaration



NOTE:
- u cant use a variable before init ? what error comes **(Use of unassigned local variable 'x')**->**compile-time error** in **C#**
- use can use keywords as variable name using "@" sign
- Compile-time error: _Cannot implicitly convert type_->assigning a value of the wrong type to a variable 
- Strongly typed-> means datatype of a variable cannot be changed
- When you run a console app **by double-clicking the `.exe` file** (or in some older setups), the console window may close instantly when the program finishes.
-   C# is a statically-typed programming language, which means..

`Console.ReadKey()` keeps the window open so you can **see the output**.

# operator precedence
a=10
b=5

![[Pasted image 20251215103235.png]]

OUTPUT:
Addition105
Error (since subtraction10(becomes a string)- b) -.wont be allowed
Multiplication 50
Division 2
John Smith

we can add paranthesis to this , to avoid such issue



for readline:
```C#
Console.ReadLine()// nothing should be put in
```

![[Pasted image 20251215105736.png]]



Breakpoint:
click on the side of the code line or press F9

to move forward from breakpoint, oneline F10 or ![[Pasted image 20251215110001.png]]

- we can hover over the variables to see the value of it.

Quickwatch:

- Select the string, right "Quickwatch", u can put in expression and test its workings
![[Pasted image 20251215111110.png]]

# Comparison and Logical operators

**SHORT-CIRCUTING**
- If the first part of the operand in || , C# would not execute the second operand
- same for &&, if first false, then second operand isnt checked


Methods

![[Pasted image 20251215160242.png]]



![[Pasted image 20251215162132.png]]

- methods can be used before they can be declared 