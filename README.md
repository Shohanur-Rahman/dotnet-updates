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
