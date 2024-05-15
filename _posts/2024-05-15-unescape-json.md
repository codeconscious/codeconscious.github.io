# Unescape JSON in .NET

In a personal C# project, I added JSON serialization for a collection of objects. However, I found that the serialized text contained escaped characters, such as  `\u0027` in place of apostrophes.

While looking for a solution, I learned that this can be resolved using [`Regex.Unescape()`](https://learn.microsoft.com/en-us/dotnet/api/system.text.regularexpressions.regex.unescape?view=net-8.0) as seen below. Very nice to know!

```cs
var json = JsonSerializer.Serialize(tagSummary, options);
var unescapedJson = System.Text.RegularExpressions.Regex.Unescape(json);
```

【日本語要約】.NETの[`Regex.Unescape()`](https://learn.microsoft.com/ja-jp/dotnet/api/system.text.regularexpressions.regex.unescape?view=net-8.0)というメソットを使えば、JSONなどでエスケープされた文字（例えば、`\u0027`）を容易に変換することができると知りました。これは使える時は使えますね！
