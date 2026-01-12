Below is a **clean, practical, and interview-ready guide to C# naming conventions** for **variables, fields, methods (functions), and classes**, following **Microsoft/.NET guidelines**.

---

# C# Naming Conventions (Official & Best Practices)

---

## 1. Class Names

### Convention: **PascalCase**

- First letter of each word is capitalized
    
- Use **nouns**
    
- Avoid abbreviations (unless well-known)
    

```csharp
class Employee
class BankAccount
class OrderProcessor
```

❌ Bad:

```csharp
class employee
class bank_account
class emp
```

---

## 2. Method (Function) Names

### Convention: **PascalCase**

- Use **verbs** or **verb + noun**
    
- Clearly describe the action
    

```csharp
void CalculateSalary()
int GetEmployeeId()
bool IsValidUser()
```

❌ Bad:

```csharp
void calculatesalary()
void get_id()
```

---

## 3. Variable Names (Local Variables)

### Convention: **camelCase**

- First word lowercase
    
- Meaningful names
    
- Avoid single-letter names (except loops)
    

```csharp
int totalAmount;
string employeeName;
bool isActive;
```

✔ Loop variables:

```csharp
for (int i = 0; i < 10; i++) { }
```

❌ Bad:

```csharp
int x;
string str;
```

---

## 4. Field Names (Class-Level Variables)

### Private Fields

### Convention: **_camelCase** (underscore prefix)

```csharp
private int _salary;
private string _employeeName;
```

✔ This clearly distinguishes fields from local variables.

---

### Public Fields (Avoid If Possible)

If unavoidable:

### Convention: **PascalCase**

```csharp
public int Salary;
```

⚠️ Best practice: **Use properties instead of public fields**

---

## 5. Property Names

### Convention: **PascalCase**

```csharp
public int Salary { get; set; }
public string EmployeeName { get; private set; }
```

❌ Bad:

```csharp
public int salary;
```

---

## 6. Parameter Names

### Convention: **camelCase**

```csharp
void UpdateSalary(int newSalary)
```

❌ Bad:

```csharp
void UpdateSalary(int NewSalary)
```

---

## 7. Interface Names

### Convention: **PascalCase with ‘I’ prefix**

```csharp
interface IRepository
interface ILogger
```

❌ Bad:

```csharp
interface Repository
```

---

## 8. Enum Names & Members

### Enum Name → PascalCase

### Enum Members → PascalCase

```csharp
enum OrderStatus
{
    Pending,
    Approved,
    Rejected
}
```

---

## 9. Constant Names

### Convention: **PascalCase**

```csharp
public const int MaxRetryCount = 3;
```

❌ Avoid ALL_CAPS (C-style)

```csharp
// ❌ Not recommended in C#
const int MAX_RETRY_COUNT = 3;
```

---

## 10. Boolean Naming (Very Important ⭐)

Use **is / has / can / should**

```csharp
bool isActive;
bool hasAccess;
bool canEdit;
bool shouldRetry;
```

❌ Bad:

```csharp
bool active;
bool flag;
```

---

## 11. Event Names

### Convention: **PascalCase (verb)**

```csharp
event EventHandler DataLoaded;
event EventHandler UserLoggedIn;
```

---

## 12. Async Method Names

### Convention: **PascalCase + Async suffix**

```csharp
Task LoadDataAsync()
Task<int> GetCountAsync()
```

❌ Bad:

```csharp
Task LoadData()
```

---

## 13. Generic Type Parameters

### Convention: **T** or **T + descriptive name**

```csharp
class Repository<T>
class Dictionary<TKey, TValue>
```

---

## 14. File Names

### Convention: **Match class name**

```text
Employee.cs
OrderService.cs
```

---

## 15. Namespaces

### Convention: **PascalCase with dots**

```csharp
namespace Company.Project.Module
```

---

## 16. Complete Example (Best Practice)

```csharp
namespace Company.Payroll
{
    public interface IEmployeeService
    {
        decimal CalculateSalary(int employeeId);
    }

    public class EmployeeService : IEmployeeService
    {
        private decimal _baseSalary;

        public decimal BaseSalary
        {
            get => _baseSalary;
            set => _baseSalary = value;
        }

        public decimal CalculateSalary(int employeeId)
        {
            bool isEligible = employeeId > 0;
            return isEligible ? _baseSalary : 0;
        }
    }
}
```

---

## 17. Quick Cheat Sheet (Interview Gold ⭐)

|Element|Convention|
|---|---|
|Class|PascalCase|
|Method|PascalCase|
|Variable|camelCase|
|Field (private)|_camelCase|
|Property|PascalCase|
|Interface|IPascalCase|
|Enum|PascalCase|
|Constant|PascalCase|
|Async Method|PascalCaseAsync|

---

## One-Line Rule to Remember ⭐

> **Public members use PascalCase, private data uses camelCase with underscore, and methods describe actions.**

---

If you want, I can also give:

- Clean Code naming tips
    
- Real-world naming mistakes
    
- Interview trick questions
    
- Java vs C# naming comparison
    

Just tell me 😊