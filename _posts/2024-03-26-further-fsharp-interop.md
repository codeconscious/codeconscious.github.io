# Further F# Interop

This evening, I merged [another F# PR](https://github.com/codeconscious/ccvtac/pull/38) in the same project as [last time](https://codeconscious.github.io/2024/02/29/first-foray-into-fsharp.html). The first PR covered downloading; in this PR, I moved most of the code related to user settings to the F# library project.

As part of this, I had the opportunity to work with JSON serialization and deserialization in an F# context. Here's a sample of the new code:

```fsharp
[<CompiledName("Read")>]
let read filePath =
    let (FilePath path) = filePath

    let verify settings =
        let isEmpty str = String.IsNullOrWhiteSpace str
        let dirMissing str = not <| (Directory.Exists str)

        match settings with
        | { WorkingDirectory = w } when isEmpty w -> Error $"No working directory was specified."
        | { WorkingDirectory = w } when dirMissing w -> Error $"Working directory \"{w}\" is missing."
        | { MoveToDirectory = m } when isEmpty m -> Error $"No move-to directory was specified."
        | { MoveToDirectory = m } when dirMissing m -> Error $"Move-to directory \"{m}\" is missing."
        | _ -> Ok settings

    try
        path
        |> File.ReadAllText
        |> JsonSerializer.Deserialize<UserSettings>
        |> verify
    with
        | :? FileNotFoundException -> Error $"\"{path}\" was not found."
        | :? JsonException -> Error $"Could not parse JSON in \"{path}\" to settings."
        | e -> Error $"Settings unexpectedly could not be read from \"{path}\": {e.Message}"
```

It might not be amazing F#, but I'm pretty fond of it. The backward pipe into `not`, the `match`ing, the argument-free `try` pipeline, even the exception handling—it was fun!

Incidentally, `[<CompiledName("Read")>]` sets how the function name will appear in the C# project, which pulls in the library as a reference. Since method and function names in C# are Pascal case, this helps reduce any visual dissonance induced via lowercase function names.

A small downside of this move is that I still have a C# wrapper class that handles calling the F# code, which is less than ideal, but I can look into that more later. I also need to think about how much of the tool I want to port over to F#. Honestly, unless I get distracted or otherwise pulled away, I might just keep transferring more and more of the C# over to F#. Thus far, it's been both educational and entertaining!
