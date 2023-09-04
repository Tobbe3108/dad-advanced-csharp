**Challenge 1: Basic Pattern Matching**  
Write a C# program that takes an input string and checks if it's a valid email address. Use pattern matching to verify if the string follows the basic email format.

<details>
<summary>Solution 1</summary>

```csharp
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        Console.Write("Enter an email address: ");
        string input = Console.ReadLine();

        if (IsValidEmail(input))
        {
            Console.WriteLine("Valid email address.");
        }
        else
        {
            Console.WriteLine("Invalid email address.");
        }
    }

    static bool IsValidEmail(string input)
    {
        // Use pattern matching to check if the input matches the basic email format.
        if (Regex.IsMatch(input, @"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"))
        {
            return true;
        }
        return false;
    }
}
```
</details>

**Challenge 2: Matching Numeric Patterns**  
Write a C# program that checks if a given string can be converted to an integer or a double. Use pattern matching to identify whether the input is numeric and, if so, whether it's an integer or a double.

<details>
<summary>Solution 2</summary>

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Enter a value: ");
        string input = Console.ReadLine();

        if (IsNumeric(input))
        {
            if (IsInteger(input))
            {
                Console.WriteLine("Integer");
            }
            else
            {
                Console.WriteLine("Double");
            }
        }
        else
        {
            Console.WriteLine("Not a numeric value.");
        }
    }

    static bool IsNumeric(string input)
    {
        return double.TryParse(input, out _);
    }

    static bool IsInteger(string input)
    {
        return int.TryParse(input, out _);
    }
}
```
</details>

**Challenge 3: Pattern Matching in Lists**  
Write a C# program that takes a list of integers and checks if it contains any prime numbers. Use pattern matching to identify prime numbers in the list.

<details>
<summary>Solution 3</summary>

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 2, 4, 7, 8, 11, 13, 15, 20 };

        foreach (var number in numbers)
        {
            if (IsPrime(number))
            {
                Console.WriteLine($"{number} is a prime number.");
            }
        }
    }

    static bool IsPrime(int number)
    {
        if (number <= 1)
        {
            return false;
        }
        if (number <= 3)
        {
            return true;
        }
        if (number % 2 == 0 || number % 3 == 0)
        {
            return false;
        }
        for (int i = 5; i * i <= number; i += 6)
        {
            if (number % i == 0 || number % (i + 2) == 0)
            {
                return false;
            }
        }
        return true;
    }
}
```
</details>

**Challenge 4: Advanced Pattern Matching with Classes**  
Create a class hierarchy representing different shapes (e.g., Circle, Rectangle, Triangle). Implement pattern matching to calculate and display the area of a shape object passed as input.

<details>
<summary>Solution 4</summary>

```csharp
using System;

class Program
{
    static void Main()
    {
        Shape shape1 = new Circle(5);
        Shape shape2 = new Rectangle(4, 6);
        Shape shape3 = new Triangle(3, 4, 5);

        CalculateAndDisplayArea(shape1);
        CalculateAndDisplayArea(shape2);
        CalculateAndDisplayArea(shape3);
    }

    static void CalculateAndDisplayArea(Shape shape)
    {
        double area = shape switch
        {
            Circle c => Math.PI * c.Radius * c.Radius,
            Rectangle r => r.Length * r.Width,
            Triangle t => 0.5 * t.Base * t.Height,
            _ => 0.0
        };

        Console.WriteLine($"Area of {shape.GetType().Name}: {area}");
    }
}

class Shape { }

class Circle : Shape
{
    public double Radius { get; }

    public Circle(double radius)
    {
        Radius = radius;
    }
}

class Rectangle : Shape
{
    public double Length { get; }
    public double Width { get; }

    public Rectangle(double length, double width)
    {
        Length = length;
        Width = width;
    }
}

class Triangle : Shape
{
    public double Base { get; }
    public double Height { get; }

    public Triangle(double @base, double height)
    {
        Base = @base;
        Height = height;
    }
}
```
</details>

**Challenge 5: Pattern Matching with Nested Objects**  
Create a complex data structure representing a directory structure with folders and files. Use pattern matching to implement a search function that finds all files with a given extension within the directory structure.

<details>
<summary>Solution 5</summary>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        // Create a sample directory structure.
        DirectoryItem root = new DirectoryItem("Root");
        DirectoryItem folder1 = new DirectoryItem("Folder1");
        DirectoryItem folder2 = new DirectoryItem("Folder2");
        FileItem file1 = new FileItem("file1.txt");
        FileItem file2 = new FileItem("file2.jpg");
        FileItem file3 = new FileItem("file3.txt");

        root.Items.Add(folder1);
        root.Items.Add(folder2);
        folder1.Items.Add(file1);
        folder1.Items.Add(file2);
        folder2.Items.Add(file3);

        // Search for files with the ".txt" extension.
        List<FileItem> txtFiles = SearchFilesWithExtension(root, ".txt");

        Console.WriteLine("Text files found:");
        foreach (var txtFile in txtFiles)
        {
            Console.WriteLine(txtFile.Name);
        }
    }

    static List<FileItem> SearchFilesWithExtension(DirectoryItem directory, string extension)
    {
        List<FileItem> foundFiles = new List<FileItem>();

        foreach (var item in directory.Items)
        {
            switch (item)
            {
                case FileItem file when file.Name.EndsWith(extension):
                    foundFiles.Add(file);
                    break;
                case DirectoryItem folder:
                    foundFiles.AddRange(SearchFilesWithExtension(folder, extension));
                    break;
            }
        }

        return foundFiles;
    }
}

class DirectoryItem
{
    public string Name { get; }
    public List<DirectoryItem> Items { get; } = new List<DirectoryItem>();

    public DirectoryItem(string

 name)
    {
        Name = name;
    }
}

class FileItem
{
    public string Name { get; }

    public FileItem(string name)
    {
        Name = name;
    }
}
```
</details>
