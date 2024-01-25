# F# Koans

On the heels of [completing Ruby koans](https://codeconscious.github.io/2024/01/08/ruby-koans.html), I've also [completed](https://github.com/codeconscious/FSharpKoans) a set of [F# koans](https://github.com/ChrisMarinos/FSharpKoans). This set wasn't quite as robust as the Ruby ones, but it was a fun and productive exercise.

This set included one apply-what-you've-learned exercise. After some struggling with the syntax, I was very happy to come up with the following solution:

```fsharp
let YouGotTheAnswerCorrect() =
    let splitCommas (x:string) = x.Split([|','|])

    let parsedDiff opn close =
        let parsedDouble strNum = System.Double.Parse(strNum, CultureInfo.InvariantCulture)
        parsedDouble(close) - parsedDouble(opn)

    let largestOpenCloseDiff list =
        list
        |> List.skip 1 // The header row
        |> List.map splitCommas
        |> List.maxBy (fun line -> parsedDiff line[1] line[4])
        |> Array.item 0

    AssertEquality "2012-03-13" (largestOpenCloseDiff stockData)
```

It's simple, but this is the first real F# I've ever written. It takes some getting used to, but I'm definitely starting to understand the appeal of F#—and of functional languages—a bit more.
