**Challenge 1: Simple Parallelism**  
Write a C# program that calculates the sum of all even numbers from 1 to N in parallel using the Task Parallel Library. Ensure that the program correctly handles synchronization and prints the final result.

<details>
<summary>Solution 1</summary>

```csharp
using System;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        int N = 1000; // Replace with your desired value.
        int[] numbers = Enumerable.Range(1, N).ToArray();
        int sum = 0;

        Parallel.ForEach(numbers, number =>
        {
            if (number % 2 == 0)
            {
                Interlocked.Add(ref sum, number);
            }
        });

        Console.WriteLine($"Sum of even numbers from 1 to {N}: {sum}");
    }
}
```
</details>

**Challenge 2: Parallelized Data Processing**  
Create a program that reads a large text file line by line and processes each line in parallel using TPL tasks. The processing task should count the number of words in each line. Ensure proper synchronization and print the total word count.

<details>
<summary>Solution 2</summary>

```csharp
using System;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        string filePath = "large_text_file.txt"; // Replace with your file path.
        int totalWordCount = 0;

        Parallel.ForEach(File.ReadLines(filePath), line =>
        {
            int lineWordCount = line.Split(' ').Length;
            Interlocked.Add(ref totalWordCount, lineWordCount);
        });

        Console.WriteLine($"Total word count: {totalWordCount}");
    }
}
```
</details>

**Challenge 3: Parallel Aggregation**  
Implement a program that calculates the average of an array of double values using parallel aggregation with TPL. Ensure proper synchronization and print the result.

<details>
<summary>Solution 3</summary>

```csharp
using System;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        double[] values = { 1.0, 2.0, 3.0, 4.0, 5.0 }; // Replace with your array of values.
        double sum = 0.0;

        Parallel.ForEach(values, () => 0.0, (value, state, localSum) =>
        {
            return localSum + value;
        },
        localSum =>
        {
            Interlocked.Add(ref sum, localSum);
        });

        double average = sum / values.Length;
        Console.WriteLine($"Average: {average}");
    }
}
```
</details>

**Challenge 4: Parallelizing Complex Tasks**  
Develop a program that simulates downloading multiple web pages in parallel using TPL tasks. Each task should download a web page and count the number of words on that page. Finally, aggregate the word counts and print the total word count.

<details>
<summary>Solution 4</summary>

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        string[] urls = { "https://example.com", "https://sample.com", "https://test.com" }; // Replace with your URLs.
        int totalWordCount = 0;

        async Task<int> DownloadAndCountWordsAsync(string url)
        {
            using (HttpClient client = new HttpClient())
            {
                string pageContent = await client.GetStringAsync(url);
                return pageContent.Split(' ').Length;
            }
        }

        var tasks = urls.Select(url => DownloadAndCountWordsAsync(url)).ToArray();
        await Task.WhenAll(tasks);

        foreach (var task in tasks)
        {
            Interlocked.Add(ref totalWordCount, task.Result);
        }

        Console.WriteLine($"Total word count: {totalWordCount}");
    }
}
```
</details>

**Challenge 5: Parallel Data Processing with Dependencies**  
Build a program that performs parallel processing of data with dependencies. You have a list of tasks, each with a duration, and some tasks depend on the completion of others. Implement a system that processes tasks in parallel while respecting their dependencies and prints the total time taken.

<details>
<summary>Solution 5</summary>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        Dictionary<string, int> tasksWithDurations = new Dictionary<string, int>
        {
            {"TaskA", 2 },
            {"TaskB", 3 },
            {"TaskC", 1 },
            {"TaskD", 4 }
        };

        Dictionary<string, List<string>> taskDependencies = new Dictionary<string, List<string>>
        {
            {"TaskA", new List<string> { "TaskB" } },
            {"TaskC", new List<string> { "TaskA", "TaskD" } },
            {"TaskD", new List<string>() }
        };

        int totalDuration = await ProcessTasksAsync(tasksWithDurations, taskDependencies);
        Console.WriteLine($"Total time taken: {totalDuration} seconds");
    }

    static async Task<int> ProcessTasksAsync(Dictionary<string, int> tasksWithDurations, Dictionary<string, List<string>> taskDependencies)
    {
        async Task<int> ProcessTaskAsync(string taskName)
        {
            int duration = tasksWithDurations[taskName];
            await Task.Delay(TimeSpan.FromSeconds(duration));
            return duration;
        }

        async Task<int> ProcessWithDependenciesAsync(string taskName)
        {
            List<string> dependencies = taskDependencies.ContainsKey(taskName) ? taskDependencies[taskName] : new List<string>();
            var dependencyTasks = dependencies.Select(dependency => ProcessTaskAsync(dependency));
            await Task.WhenAll(dependencyTasks);
            int taskDuration = await ProcessTaskAsync(taskName);
            return taskDuration;
        }

        var tasks = tasksWithDurations.Keys.Select(taskName => ProcessWithDependenciesAsync(taskName));
        int[] durations = await Task.WhenAll(tasks);
        return durations.Sum();
    }
}
```
</details>
