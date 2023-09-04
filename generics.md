**Challenge 1: Generic Identity Function**  
Create a generic function called `Identity` that takes an input value of any type and returns that value unchanged.

<details>
<summary>Solution 1</summary>

```csharp
public static T Identity<T>(T input)
{
    return input;
}
```
</details>

**Challenge 2: Generic Swap Function**  
Write a generic function called `Swap` that takes two parameters of the same type and swaps their values.

<details>
<summary>Solution 2</summary>

```csharp
public static void Swap<T>(ref T a, ref T b)
{
    T temp = a;
    a = b;
    b = temp;
}
```
</details>

**Challenge 3: Generic List Filter**  
Create a generic function called `Filter` that accepts a list of elements of any type and a predicate function. It should return a new list containing only the elements for which the predicate returns `true`.

<details>
<summary>Solution 3</summary>

```csharp
public static List<T> Filter<T>(List<T> list, Func<T, bool> predicate)
{
    List<T> filteredList = new List<T>();
    foreach (T item in list)
    {
        if (predicate(item))
        {
            filteredList.Add(item);
        }
    }
    return filteredList;
}
```
</details>

**Challenge 4: Generic Stack with Max Value**  
Implement a generic `MaxStack` class that can store elements of any type and has a `Max` method that returns the maximum value in the stack. The `Max` method should have O(1) time complexity.

<details>
<summary>Solution 4</summary>

```csharp
public class MaxStack<T> where T : IComparable<T>
{
    private Stack<T> stack = new Stack<T>();
    private Stack<T> maxStack = new Stack<T>();

    public void Push(T item)
    {
        stack.Push(item);

        if (maxStack.Count == 0 || item.CompareTo(maxStack.Peek()) >= 0)
        {
            maxStack.Push(item);
        }
    }

    public T Pop()
    {
        if (stack.Count == 0)
        {
            throw new InvalidOperationException("Stack is empty");
        }

        T poppedItem = stack.Pop();

        if (poppedItem.Equals(maxStack.Peek()))
        {
            maxStack.Pop();
        }

        return poppedItem;
    }

    public T Max()
    {
        if (maxStack.Count == 0)
        {
            throw new InvalidOperationException("Stack is empty");
        }

        return maxStack.Peek();
    }
}
```
</details>

**Challenge 5: Generic Key-Value Store**  
Create a generic `KeyValueStore` class that can store key-value pairs of any types. It should have methods for adding a key-value pair, retrieving a value by key, and checking if a key exists.

<details>
<summary>Solution 5</summary>

```csharp
public class KeyValueStore<TKey, TValue>
{
    private Dictionary<TKey, TValue> store = new Dictionary<TKey, TValue>();

    public void Add(TKey key, TValue value)
    {
        store[key] = value;
    }

    public TValue Get(TKey key)
    {
        if (store.TryGetValue(key, out TValue value))
        {
            return value;
        }
        throw new KeyNotFoundException($"Key '{key}' not found");
    }

    public bool ContainsKey(TKey key)
    {
        return store.ContainsKey(key);
    }
}
```
</details>
