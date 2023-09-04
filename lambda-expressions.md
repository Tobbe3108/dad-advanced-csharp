**Challenge 1: Basic Delegates**  
Write a C# program that defines a delegate and uses it to print "Hello, World!" to the console.

<details>
<summary>Solution 1</summary>

```csharp
using System;

class Program
{
    delegate void PrintMessage();

    static void Main(string[] args)
    {
        PrintMessage message = () => Console.WriteLine("Hello, World!");
        message();
    }
}
```
</details>

**Challenge 2: Func and Delegates**  
Create a delegate that takes two integers as parameters and returns their sum using Func<int, int, int>.

<details>
<summary>Solution 2</summary>

```csharp
using System;

class Program
{
    delegate int Calculate(int a, int b);

    static void Main(string[] args)
    {
        Calculate add = (x, y) => x + y;
        int result = add(5, 7);
        Console.WriteLine(result);
    }
}
```
</details>

**Challenge 3: Action and Delegates**  
Define an Action delegate that takes an integer as a parameter and prints its square to the console.

<details>
<summary>Solution 3</summary>

```csharp
using System;

class Program
{
    delegate void PerformAction(int number);

    static void Main(string[] args)
    {
        PerformAction squareAndPrint = (x) => Console.WriteLine(x * x);
        squareAndPrint(4);
    }
}
```
</details>

**Challenge 4: Multicast Delegates**  
Create a program that demonstrates the use of a multicast delegate to execute multiple methods sequentially.

<details>
<summary>Solution 4</summary>

```csharp
using System;

class Program
{
    delegate void MathOperation(int a, int b);

    static void Add(int a, int b)
    {
        Console.WriteLine($"Addition: {a + b}");
    }

    static void Subtract(int a, int b)
    {
        Console.WriteLine($"Subtraction: {a - b}");
    }

    static void Main(string[] args)
    {
        MathOperation operations = Add;
        operations += Subtract;

        operations(10, 5);
    }
}
```
</details>

**Challenge 5: Generic Delegates**  
Create a generic delegate that takes two arguments and returns a result of any type.

<details>
<summary>Solution 5</summary>

```csharp
using System;

class Program
{
    delegate TResult GenericOperation<T1, T2, TResult>(T1 a, T2 b);

    static void Main(string[] args)
    {
        GenericOperation<int, int, double> divide = (x, y) => (double)x / y;
        double result = divide(10, 2);
        Console.WriteLine(result);
    }
}
```
</details>

**Challenge 6: Func and Lambda Expressions**  
Use a Func delegate and a lambda expression to find the maximum of two numbers.

<details>
<summary>Solution 6</summary>

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Func<int, int, int> findMax = (x, y) => x > y ? x : y;
        int max = findMax(7, 12);
        Console.WriteLine(max);
    }
}
```
</details>

**Challenge 7: Action with Lists**  
Define an Action delegate that takes a List of integers and prints each element to the console.

<details>
<summary>Solution 7</summary>

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        Action<List<int>> printList = (list) =>
        {
            foreach (int item in list)
            {
                Console.WriteLine(item);
            }
        };

        List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
        printList(numbers);
    }
}
```
</details>

**Challenge 8: Delegates as Callbacks**  
Create a program that uses delegates as callbacks to implement a simple event handling system.

<details>
<summary>Solution 8</summary>

```csharp
using System;

class Program
{
    delegate void EventHandler(string message);

    static void Main(string[] args)
    {
        EventHandler eventHandler = (message) => Console.WriteLine("Event fired: " + message);

        // Simulate an event
        eventHandler("Button Clicked");
    }
}
```
</details>

**Challenge 9: Func Composition**  
Compose two Func delegates to calculate the square of the sum of two numbers.

