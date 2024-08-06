# C#: Safer `Dictionary` access in CCVTAC

In my tool [CCVTAC](https://github.com/codeconscious/ccvtac/), there are currently two categories of user inputs, which I model using an enum:

```cs
internal enum InputCategory { Url, Command }
```

(In the future, I might use [a discriminated union](https://codeconscious.github.io/2024/07/30/csharp-type-unions-proposal.html) instead.)

Users can enter inputs of any combination at once. When the user submits their inputs, the program determines the `InputCategory` of each input and places the results in a collection of `CategorizedInput`s:

```cs
internal record CategorizedInput(string Text, InputCategory Category);
```

Additionally, I also generate a key-value pair of the counts of each category, and this step is the subject of this post.

Originally, I used a `Dictionary<InputCategory, int>` for holding the counts. However, there was an issue with this: When the user entered only one category of inputs—i.e., only URLs and no commands, or vice versa—that meant that the unused category would not be added to the dictionary; yet the program would attempt to access that missing `InputCategory` key while counting the occurrences of input of _both_ categories. This, of course, caused `KeyNotFoundException` exceptions to be thrown.

I felt I needed more behavior than what a plain `Dictionary` could provide, so I settled on a custom class wrapping a `Dictionary`.

My initial approach was simply manually ensuring that both categories were added to the `Dictionary` during class construction, adding missing entries with a default of `0` during class construction. This looked something like the unfinished code below:

```cs
internal class CategoryCounts
{
    public FrozenDictionary<InputCategory, int> Counts { get; init; }

    internal CategoryCounts(IDictionary<InputCategory, int> input)
    {
        if (!input.ContainsKey(InputCategory.Url))
        {
            input[InputCategory.Url] = 0;
        }

        if (!input.ContainsKey(InputCategory.Command))
        {
            input[InputCategory.Command] = 0;
        }

        // Ensure all categories have been covered.
        if (input.Keys.Count != Enum.GetNames(typeof(InputCategory)).Length)
            throw new ArgumentException("The", nameof(input));

        Counts = input.ToFrozenDictionary();
    }
}
```

However, if I added more input categories at a later date, it would necessitate remembering to add extra conditionals in this constructor to avoid runtime exceptions, which felt inelegant.

I then throught about iterating over the enum values instead of adding them manually:

```cs
internal class CategoryCounts
{
    public FrozenDictionary<InputCategory, int> Counts { get; init; }

    internal CategoryCounts(IDictionary<InputCategory, int> input)
    {
        // Ensure each category type is present.
        foreach (InputCategory category in Enum.GetValues<InputCategory>())
        {
            if (!input.ContainsKey(category))
                input[category] = 0;
        }

        Counts = input.ToFrozenDictionary();
    }
}
```

This approach is better and allievated my concern above, making the constructor more future-proof. However, I still felt I was missing something. (For one, that public `FrozenDictionary` didn't feel right, though I was glad to try out that new type.)

It was then I realized that I could use indexing to make this far smoother:

```cs
internal class CategoryCounts
{
    private readonly Dictionary<InputCategory, int> _counts;

    internal CategoryCounts(Dictionary<InputCategory, int> counts)
    {
        _counts = counts;
    }

    public int this[InputCategory category]
    {
        get => _counts.TryGetValue(category, out var count) ? count : 0;
    }
}
```

Much better! This approach means that I can access the values in the underlying `Dictionary` by using indexing on an instance of the `CategoryCounts` class, like below, and remain confident that a valid value will always be passed.

```cs
// The variable `counts` is an instance of `CategoryCounts`.
var urlSummary = counts[InputCategory.Url] switch
{
    1 => "1 URL",
    >1 => $"{counts[InputCategory.Url]} URLs",
    _ => string.Empty
};
```

To be fair, I had to review [the documentation](https://learn.microsoft.com/en-us/dotnet/csharp/indexers#dictionaries) to recall exactly how to do this.

I think one minor concern of this approach is that, instead of setting values once in the constructor, the `TryGetValue()` conditional is called each time a value is retrieved. For a larger project, that might be a bigger concern, but I don't think it's particularly relevant here. I'll trust the BCL's performance on this one.

I enjoy this sort of iterative approach. It's always so satisfying and enjoyable to watch code I write gradually improve like this.
