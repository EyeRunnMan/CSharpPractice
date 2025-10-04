# DateTimeOffset

```csharp

// Here The intent is to under stand difference between Date Time and Date Time Offset

// there is DateTime and DateTimeOffset

// But DateTime alone is not enough to represent a point in time unambiguously.
// DateTimeOffset represents a point in time relative to UTC (Coordinated Universal Time) by including an offset.
// DateTimeOffset is particularly useful in scenarios where you need to work with dates and times across different time zones.
// DateTime.Now gives you the current date and time of the system's local time zone. without any offset information.
// DateTime.UtcNow gives you the current date and time in Coordinated Universal Time (UTC).
// DateTimeOffset.Now gives you the current date and time along with the offset of the system's local time zone from UTC.

// Same moment in time, different representations:
DateTimeOffset newYork = new DateTimeOffset(2025, 10, 2, 14, 0, 0, TimeSpan.FromHours(-4));
DateTimeOffset london = new DateTimeOffset(2025, 10, 2, 19, 0, 0, TimeSpan.FromHours(1));
DateTimeOffset tokyo = new DateTimeOffset(2025, 10, 3, 3, 0, 0, TimeSpan.FromHours(9));

// All three are equal when compared:
Console.WriteLine(newYork == london);  // True - same instant in time!
```
