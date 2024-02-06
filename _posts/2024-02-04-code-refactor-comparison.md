# Code Refactor Comparison

While refactoring a method in my [AudioTagger](https://github.com/codeconscious/audiotagger) tool, I found myself undecided between two ways of accomplishing the same task in C#, which was to examine a collection of directory and files paths and partitioning them into `(ImmutableList<string> Valid, ImmutableList<string> Invalid)`—that is, a two-pronged tuple containing partitioned valid (existing) and invalid (nonexistant) directory and file paths.

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

I really like using [`Aggregate()`](https://learn.microsoft.com/en-us/dotnet/api/system.linq.enumerable.aggregate?view=net-8.0) (which corresponds to some other languages' `reduce` function) where I can. Yet, I found myself wondering about the readability of version 2 compared with version 1. The second one is less procedural and more functional, but is the top one easier to read and reason about? Is the second one safer code?

I'm not sure which way I'll go as I write this, but I find the questions intriguing. I think it's the sort of thing we have to keep in mind as we write code.

_Update:_ I came up with a draft of a potential **Version 3** using `GroupBy()`:

```csharp
static ImmutableList<string> extractBranch(
            IEnumerable<IGrouping<bool, string>> group, bool branchKey) =>
                group.Where(r => r.Key == branchKey)
                    .SelectMany(g => g.Select(n => n))
                    .ToImmutableList();

var groups = paths.GroupBy(p => Path.Exists(p));
var valid = extractBranch(groups, true);
var invalid = extractBranch(groups, false);
return new (valid, invalid);
```

In its current state, though, it iterates over `groups` twice, which is less than ideal.

There's no right answer here and the answer might differ in various contexts; however, ultimately, I think the straightforwardness of Version 1 is winning me over. It's important to be practical, after all.
