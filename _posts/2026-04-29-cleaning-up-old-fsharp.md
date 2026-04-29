# Cleaning Up Old F#

I decided to lightly brush up an old F# script I worked on over a year ago more toward the beginning of my F# and functional programming studies. I'm glad kept it, as it's more evidence of how I'm slowly progressing. (There's nothing like being embarrassed by your old own code. 😄)

For example, check out this block I wrote when I apparently first learned about [computation expressions](https://learn.microsoft.com/en-us/dotnet/fsharp/language-reference/computation-expressions) (CEs):

```fsharp
result {
    let! args = checkArgCount rawArgs
    let! args' = checkStyleName args
    let! args'' = checkInputLength args'
    let! args''' = checkInputChars args''
    return args'''
}
```

That code works, of course, but it's needlessly verbose and prone to errors due to the similar variable names.

I immediately realized that, under the hood, there was just some monadic `bind`ing of the `Result`s going on, so I rewrote the code like this:

```fsharp
rawArgs
|> checkArgCount
>>= checkStyleName
>>= checkInputLength
>>= checkInputChars
```

Terser, clearer, _and_ safer. I love it.

(Not that CEs aren't great too, of course. Just not here.)

For practice, I tried out function composition too. Admittedly, I first tried `>>` out of habit, though of course it didn't work. I immediately realized what I actually needed to combine monadic functions was [the Kleisli composition operator](https://blog.ploeh.dk/2022/04/04/kleisli-composition/):

```fsharp
// Inline version
rawArgs
|> (checkArgCount >=> checkStyleName >=> checkInputLength >=> checkInputChars)

// Bound version, which is likely more practical.
let validate =
    checkArgCount
    >=> checkStyleName
    >=> checkInputLength
    >=> checkInputChars

validate rawArgs
```

I think it's only the second time I've actually used this operator, so I'm glad I recalled it.
