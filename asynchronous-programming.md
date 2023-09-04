**Challenge 1: Basic Asynchronous Method**  
Create an asynchronous method that simulates a simple delay of 2 seconds. Use async and await to achieve this.

<details>
<summary>Solution 1</summary>

```csharp
await DelayAsync();
Console.WriteLine("Delay completed.");
return;

static async Task DelayAsync()
{
  await Task.Delay(2000);
}
```
</details>

**Challenge 2: Parallel Execution**  
Write a program that launches two asynchronous tasks. Each task should simulate a delay of 3 seconds. Ensure that both tasks run in parallel and complete independently.

<details>
<summary>Solution 2</summary>

```csharp
var task1 = DelayAsync(3000);
var task2 = DelayAsync(3000);

await Task.WhenAll(task1, task2);

Console.WriteLine("Both tasks completed.");
return;

static async Task DelayAsync(int milliseconds)
{
  await Task.Delay(milliseconds);
}
```
</details>

**Challenge 3: Asynchronous File I/O**  
Create an asynchronous method that reads a text file named "sample.txt" and prints its contents to the console. Ensure proper exception handling.

<details>
<summary>Solution 3</summary>

```csharp
try
{
  var content = await ReadFileAsync("sample.txt");
  Console.WriteLine(content);
}
catch (FileNotFoundException)
{
  Console.WriteLine("File not found.");
}
catch (Exception ex)
{
  Console.WriteLine($"An error occurred: {ex.Message}");
}

return;

static async Task<string> ReadFileAsync(string fileName)
{
  using var reader = new StreamReader(fileName);
  return await reader.ReadToEndAsync();
}
```
</details>

**Challenge 4: Asynchronous Web Request**  
Write a program that asynchronously fetches the contents of a website (e.g., "https://www.example.com") and displays the number of characters in the response.

<details>
<summary>Solution 4</summary>

```csharp
const string url = "https://www.example.com";
var content = await FetchWebsiteContentAsync(url);
var characterCount = content.Length;

Console.WriteLine($"Content length of {url}: {characterCount} characters.");
return;

static async Task<string> FetchWebsiteContentAsync(string url)
{
  using var httpClient = new HttpClient();
  return await httpClient.GetStringAsync(url);
}
```
</details>

**Challenge 5: Asynchronous Task Coordination**  
Write a program that downloads three images asynchronously from different URLs and saves them to disk. Ensure that all downloads run concurrently, but the program should only complete when all images are downloaded successfully.

<details>
<summary>Solution 5</summary>

```csharp
string[] urls =
{
  "https://example.com/image1.jpg", "https://example.com/image2.jpg", "https://example.com/image3.jpg"
};

await DownloadImagesAsync(urls);

Console.WriteLine("All images downloaded successfully.");
return;

static async Task DownloadImagesAsync(IEnumerable<string> urls)
{
  var httpClient = new HttpClient();

  var tasks = urls.Select(async url =>
  {
    var response = await httpClient.GetAsync(url);
    response.EnsureSuccessStatusCode();
    var content = await response.Content.ReadAsByteArrayAsync();
    var fileName = Path.GetFileName(url);
    await File.WriteAllBytesAsync(fileName, content);
  });

  await Task.WhenAll(tasks);
}
```
</details>
