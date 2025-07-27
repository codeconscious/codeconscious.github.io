# Option Pipeline Vs. If-Then

This morning, I happened to glance at this block of code in [my Audio Tag Tools repo](https://github.com/codeconscious/audio-tag-tools/):

```fsharp
let title =
    fileTags.Title
    |> Option.ofObj // Converts an external nullable string to an Option.
    |> Option.map _.Normalize()
    |> Option.defaultValue String.Empty
```

I wondered offhand if, in this case, there was any real benefit to using the `Option` type methods in a pipeline like this.

So, as an experiment, I rewrote it using if-then syntax:

```fsharp
let title' =
    let title = fileTags.Title
    if title <> null
    then String.Empty
    else title.Normalize()
```

There didn't seem to be much of a difference to my eye.

Until I spotted the bug I introduced. Did you catch it? (If not, have another look.)

As you've noticed, I'd inadvertently switched the expressions to return, thus breaking the logic and carelessly introducing a bug that could have resulted in an unslightly runtime error. (To be fair, I wasn't concentrating on this. At least I noticed it right away. 😅)

The correct code, of course, should look like this:

```fsharp
let title' =
    let title = fileTags.Title
    if title <> null
    then title.Normalize()
    else String.Empty
```

I tried introducing a similar bug in the pipeline version, but because it results in passing incorrect types to its functions, it doesn't even compile, thus preventing that bug altogether:

```fsharp
// This does not compile!
let title =
    fileTags.Title
    |> Option.ofObj
    |> Option.map String.Empty // This expression was expected to
                               // have type 'String -> 'a' but
                               // here has type 'string'
    |> Option.defaultValue _.Normalize() // Lookup on object of
                                         // indeterminate type [...]
```

Lovely. For me, this simple quasi–real life example did a good job of demonstrating the advantage of the pipeline version. I'll be keeping that code as it is.
