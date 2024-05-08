# F# "enquoten" script

As part of my F# studies, I created a script that processes text files by (1) truncating lines to a specified maximum length and (2) prepending `> ` to the beginning of lines, thereby quoting them as in plain text emails.

<script src="https://gist.github.com/codeconscious/6e098acad292171667eda3862aa6cdc7.js"></script>

I'm still tinkering with it, but it has been a suprisingly good little exercise. I'm sure it can be done much better (and probably even as a crazy bash one-liner, though I'd argue this is far easier to debug 😄), but I'm pretty pleased with it as a relatively newbie to the language.

I had the idea to create a tool like this when I realized that it was a perfect chance for practicing tail-recursive functions.

_Edit:_ I've since made several updates from [the initial version](https://gist.github.com/codeconscious/6e098acad292171667eda3862aa6cdc7/dd8dacabc72f91f0c5af079dba31a08963112078) and have add features as computation expressions and generics too!

## Example

Source text from [Wikipedia's F# page](https://en.wikipedia.org/wiki/F_Sharp_(programming_language)), which I saved to a local text file:

> F# (pronounced F sharp) is a general-purpose, strongly typed, multi-paradigm programming language that encompasses functional, imperative, and object-oriented programming methods. It is most often used as a cross-platform Common Language Infrastructure (CLI) language on .NET, but can also generate JavaScript and graphics processing unit (GPU) code.
> 
> F# is developed by the F# Software Foundation, Microsoft and open contributors. An open source, cross-platform compiler for F# is available from the F# Software Foundation. F# is a fully supported language in Visual Studio and JetBrains Rider. Plug-ins supporting F# exist for many widely used editors including Visual Studio Code, Vim, and Emacs.
> 
> F# is a member of the ML language family and originated as a .NET Framework implementation of a core of the programming language OCaml. It has also been influenced by C#, Python, Haskell, Scala and Erlang.

Output from `dotnet fsi Enquoten.fsx 40 "> " ~/Downloads/fsharp.txt`:

```fundamental
> F# (pronounced F sharp) is a 
> general-purpose, strongly typed, 
> multi-paradigm programming language 
> that encompasses functional, 
> imperative, and object-oriented 
> programming methods. It is most often 
> used as a cross-platform Common 
> Language Infrastructure (CLI) 
> language on .NET, but can also 
> generate JavaScript and graphics 
> processing unit (GPU) code.
> 
> F# is developed by the F# Software 
> Foundation, Microsoft and open 
> contributors. An open source, 
> cross-platform compiler for F# is 
> available from the F# Software 
> Foundation. F# is a fully supported 
> language in Visual Studio and 
> JetBrains Rider. Plug-ins supporting 
> F# exist for many widely used editors 
> including Visual Studio Code, Vim, 
> and Emacs.
> 
> F# is a member of the ML language 
> family and originated as a .NET 
> Framework implementation of a core of 
> the programming language OCaml. It 
> has also been influenced by C#, 
> Python, Haskell, Scala and Erlang. 
```
