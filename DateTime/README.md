# DateTime

```csharp
// Unix time(also called Unix timestamp or epoch time) is a way of tracking time as a single number.
// The Concept:
// It's the number of seconds that have elapsed since:

// January 1, 1970 at 00:00:00 UTC(called the "Unix epoch")

// Examples:
// Unix Time: 0 = January 1, 1970 00:00:00 UTC
// Unix Time: 1000000000 = September 9, 2001 01:46:40 UTC
// Unix Time: 1727787600 = October 1, 2025 09:00:00 UTC(example)
// Why It's Useful:

// Simple - Just one number instead of year/month/day/hour/minute/second
// Easy math - Calculate time differences by subtracting: 1000 - 500 = 500 seconds
// No timezone confusion - Always in UTC
// Universal - Works across all programming languages and systems
// Compact - Easy to store in databases

// Real World Example:
// csharplong meeting1 = 1727787600;  // 9:00 AM
// long meeting2 = 1727791200;  // 10:00 AM

// long difference = meeting2 - meeting1;
// Console.WriteLine($"{difference} seconds apart");  // 3600 seconds (1 hour)
// Variations:

// Seconds: Standard Unix time(most common)
// Milliseconds: Unix time × 1000(used in JavaScript, some APIs)
// Microseconds: Unix time × 1,000,000

// Unix time will eventually have the "Year 2038 problem" when 32-bit systems overflow, but 64-bit systems are safe for billions of years!


// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");

DateTime dateTime = DateTime.UtcNow;
Console.WriteLine("_____________");
Console.WriteLine("dateTime" + dateTime);
Console.WriteLine("dateTime.ToString()" + dateTime.ToString());
Console.WriteLine("dateTime.ToBinary() " + dateTime.ToBinary());
Console.WriteLine("dateTime.Ticks" + dateTime.Ticks);
long epochSeconds = DateTimeOffset.UtcNow.ToUnixTimeSeconds();
Console.WriteLine("epoch " + epochSeconds);



```
