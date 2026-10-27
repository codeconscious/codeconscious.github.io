# Auto-wrap Git commit messages in Vim

(tl;dr: Add `filetype plugin on` to .vimrc.)

---

I've been using Copilot much more at work recently, and for more LLM-heavy code updates, I've been experimenting with sometimes leaving more detailed Git commit message bodies that include LLM comments as well for providing additional context. For example, if GitHub Copilot recommends a high-priority change that I approve, I'll include those notes in the commit message body.

In this, I've admittedly been influenced by David Thompson's post "[My favourite Git commit](https://dhwthompson.com/2019/my-favourite-git-commit)." (Also, let me note Michael Lynch's "[No Longer My Favorite Git Commit](https://mtlynch.io/no-longer-my-favorite-git-commit/)" which I came across while searching for the former link.)

I'm still unsure how valuable this really is, but it doesn't take much time, and I do like the idea of that technical information and background context being available in the unlikely chance we need to investigate a commit or understand why it was made. It seems kind of wasteful to just let that context disappear into the aether if it could be useful, especially for more unique cases.

## The 50/72 Rule

During this little exercise, I learned about the "50/72 rule" for commit messages, which states:
- The initial line (the title, essentially) should be limited to 50 characters
- Subsequent lines (the body, essentially) should be limited to 72 characters

I suspect these guidelines were likely made for an earlier time and aren't quite as relevant today as they were then, but I've been adhering to them all the same (though not always the 50-character limit). It makes some sense for terminal reading and even for ease of reading on GitHub on very wide screens.

I learned how I could have Vim automatically hard-wrap lines during a `git commit` [on StackOverflow](https://stackoverflow.com/a/48754406/11767771). It just required adding this to my .vimrc file: `filetype plugin on`.

If you so and you have a relatively recent version of Vim, then when you edit commit messages, hard line breaks will be automatically inserted. (Note that I haven't look into the details yet, so there might be other unknown effects that I'm still unaware of.)

## My Vim settings

Incidentally, here's my entire .vimrc file:

```
set number
filetype plugin on
syntax on
```

The first and third lines display line numbers and add syntax highlighting, respectively.

Yeah, it's kind of sparse, but I don't use Vim all *that* much. I'm sure there are a lot more settings I should look into, though.
