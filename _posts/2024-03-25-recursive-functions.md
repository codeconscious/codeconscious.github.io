# Thinking About Recursive Functions

The other evening, after learning [at Wikibooks](https://en.wikibooks.org/wiki/F_Sharp_Programming/Recursion#Greatest_Common_Divisor_(GCD)) that two numbers' greatest common divisor can be calculated recursively and that the process for doing so was determined by Euclid way back when (around 300 BC!), it naturally brought F# recursive functions to mind.

Here's a very simple one that I drew up quickly for practice:


```fsharp
let printEachChar str =
    let chars = str |> Seq.toList
    let rec loop chars =
        match chars with
        | [] -> ()
        | h :: t ->
            printf " > %c" h
            loop t
    loop chars
```

Yes, it's simple, but still being very new to functional languages and syntax, I was glad to be able to put it together so quickly. It wouldn't have been particularly possible a few weeks ago, and it's important to celebrate the small wins.

I'm working on something slightly meatier, though, that I'll post about soon.
