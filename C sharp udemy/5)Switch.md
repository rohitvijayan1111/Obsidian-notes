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
