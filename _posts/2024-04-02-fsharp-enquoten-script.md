# F# "enquoten" script

As part of my F# studies, I created a script that processes text files by (1) truncating lines to a specified maximum length and (2) prepending `> ` to the beginning of lines, thereby quoting them as in plain text emails.

<script src="https://gist.github.com/codeconscious/6e098acad292171667eda3862aa6cdc7.js"></script>

I'm still tinkering with it, but it has been a suprisingly good little exercise. I'm sure it can be done much better (and probably even as a crazy bash one-liner 😄), but I'm pretty pleased with it.

In particular, I had the idea to create a tool like this when I realized that it was a perfect chance for practicing tail-recursive functions.
