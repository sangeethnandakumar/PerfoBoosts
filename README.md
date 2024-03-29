# Use-Case Based Optimisations

## HashSet vs List

### Use HashSet
- If order is not important
- All values are unique
- Extreamily fast lookups
- O(1) time complexity

### Use List
- Order is important
- Values can be duplicate
- Fast indexed access
- O(n) time complexity

## IEnnumerable vs List

### Use IEnnumerable
- Better for Read only use cases
- More memory efficient & Less overhead
- Don't use for frequent access
- Slower if foreach and LINQ/LAMBDA involved as each iteration reads again without catching

### Use List
- Use when Read/Write is involved
- Use for catched frequent access
- Use on foreach and LINQ/LAMBDA














# 1. Aggregated Perfomance Boosting - By Sealing Classes
Explicitly seal all your classes by default unless it need to be inherited in a known situation. Sealed classes offer aggregated perfomance benifits that is 10x to 1000x faster than open classes.

> 10 to 10,000X Faster

```csharp
public class OpenClass
{
}

public sealed class SealedClass
{
}
```
![image](https://user-images.githubusercontent.com/24974154/190895170-26b51d10-7ee5-41e7-8c93-e3ae91d52241.png)

---

# 2. Fastest Assending Sort - By Adaptive Sort In Span.Sort()
Span soft is mutable. Which means as it sorts it mutates the collection. Beware in order critical scenerios when using.

> 3 to 4X Memory efficient

> 2X Faster

```csharp
using System.Runtime.InteropServices;
```
![image](https://user-images.githubusercontent.com/24974154/190895033-4cedb2e3-633c-4c9e-b317-c35db2378f8b.png)

---

# 3. Efficient Iteration - By Marshalling IEnumerable to Span<T>
Most efficient loop with faster speeds and no allocations. If performing only iterations and no data mutations use this one to boost perfomance 

 > 100% Memory efficient

> 2X Faster
    
```csharp
using System.Runtime.InteropServices;

foreach (var item in CollectionsMarshal.AsSpan(items))
{
    // Don't mutate item as it is span
    // Use only for readonly iterations
}

var collectionAsSpan = CollectionsMarshal.AsSpan(items);
for (var i = 0; i < collectionAsSpan.Length; i++)
{
    // Don't mutate item as it is span
    // Use only for readonly iterations
}
```
![image](https://user-images.githubusercontent.com/24974154/190895076-359bd5d8-8962-48f5-b8ed-78bfb74f67f9.png)

---

 # 4. Hyper Fast Aggregate Functions For Primitive Collections - By .NET 7 BuiltIn Hadrdware Vectorization (If supported)
Upgrade to .NET 7 if you use primitive collection aggregate functions a lot. Your hardware must support vectorization else the function will fallback to normal compute.

 > 100% Memory efficient

> 10 to 40X Faster
    
```csharp
using System.Runtime.InteropServices;

foreach (var item in CollectionsMarshal.AsSpan(items))
{
    // Don't mutate item as it is span
    // Use only for readonly iterations
}

var collectionAsSpan = CollectionsMarshal.AsSpan(items);
for (var i = 0; i < collectionAsSpan.Length; i++)
{
    // Don't mutate item as it is span
    // Use only for readonly iterations
}
```
 
 ![image](https://user-images.githubusercontent.com/24974154/190895304-8dd2f9ef-1394-4b98-a475-1cfa542c930d.png)

---

 # 5. HardCast To Get Back From Object Collection - Using typeof()
Use a hard cast like this when casting instances out of object collections for maimum perfomance gains

> 40X Faster

```csharp
    public List<object> MyCollection { get; set; }

    public List<Person> HardCast_TypeOf()
    {
        return MyCollection
            .Where(x => x.GetType() == typeof(Person))
            .Select(x => (Person)x)
            .ToList();
    }
```

![image](https://user-images.githubusercontent.com/24974154/190919773-8e4a2234-673c-4a7c-90c9-b1ae008d7600.png)
 
 ---

 # 6. Using List Patterns - For Powerfull Pattern Matching Switch Cases
Use a hard cast like this when casting instances out of object collections for maimum perfomance gains

```csharp
 //Simple cases
var names = new[] { "Sangeeth", "Nandakumar", "Navaneeth", "Nandakumar" };

var text = names switch
{
    [_, .. string[] middle, _] => $"Middle values are {string.Join(",", middle)}",
    _ => "Default pattern"
};

Console.WriteLine(text);

//Complex Jagged cases
var jagedArray = new[]
{
    new [] {1,2,3,4},
    new [] {5,6,7, 8},
    new [] {9,10,11,12},
};
var val = jagedArray switch
{
    [.., [_, .. int[] middle, _]] => $"Last array's middle values are {string.Join(",", middle)}",
    _ => "Default pattern"
};

Console.WriteLine(val);
Console.Read();
```
