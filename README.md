# dotnet-updates
### Primary Constructors
In .NET 8 and C# 12, primary constructors offer a clean way to define classes and their dependencies, including dependency injection (DI). With the introduction of primary constructors, you can inject services into your classes directly through the constructor parameters.
###### Dependency Injection with Primary Constructors
```
public interface IMyService
{
    void DoWork();
}

public class MyService : IMyService
{
    public void DoWork()
    {
        Console.WriteLine("Doing work...");
    }
}

public class MyController(IMyService myService) : ControllerBase
{
    private readonly IMyService _myService = myService;

    [HttpGet]
    public IActionResult Get()
    {
        _myService.DoWork();
        return Ok("Service performed work.");
    }
}

```

###### Dependency Injection in console application

```
public class PersonService(IMyService myService)
{
    private readonly IMyService _myService = myService;

    public void Serve()
    {
        _myService.DoWork();
        Console.WriteLine("Person service is serving...");
    }
}

```

### DateOnly in .NET 6
In .NET 6, the DateOnly type was introduced as a new type to represent a date without a time component. This type is useful when you want to work with just the date part (year, month, day) and avoid dealing with the time (hours, minutes, seconds).

```
DateOnly date = new DateOnly(2023, 3, 21); // Year, Month, Day
Console.WriteLine(date); // Output: 2023-03-21
```

```
DateTime dateTime = DateTime.Now; // Current DateTime (includes time)
DateOnly dateFromDateTime = DateOnly.FromDateTime(dateTime);
Console.WriteLine(dateFromDateTime); // Output: Only the date part (e.g., 2025-03-21)
```

### Numerical StringComparer coming in .NET 10
In .NET 10, a new feature is being introduced that includes a Numerical StringComparer. This feature aims to provide a way to compare strings that represent numbers in a more intuitive, numeric way rather than lexicographically. In most programming languages, strings are compared lexicographically, meaning each character in a string is compared based on its Unicode value. For example, comparing numeric strings like "10" and "2" lexicographically would result in "10" being considered less than "2" because the character '1' in "10" is smaller than '2' in "2". However, this is not how we would normally expect numbers to be compared.

```
List<string> numberStrings = new List<string> { "10", "2", "100", "11" };
numberStrings.Sort(NumericalStringComparer.Ordinal);
foreach (var item in numberStrings)
{
    Console.WriteLine(item);  // Output: 2, 10, 11, 100
}
```
