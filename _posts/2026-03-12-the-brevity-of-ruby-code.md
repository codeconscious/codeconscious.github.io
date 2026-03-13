# On The Brevity of Ruby Code

Today at work, I wanted to create a small script to reduce multiline strings to single-line ones with `\n` as a separator.

I started with F#, ending up with the code below, which uses [my general-use library](https://www.nuget.org/packages/CCFSharpUtils/):

```fsharp
#r "nuget: CCFSharpUtils"

open CCFSharpUtils.Library
open System.Diagnostics

let readClipboard () =
    let psi = ProcessStartInfo("pbpaste",
        RedirectStandardOutput = true,
        UseShellExecute = false)
    use p = Process.Start psi
    p.StandardOutput.ReadToEnd().TrimEnd()

readClipboard ()
|> _.Split(String.newLine)
|> Array.map String.trim
|> String.concat "\\n"
|> printfn "%s"
```

This is the equivalent Ruby:

```rb
puts `pbpaste`
        .split(/\r?\n/)
        .map(&:strip)
        .join("\\n")
```

That's a striking difference! That `pbpaste` line is pretty slick.

I feel this highlights Ruby's strength as a scripting language. For much larger scripts (and certainly for actual non-script projects), I would choose F# or another statically typed language (because brevity isn't _everything_), but this helped me appreciate Ruby's brevity anew and reiterated to me how it's a natural choice for smaller scripts like this.

(Note: This code likely only works on macOS because it leverages its [`pbpaste`](https://ss64.com/mac/pbpaste.html) command.)
