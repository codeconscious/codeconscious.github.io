# F# Script: Convert Text to Slack Emoji

After first creating [the Ruby version of this](https://codeconscious.github.io/2024/06/25/ruby-text-to-slack-emoji.html) the other day, I couldn't resist doing it in F# as well over the three-day holiday.

Some minor highlights:
- This was my first time using the `Literal` attribute.
- I made use of F# 8's "_.Property" shorthand.
- I used `eprintfn` to print to STDERR. (I forget to use this...)

<script src="https://gist.github.com/codeconscious/56cef39c6e9869ab02080c12dc2114c6.js"></script>
