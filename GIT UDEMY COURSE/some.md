Need to study on the default vlau

|Literal Type|Example|
|---|---|
|Decimal Integer|`85`|
|Octal Integer|`0213`|
|Hexadecimal Integer|`0x4b`|
|Unsigned Integer|`30u`|
|Long Integer|`30L`|
|Float|`3.14f`|
|Double|`3.14159`|
|Exponential|`2.5E3`|
|Boolean|`true`, `false`|



### 4. Reference

A [reference variable](https://www.tutorialspoint.com/cplusplus/cpp_references.htm) is used to create a copy of a variable with the same reference. Hence, changes made to the reference variable also reflect on the original variable.

#### Syntax

data_type & reference_name= variable_name;



## typedef Declarations

You can create a new name for an existing type using **typedef**. Following is the simple syntax to define a new type using typedef −

typedef type newname; 

For example, the following tells the compiler that feet is another name for int −

typedef int feet;

Now, the following declaration is perfectly legal and creates an integer variable called distance −