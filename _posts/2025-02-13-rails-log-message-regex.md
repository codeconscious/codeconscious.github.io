# Regex: Extract messages from Rails logs

Today, I wanted to extract only the `message` fields from JSON-formatted Ruby on Rails logs in my terminal.

So, I created this simple regular expression to accomplish this easily using a lookahead and lookbehind:

```
^.*,(?="message")|(?<="message":".*").*
```

Copying and pasting the relevant logs into VS Code and then replacing all text matched by this regex did the trick.

Ain't regex fun? ^_^

<hr>

**Update:** This is a slightly improved version that doesn't choke on `\"` within messages:

```
^.*,(?="message")|(?<="message":".*(?<!\\)").*
```
