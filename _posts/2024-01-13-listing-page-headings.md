# Bookmarklet to list page headings

When I find particularly notable articles online, I like to log them in my personal note collection, which I organize with [Obsidian](https://obsidian.md/).

To help with this, I recently wrote the following JavaScript bookmarklet to list up the text of pages' headings (indicated via HTML tags like `H1` and `H2`) in Firefox (and, hopefully, other browsers too):

<script src="https://gist.github.com/codeconscious/0d7ac8ca0b1ee09c6ac81690897a683b.js"></script>

This bookmarklet appends a Markdown-friendly bulleted list to the page, indenting more for each subheading level and also stripping out terminating colons (which, admittedly, are rare).

Here's example output using [the article for which I decided to write this bookmarklet](https://www.indiehackers.com/post/aim-fire-scan-the-80-20-of-executing-on-big-projects-571580cd0a):

> - Aim, fire, scan: the 80/20 of executing on big projects
>   - The Contract
>   - Plan, Do, Learn
>   - AIM: The 80/20 of Good Planning
>     - 1. ABZs
>     - 2. Interrogate
>     - 3. Mandatory
>   - FIRE: The 80/20 of Good Doing
>     - 1. Frontload
>     - 2. Improvise
>     - 3. Resourcefulness
>     - 4. Exhaust
>   - SCAN: The 80/20 of Good Learning
>     - 1. Score
>     - 2. Critique
>     - 3. Adjust
>     - 4. Notes

(The repeating ones are due to a GitHub Markdown rendering issue. The numbering is correct in the actual text.)

I think reviewing heading summaries like this might be beneficial for both remembering and recalling articles' contents.

## 日本語の要約

上記のJavaScript bookmarkletをブラウザーで実行することによって、ページに載っているヘッダータッグの文字列を自動的にMarkdown記法でリストアップできます。メモっておきたい時には役に立つかもしれないと思います。
