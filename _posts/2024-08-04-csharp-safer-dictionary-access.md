# C#: Safer `Dictionary` access in CCVTAC

In my tool [CCVTAC](https://github.com/codeconscious/ccvtac/), there are currently two categories of user inputs, which I model using an enum:

```cs
internal enum InputCategory { Url, Command }
```

(In the future, I might use [a discriminated union](https://codeconscious.github.io/2024/07/30/csharp-type-unions-proposal.html) instead.)

Users can enter inputs of any combination at once. When the user submits their inputs, the program determines the category of each input and places the results in a collection of `CategorizedInput`s:

```cs
internal record CategorizedInput(string Text, InputCategory Category);
```

Additionally, I also generate a key-value pair of the counts of each category. Originally, I used a `Dictionary<InputCategory, int>` for this.

However, there was an issue: When the user entered only one category of inputs—e.g., only URLs and no commands—that meant that the unused category would not be added to the dictionary; yet the program would attempt to access that missing key while counting the occurrences of items of both categories. This caused a `KeyNotFoundException` exception to be thrown.

I felt I needed more behavior than what a plain `Dictionary` could provide, so I settled on a custom class wrapping a `Dictionary`.

My initial idea was to simply manually ensuring both categories were added to the `Dictionary` during class construction, adding missing entries with a default of `0` where necessary. This looked something like the unfinished code below:

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

However, if I added more input categories at a later date, it would necessitate remembering to add extra conditionals in this constructor, which felt inelegant.

I then considered a similar approach, instead iterating over the enum values instead of adding them manually:

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

This approach allievated my concern above, making the constructor more future-proof even if I add more input categories in the future. However, I still felt I was missing something. For one, that public `FrozenDictionary` didn't feel right (though I was glad to try out that new type).

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

Much better! This approach means that I can access the values in the underlying `Dictionary` by using indexing on class instances, like below, and remain confident that a valid value will always be passed.

```cs
var urlSummary = counts[InputCategory.Url] switch
{
    1 => "1 URL",
    >1 => $"{counts[InputCategory.Url]} URLs",
    _ => string.Empty
};
```

I think one minor concern of this approach, though, is that instead of a single set operation in the constructor, the `TryGetValue()` conditional is called each time a value is retrieved. For a larger project, that might be a bigger concern, but I don't think it's particularly relevant here. I trust the BCL's performance on this one.

I enjoy this sort of iterative approach. It's deeply satisfying and enjoyable to watch my code gradually improve like this.
