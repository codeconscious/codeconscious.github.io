# Fixing Rust koan errors in Visual Studio Code

After completing [Ruby](https://codeconscious.github.io/2024/01/08/ruby-koans.html) and [F#](https://codeconscious.github.io/2024/01/25/fsharp-koans.html) koans, I've begun on [Rust koans](https://github.com/crazymykl/rust-koans) since I've been away from Rust for a while. However, immediately after beginning, I experienced rampant "This rust file does not belong to a loaded cargo project" errors in VS Code, basically each time I typed something.

After looking into the issue, I came across [a rust analyzer GitHub issue](https://github.com/rust-lang/rust-analyzer/issues/14523) that contains [a simple workaround](https://github.com/rust-lang/rust-analyzer/issues/14523#issuecomment-1911743855), which I'll summarize below, adapted for the Rust koans repository:

1. Add `mod koans` to `main.rs`
2. Create a new file in the `src` directory named `koans.rs`

This was sufficient to resolve the issue for me.
