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


# 2. Fastest Assending Sort - By Adaptive Sort In Span.Sort()
Span soft is mutable. Which means as it sorts it mutates the collection. Beware in order critical scenerios when using.

> 3 to 4X Memory efficient

> 2X Faster

```csharp
using System.Runtime.InteropServices;
```
![image](https://user-images.githubusercontent.com/24974154/190895033-4cedb2e3-633c-4c9e-b317-c35db2378f8b.png)

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

 # 4. Hyper Fast Aggregate Functions For Int Collections - By .NET 7 BuiltIn Hadrdware Vectorization (If supported)
Upgrade to .NET 7 if you use int collection aggregate functions a lot. Your hardware must support vectorization else the function will fallback to normal compute.

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

