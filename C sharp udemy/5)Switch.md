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


![[Pasted image 20251216214015.png]]


![[Pasted image 20251216221511.png]]

![[Pasted image 20251216221542.png]]

https://docs.google.com/document/d/1EsRcNv33QH9Wi2B1uAmkvwHq_p4NKw0QtijpxM0VlqM/edit?tab=t.0#heading=h.4fcghembqy5w



# CHar

- "" indicates a string
- '' indicates a char
- so if we want to return `char` type , use single quotes'
- string is a collection of char
- 