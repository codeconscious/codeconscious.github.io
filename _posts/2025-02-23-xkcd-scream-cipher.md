# xkcd Scream Cipher

Popular webcomic [xkcd](https://xkcd.com) posted a comic ([#3054](https://xkcd.com/3054/)) that presented a cipher in which all letters are converted to the letter `A` with various diacritics (e.g., `A̋`, `A̧`, `A̤`). This seemed like it would be a nice little programming exercise—and I found that others in [a related Reddit thread](https://old.reddit.com/r/xkcd/comments/1iuwko7/xkcd_3054_scream_cipher/) had the same idea, which further spurred me on—so I spent some time this afternoon implementing my own version.

I briefly debated whether to build it in Ruby (which I use at work) or F#, but I yet again couldn't resist the allure of F# for this. Along with being more enjoyable to work in, I appreciate how F# (and, presumably, other functional languages) makes it suitably easy to write satisfyingly robust code. (Aside: I'm pretty surprised that C# wasn't even in this equation, given that it's been my go-to language for years until recently.)

My implementation is in my scripts repo: [**XkcdScreamCipher.fsx**](https://github.com/codeconscious/scripts/blob/main/fsharp/XkcdScreamCipher.fsx).

It was fun to make! I perhaps went a wee bit overboard for what's essentially a throwaway script, but part of the reason for the exercise at all is to enjoy myself. ☺️

## Usage examples

Here are some usage examples. Note that `dfsi` is my alias for `dotnet fsi`.

```sh
$ dfsi fsharp/XkcdScreamCipher.fsx --encode "hello"
A̰ÁĂĂÅ
```

```sh
$ dfsi fsharp/XkcdScreamCipher.fsx --decode A̰ÁĂĂÅ
HELLO
```

```sh
# `--test` confirms there are no conversion issues with the given string(s).
$ dfsi fsharp/XkcdScreamCipher.fsx --test "hello" "hi" "how neat\!" 123
OK: HELLO --> A̰ÁĂĂÅ --> HELLO
OK: HI --> A̰Ả --> HI
OK: HOW NEAT! --> A̰ÅȀ ÂÁAĀ! --> HOW NEAT!
OK: 123 --> 123 --> 123
```

## StringInfo.SubstringByTextElements method

Through this exercise, I learned about [the StringInfo.SubstringByTextElements method in the System.Globalization namespace](https://learn.microsoft.com/en-us/dotnet/api/system.globalization.stringinfo.substringbytextelements?view=net-9.0). It was necessary for properly iterating over encoded Unicode composed characters, instead of their composite parts, when decoding.

You can read a bit more about Unicode normalization in my recent post "[Unicode Normalization Forms and Recursive Path Normalizer (F# Script)](https://codeconscious.github.io/2025/02/01/recursive-path-normalizer.html)."

## Argument issue

I experienced one fascinating issue while setting up argument validation.

I had originally intended to allow `-d` as an argument to indicate that the provided input should be decoded back to standard letters. However, when examining the arguments during validation, `-d` would always be combined with the following argument. (For example, if I passed `-d "A̰ÁĂĂÅ"`, the first argument would be `-d:A̰ÁĂĂÅ` during runtime, which led to spurious validation failures.)

I was pretty confused until I came across an issue on the official F# repository entitled "[fsi.CommandLineArgs different behavior on -d/-r/-I args, ignores --](https://github.com/dotnet/fsharp/issues/10819)," which confirmed it as a bug and explained why it occurs.

I'm glad I came across that issue! I might have to figure out what I want to do as a workaround for that, though it's hardly a big deal either way.

