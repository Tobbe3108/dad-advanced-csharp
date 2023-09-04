**Challenge 1: Accessing Type Information**  
Write a C# program that uses reflection to retrieve and display the full name of a given data type (e.g., System.Int32). Ensure that the program handles exceptions gracefully.

<details>
<summary>Solution 1</summary>

```csharp
using System;

class Program
{
    static void Main()
    {
        string typeName = "System.Int32"; // Change to any type you want to inspect
        try
        {
            Type type = Type.GetType(typeName);
            if (type != null)
            {
                Console.WriteLine("Full Name: " + type.FullName);
            }
            else
            {
                Console.WriteLine("Type not found.");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("An error occurred: " + ex.Message);
        }
    }
}
```
</details>

**Challenge 2: List Methods and Properties**  
Write a program that lists all the methods and properties of a given type using reflection. Allow the user to specify the type interactively.

<details>
<summary>Solution 2</summary>

```csharp
using System;
using System.Reflection;

class Program
{
    static void Main()
    {
        Console.Write("Enter a type name (e.g., System.String): ");
        string typeName = Console.ReadLine();

        try
        {
            Type type = Type.GetType(typeName);
            if (type != null)
            {
                Console.WriteLine("Methods:");
                foreach (MethodInfo methodInfo in type.GetMethods())
                {
                    Console.WriteLine(methodInfo.Name);
                }

                Console.WriteLine("\nProperties:");
                foreach (PropertyInfo propertyInfo in type.GetProperties())
                {
                    Console.WriteLine(propertyInfo.Name);
                }
            }
            else
            {
                Console.WriteLine("Type not found.");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("An error occurred: " + ex.Message);
        }
    }
}
```
</details>

**Challenge 3: Create an Object Using Reflection**  
Write a program that dynamically creates an instance of a specified type using reflection and invokes one of its methods.

<details>
<summary>Solution 3</summary>

```csharp
using System;
using System.Reflection;

class Program
{
    static void Main()
    {
        Console.Write("Enter a type name (e.g., System.String): ");
        string typeName = Console.ReadLine();

        try
        {
            Type type = Type.GetType(typeName);
            if (type != null)
            {
                object instance = Activator.CreateInstance(type);
                MethodInfo methodInfo = type.GetMethod("ToString"); // Change to any method you want to call
                if (methodInfo != null)
                {
                    string result = (string)methodInfo.Invoke(instance, null);
                    Console.WriteLine("Result of invoking ToString(): " + result);
                }
                else
                {
                    Console.WriteLine("Method not found.");
                }
            }
            else
            {
                Console.WriteLine("Type not found.");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("An error occurred: " + ex.Message);
        }
    }
}
```
</details>

**Challenge 4: Modify Object Properties Using Reflection**  
Write a program that uses reflection to modify the properties of an object. Allow the user to specify the object's type and property name interactively.

<details>
<summary>Solution 4</summary>

```csharp
using System;
using System.Reflection;

class Program
{
    static void Main()
    {
        Console.Write("Enter a type name (e.g., System.String): ");
        string typeName = Console.ReadLine();

        try
        {
            Type type = Type.GetType(typeName);
            if (type != null)
            {
                object instance = Activator.CreateInstance(type);

                Console.Write("Enter a property name: ");
                string propertyName = Console.ReadLine();

                PropertyInfo propertyInfo = type.GetProperty(propertyName);
                if (propertyInfo != null)
                {
                    Console.Write("Enter a new value: ");
                    string newValue = Console.ReadLine();

                    propertyInfo.SetValue(instance, Convert.ChangeType(newValue, propertyInfo.PropertyType), null);
                    Console.WriteLine("Property value updated successfully.");
                }
                else
                {
                    Console.WriteLine("Property not found.");
                }
            }
            else
            {
                Console.WriteLine("Type not found.");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("An error occurred: " + ex.Message);
        }
    }
}
```
</details>

**Challenge 5: Advanced Reflection - Analyze Assembly**  
Write a program that analyzes an assembly and displays information about its types, methods, and properties. Allow the user to load an assembly file interactively.

<details>
<summary>Solution 5</summary>

```csharp
using System;
using System.Reflection;

class Program
{
    static void Main()
    {
        Console.Write("Enter the path to an assembly file (e.g., MyAssembly.dll): ");
        string assemblyPath = Console.ReadLine();

        try
        {
            Assembly assembly = Assembly.LoadFrom(assemblyPath);
            Console.WriteLine("Assembly Information:");
            Console.WriteLine("Name: " + assembly.GetName().Name);
            Console.WriteLine("Version: " + assembly.GetName().Version);

            Type[] types = assembly.GetTypes();
            Console.WriteLine("\nTypes in the Assembly:");
            foreach (Type type in types)
            {
                Console.WriteLine("Type: " + type.FullName);
                Console.WriteLine("Methods:");
                foreach (MethodInfo methodInfo in type.GetMethods())
                {
                    Console.WriteLine("  " + methodInfo.Name);
                }
                Console.WriteLine("Properties:");
                foreach (PropertyInfo propertyInfo in type.GetProperties())
                {
                    Console.WriteLine("  " + propertyInfo.Name);
                }
                Console.WriteLine();
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("An error occurred: " + ex.Message);
        }
    }
}
```
</details>
