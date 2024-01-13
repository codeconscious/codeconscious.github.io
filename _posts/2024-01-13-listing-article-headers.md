# Listing article headers

Tags: javascript, english

When I find particularly notable articles online, I like to log them in my personal notes, which I organize with [Obsidian](https://obsidian.md/).

Recently, I wrote the following Javascript to list up the headings of articles:

```javascript
Array.from(document.querySelectorAll("h1, h2, h3, h4")).map(e => `${" ".repeat((parseInt(e.tagName[1])-1)*2)}- ${e.outerText.replace(/\:$/, '')}` ).join("\n")
```

This one-liner lists the headings on a page as a bulleted list in Markdown format, indenting more for each subheading and stripping out terminating colons (which, admittedly, are rare).

Here's example output using [the article for which I decided to write this script](https://www.indiehackers.com/post/aim-fire-scan-the-80-20-of-executing-on-big-projects-571580cd0a):

- Aim, fire, scan: the 80/20 of executing on big projects
  - The Contract
  - Plan, Do, Learn
  - AIM: The 80/20 of Good Planning
    - 1. ABZs
    - 2. Interrogate
    - 3. Mandatory
  - FIRE: The 80/20 of Good Doing
    - 1. Frontload
    - 2. Improvise
    - 3. Resourcefulness
    - 4. Exhaust
  - SCAN: The 80/20 of Good Learning
    - 1. Score
    - 2. Critique
    - 3. Adjust
    - 4. Notes

I think reviewing lists like this might be beneficial for remembering articles' contents and recalling them later.