<details>
<summary>Solution 9</summary>

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Func<int, int, int> add = (x, y) => x + y;
        Func<int, int> square = (x) => x * x;

        Func<int, int, int> squareOfSum = (a, b) => square(add(a, b));

        int result = squareOfSum(3, 4);
        Console.WriteLine(result);
    }
}
```
</details>

**Challenge 10: Action with Events**  
Create a program that demonstrates using Action with events.

<details>
<summary>Solution 10</summary>

```csharp
using System;

class Program
{
    static event Action<string> LogEvent;

    static void Main(string[] args)
    {
        LogEvent += (message) => Console.WriteLine("Log: " + message);

        // Simulate an event
        LogEvent?.Invoke("An error occurred.");
    }
}
```
</details>

**Challenge 11: Func and Memoization**  
Implement a memoization technique using Func to store and retrieve the Fibonacci sequence.

<details>
<summary>Solution 11</summary>

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static Dictionary<int, long> fibCache = new Dictionary<int, long>();

    static long Fibonacci(int n)
    {
        if (fibCache.ContainsKey(n))
            return fibCache[n];

        if (n <= 2)
            return 1;

        long result = Fibonacci(n - 1) + Fibonacci(n - 2);
        fibCache[n] = result;
        return result;
    }

    static void Main(string[] args)
    {
        int n = 10;
        long result = Fibonacci(n);
        Console.WriteLine($"Fibonacci({n}) = {result}");
    }
}
```
</details>

**Challenge 12: Action with Exception Handling**  
Create a program that uses Action to handle exceptions and log error messages.

<details>
<summary>Solution 12</summary>

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Action<string, Action> tryCatchLog = (message, action) =>
        {
            try
            {
                action();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {message}. Exception: {ex.Message}");
            }
        };

        tryCatchLog("Divide by zero", () =>
        {
            int x = 10, y = 0;
            int result = x / y;
            Console.WriteLine(result);


        });
    }
}
```
</details>

**Challenge 13: Delegates with LINQ**  
Use delegates to filter a list of numbers and return only the even ones using LINQ.

<details>
<summary>Solution 13</summary>

```csharp
using System;
using System.Linq;
using System.Collections.Generic;

class Program
{
    delegate bool FilterPredicate(int num);

    static void Main(string[] args)
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

        FilterPredicate isEven = (num) => num % 2 == 0;

        var evenNumbers = numbers.Where(num => isEven(num)).ToList();

        Console.WriteLine("Even numbers:");
        foreach (var num in evenNumbers)
        {
            Console.WriteLine(num);
        }
    }
}
```
</details>

**Challenge 14: Delegate Chains**  
Create a program that chains multiple delegates to perform a sequence of actions.

<details>
<summary>Solution 14</summary>

```csharp
using System;

class Program
{
    delegate void StringAction(ref string value);

    static void AddHello(ref string value)
    {
        value += " Hello";
    }

    static void AddWorld(ref string value)
    {
        value += " World";
    }

    static void Main(string[] args)
    {
        string message = "C#";
        StringAction addActionChain = AddHello;
        addActionChain += AddWorld;

        addActionChain(ref message);
        Console.WriteLine(message);
    }
}
```
</details>

**Challenge 15: Advanced Delegates**  
Create a program that uses delegates and events to implement a simple pub-sub system.

<details>
<summary>Solution 15</summary>

```csharp
using System;

class Program
{
    delegate void MessageHandler(string message);

    static event MessageHandler MessageReceived;

    static void Main(string[] args)
    {
        // Subscriber 1
        MessageReceived += (message) => Console.WriteLine("Subscriber 1: " + message);

        // Subscriber 2
        MessageReceived += (message) => Console.WriteLine("Subscriber 2: " + message);

        // Publish a message
        MessageReceived?.Invoke("Hello, Pub-Sub!");

        // Unsubscribe Subscriber 2
        MessageReceived -= (message) => Console.WriteLine("Subscriber 2: " + message);

        // Publish another message
        MessageReceived?.Invoke("Goodbye, Pub-Sub!");
    }
}
```
</details>
