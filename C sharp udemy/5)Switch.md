![[Pasted image 20251216212958.png]]

default is also possible


```
public static string DescribeDay(int dayNumber)
{
    switch (dayNumber)
    {
        case 1..5:
            return "Working day";

        case 6..7:
            return "Weekend";

        default:
            return "Invalid day number";
    }
}

```

the above possible in modern day c#

class Test
{
    static int x;

    static Test()
    {
        x = 10;
    }
}



![[Pasted image 20251216214015.png]]


![[Pasted image 20251216221511.png]]

![[Pasted image 20251216221542.png]]

https://docs.google.com/document/d/1EsRcNv33QH9Wi2B1uAmkvwHq_p4NKw0QtijpxM0VlqM/edit?tab=t.0#heading=h.4fcghembqy5w



# CHar

- "" indicates a string
- '' indicates a char
- so if we want to return `char` type , use single quotes'
- string is a collection of char
- so using += i can concatinate a char with string, as well as string with string 


![[Pasted image 20251217122453.png]]
![[Pasted image 20251217122530.png]]


![[Pasted image 20251217122853.png]]

.Length is used to find the length of the string



# For loop:

- has three sections, initialization section, condition section, iterator section
- ![[Pasted image 20251217123231.png]]
- iterator is executed only after the end of the loop
![[Pasted image 20251217123330.png]]



# break
- stops the execution of the loop
# continue
- skips the current iterations of the loop and moves to the next iteration
# .All method
![[Pasted image 20251217123837.png]]
The **`.All()`** method is a **LINQ** extension method used to check **whether every element in a collection satisfies a condition**.
# Loop performance optimization

- try to break, when ur operation has been done
- if possible, do the heavy calls outside the nested loops( database calls, not dependent on the loop )