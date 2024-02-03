# Code Refactor Comparison

While refactoring a method in my [AudioTagger](https://github.com/codeconscious/audiotagger) tool, I found myself undecided between two ways of accomplishing the same task, which was to examine a collection of directory and files paths and partitioning them into `(ImmutableList<string> Valid, ImmutableList<string> Invalid)`—that is, a two-pronged tuple with named members containing partitioned valid and invalid paths.

I've included the two versions I had, as written in C# 12, below:

**Version 1:**

```csharp
List<string> valid = [];
List<string> invalid = [];

foreach (string path in paths)
{
    if (Path.Exists(path))
        valid.Add(path);
    else
        invalid.Add(path);
}

return new ([.. valid], [.. invalid]);
```

**Version 2:**

```csharp
var results = paths.Aggregate(
    new Dictionary<bool, List<string>>
    {
        [true] = [], // To hold valid paths (i.e., those that exist)
        [false] = [] // To hold invalid paths
    },
    (memo, path) => {
        memo[Path.Exists(path)].Add(path);
        return memo;
    },
    memo => memo
);

return new ([.. results[true]], [.. results[false]]);
```

I really like using [`Aggregate()`](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.aggregate?view=net-8.0) (which corresponds to some other languages' `reduce` function) where I can. Yet, I found myself wondering about the readability of version 2 compared with version 1. It's more procedural, but perhaps easier to read?

I'm not sure which way I'll go as I write this, but I think the question is intriguing.
