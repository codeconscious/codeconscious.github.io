# `grep`ping `curl` output

By chance, I [learned](https://unix.stackexchange.com/a/166360) today that curl writes its output to stderr, not stdout. Thus, if you want to want to apply `grep` to `curl` output, you first need to redirect `curl`'s output to stdout.

Someone at my company asked about this, so here's the brief sample I shared with them:

```sh
curl -v --silent https://www.google.com --stderr - | grep "^\* Connected to"
```

That's interesting. I was quite confused at first when my original `grep` command seemed to have no effect!
