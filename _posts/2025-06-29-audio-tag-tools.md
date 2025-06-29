# Learning F# Type Providers via Audio Tag Tools

## Background

I've been handling many audio tag–related tasks in my C# tool [AudioTagger](https://github.com/codeconscious/audiotagger/). (Wow, its development began on Feb 12, 2021—over four years ago!) However, AudioTagger works by first loading the metadata of all files underneath a specific directory. This has become inconvenient because the audio files on which I use it are on a slow external drive—and there are many of them. Reading that data takes over 20 minutes each time I run it. (In retrospect, a TUI interface likely would have been more efficient. I might still implement that someday.)

## The Problem

I realized, though, that some operations, such as searching for duplicates, could work just as well from a cached version of the file tags. Originally, I thought about incorporating support for reading cached tags into AudioTagger, but it was turning out to be a bigger refactor than I wanted to commit to. (That said, it does support caching tags to JSON—just not reading those files.)

## The Solution

Ultimately, I created [**Audio Tag Tools**](https://github.com/codeconscious/audio-tag-tools), something of a complement to AudioTagger that handles a subset of its operations and works with cached tags in JSON files. Thanks to this application, the time required for searching for duplicates, for example, has literally dropped from about **20 minutes to 20 seconds**. 😲

Another reason I opted to create it was because it seemed to be a natural project to learn [F# type providers](https://learn.microsoft.com/en-us/dotnet/fsharp/tutorials/type-providers/), which I've seen touted as one of F#'s best features. I used JSON type providers in Audio Tag Tools and, indeed, they are pretty nice. I simply provide a sample JSON string, and F# parses it and automatically creates all the necessary types for it without me needed to do so manually. (You can see the samples I added for [cached file tags](https://github.com/codeconscious/audio-tag-tools/blob/205918d2a6907bc595a65dcf273be0ef641d7a41/src/AudioTagTools.Cacher/Tags.fs#L31-L47) and [duplicate search settings](https://github.com/codeconscious/audio-tag-tools/blob/205918d2a6907bc595a65dcf273be0ef641d7a41/src/AudioTagTools.DuplicateFinder/Settings.fs#L6-L33).) It's convenient, no doubt.

I've also been learning to use more functions in the [FsToolkit.ErrorHandling](https://demystifyfp.gitbook.io/fstoolkit-errorhandling) package. I thought [`Result.tee`](https://demystifyfp.gitbook.io/fstoolkit-errorhandling/fstoolkit.errorhandling/result/teefunctions#tee) was pretty interesting in how it simplifies introducing side effects in a monadic pipeline. There's a _lot_ more to work with in that package, though.

The feature overlap with AudioTagger does bug me, though. To avoid needing to maintain duplicate features in both applications, I might remove the duplicates from AudioTagger. I'm probably the only user that would be affected by this, and I don't mind. 😉
