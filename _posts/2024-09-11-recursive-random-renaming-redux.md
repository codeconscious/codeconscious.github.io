# Recursive Random Renaming Redux

I just couldn't help myself... I recreated [my Ruby script from the other day](https://codeconscious.github.io/2024/09/05/recursive-random-renaming.md.html) as an F# script: [**RecursiveRandomRename.fsx**](https://github.com/codeconscious/scripts/blob/main/fsharp/RecursiveRandomRename.fsx).

As usual, the experience was enjoyable and educational. I'm still early in my functional journey, but I think this style of programming really agrees with me. That said, I struggled a bit more than I thought I would to get the recursive section just right—but I nailed it in the end.

I think one of the personal highlights for me was discovering right at the end that I could elide `fun` in a couple places, as seen below:

```fs
// Before
allDirectoryItems args.Directory args.IncludedExtensions false
|> Seq.map (fun itemInDir -> rename itemInDir)
|> Seq.iter (fun result -> print result)

// After
allDirectoryItems args.Directory args.IncludedExtensions false
|> Seq.map rename
|> Seq.iter print
```

That's just lovely.
