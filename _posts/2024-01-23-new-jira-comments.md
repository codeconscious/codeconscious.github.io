# Bookmarklet to move new-comment Jira controls higher

At work, Jira insists on sorting comments with the newest ones at the top. However, the "Add a comment" button is located underneath all the comments. So, often, I'll read the topmost comment and then have to scroll to the bottom of the page to add a new comment.

It's a very minor but persistent UX bummer, so today I decided to do something about it: I created a bookmarklet that, when activated, moves the new-comment button and the subsequent new-comment textbox and controls to immediately above the comments area.

<script src="https://gist.github.com/codeconscious/7fd3a8bed27d83c687578b1ee9c42dc8.js"></script>

Just a simple fix for a small daily annoyance.

_Update:_ I learned the following day that I can immediately jump to new comment entry with the `m` key. Nice to know!
