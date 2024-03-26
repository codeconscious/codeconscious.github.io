# Thinking About Recursive Functions

The other evening, after learning [at Wikibooks](https://en.wikibooks.org/wiki/F_Sharp_Programming/Recursion#Greatest_Common_Divisor_(GCD)) that two numbers' greatest common divisor can be calculated recursively and that the process for doing so was determined by Euclid way back when (around 300 BC!), it naturally brought F# recursive functions to mind.

Out of a desire to toy with one right quick, I quickly created this very simple one for practice:


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

Yes, it's quite simple, but still being very new to functional languages and F# syntax, I was glad to be able to put it together so quickly. It wouldn't have been particularly possible (at least, not without significantly more research and time) a few weeks ago, and it's important to celebrate even small personal wins and development. (I think this is the first time I've used the cons operator as well. Nice.)

I'm working on something slightly meatier, though, that I'll post about soon.
