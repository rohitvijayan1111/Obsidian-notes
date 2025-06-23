```

def generate_palindromes(length):
    palindromes = []
    for half in range(10**(length - 1), 10**length):
        s = str(half)
        
        # Even-length palindrome
        even_pal = int(s + s[::-1])
        palindromes.append(even_pal)

        # Odd-length palindrome
        odd_pal = int(s + s[-2::-1])
        palindromes.append(odd_pal)
    
    return palindromes

```