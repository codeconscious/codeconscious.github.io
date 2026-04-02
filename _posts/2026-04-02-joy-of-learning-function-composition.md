# The Joy of Learning, Function Composition–Style

I'm just sharing a very small FP epiphany I had this evening.

I had this code:

```fsharp
|> Array.filter (fun (_, tags) -> Array.hasMultiple tags)
```

Looking at this, I wondered if I could use function composition to improve this a bit, skipping the lambda entirely.

So, I tried this:

```fsharp
|> Array.filter (snd >> Array.hasMultiple)
```

And, lo, it worked! That small tweak is just so much more elegant. (Is it as idiomatic? I can't say, but I find it perfectly readable in its context.)

For those familiar with FP, this is likely a painfully obvious improvement, but I think it represents real progress in learning to think more functionally. Such a small thing, but there's no way could I have figured that out a year or so ago! Celebrate the small wins, I say.

There are few things as satisfying as learning and improving in something that truly interests you.
