# Seal All Internal Classes
Explicitly seal all your classes by default unless it need to be inherited in a known situation. Sealed classes offer aggregated perfomance benifits that is 10x to 1000x faster than open classes.

```csharp
public class OpenClass
{
}

public sealed class SealedClass
{
}
```

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
