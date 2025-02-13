# Regex: Extract messages from Rails logs

Today, I wanted to extract only the `message` fields from JSON-formatted Ruby on Rails logs in my terminal. This regular expression that I created helped me accomplish this easily:

```
^.*,(?="message")|(?<="message":".*").*
```

Copying and pasting the relevant logs into VS Code, then replacing all the text matched by this regex did the trick.

Ain't regex fun? ^_^
