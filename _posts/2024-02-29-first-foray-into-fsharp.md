# First Foray Into F#

On the heels of [completing F# koans](https://codeconscious.github.io/2024/01/25/fsharp-koans.html), I wanted to see if I could integrate F# into [a small C# command line application](https://github.com/codeconscious/ccvtac) I created and tinker on regularly. I started it as an experiment, but things went so well that I decided to merge the branch into `main` this evening. So, now my application leverages both C# and F#. I even created some F# tests as well.

Interop with C# was incredibly easy: I only needed to add a reference to the F# project from the C# one in order to access the F# entities and functions. Being able to use both C# and F# so easily in one solution—and in the very same file—was rather exhilarating.

One of the most exciting parts was realizing that [my one F# file](https://github.com/codeconscious/ccvtac/blob/main/CCVTAC/CCVTAC.FSharp/Downloading.fs) could replace 7 C# files (1 interface and 6 classes). That said, that's not a criticism of C# but instead of the overly OOP way in which I arranged those classes in the first place. Modern C# can be written in a more functional style, after all. But where it's more optional in C#, F# compels you to think more in that way, and I like that.

Also, I found that C# automatically provided helper properties for discriminated union cases from F#. For example, I have a union type called `MediaType` that contains a case called `Video`, and within C# I had access to the boolean property `IsVideo` automatically. I didn't know about that feature, but it was an exciting—and quite convenient, since I no longer needed `GetType()` like I thought I did—little discovery.

All in all, I really enjoyed my first foray into F#! It was definitely challenging since it's a different paradigm and because I just kind of jumped in. However, the advantages of functional programming are more apparent to me now, and I definitely want to work with F# more. I'm likely to integrate it further into the same application.
