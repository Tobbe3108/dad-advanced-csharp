**Challenge 1: Filtering an Array**  
You have an array of integers. Write a LINQ query to filter the array and select all even numbers.

<details>
<summary>Solution 1</summary>

```csharp
int[] numbers = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

var evenNumbers = numbers.Where(n => n % 2 == 0);

foreach (var number in evenNumbers)
{
    Console.WriteLine(number);
}
```

</details>

**Challenge 2: Finding the Maximum Value**  
Given an array of integers, find the maximum value using LINQ.

<details>
<summary>Solution 2</summary>

```csharp
int[] numbers = { 4, 7, 2, 9, 1, 5, 8, 3, 6 };

int max = numbers.Max();

Console.WriteLine("The maximum value is: " + max);
```

</details>

**Challenge 3: Filtering and Sorting**  
Given a list of strings, filter out strings that contain the letter 'a' and then sort the remaining strings alphabetically.

<details>
<summary>Solution 3</summary>

```csharp
var words = new List<string> { "apple", "banana", "cherry", "date", "fig" };

var filteredAndSorted = words.Where(word => !word.Contains("a")).OrderBy(word => word);

foreach (var word in filteredAndSorted)
{
    Console.WriteLine(word);
}
```

</details>

**Challenge 4: Grouping Data**  
Given a list of persons with their names and ages, group them by age and count the number of persons in each age group.

<details>
<summary>Solution 4</summary>

```csharp
var people = new List<Person>
{
    new Person("Alice", 25),
    new Person("Bob", 30),
    new Person("Charlie", 25),
    new Person("David", 35),
    new Person("Eve", 30),
};

var ageGroups = people.GroupBy(person => person.Age)
                     .Select(group => new { Age = group.Key, Count = group.Count() });

foreach (var group in ageGroups)
{
    Console.WriteLine($"Age: {group.Age}, Count: {group.Count}");
}
return;

public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}
```

</details>

**Challenge 5: Joining Data**  
Given two lists, one containing customers and another containing their orders, join the data to create a list of customer names and the total order amount for each customer.

<details>
<summary>Solution 5</summary>

```csharp
var customers = new List<Customer>
{
    new Customer { Id = 1, Name = "Alice" },
    new Customer { Id = 2, Name = "Bob" },
    new Customer { Id = 3, Name = "Charlie" },
};

List<Order> orders = new List<Order>
{
    new Order { CustomerId = 1, Amount = 100 },
    new Order { CustomerId = 2, Amount = 50 },
    new Order { CustomerId = 1, Amount = 200 },
    new Order { CustomerId = 3, Amount = 75 },
};

var customerOrders = from customer in customers
                     join order in orders on customer.Id equals order.CustomerId into customerGroup
                     select new
                     {
                         CustomerName = customer.Name,
                         TotalAmount = customerGroup.Sum(order => order.Amount)
                     };

foreach (var result in customerOrders)
{
    Console.WriteLine($"Customer: {result.CustomerName}, Total Amount: {result.TotalAmount}");
}
return;

public class Customer
{
    public int Id { get; set; }
    public string Name { get; set; }
}

public class Order
{
    public int CustomerId { get; set; }
    public decimal Amount { get; set; }
}
```

</details>
