# Fastest Loop
Most efficient loop with faster speeds and no allocations. If performing only iterations and no data mutations use this one to boost perfomance 

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
