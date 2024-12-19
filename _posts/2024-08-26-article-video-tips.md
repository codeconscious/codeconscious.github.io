# Tips for Articles and Videos

I'd like to share some advice for creating programming-related articles and videos. These are minor issues I've noticed several times over the years, and I think eliminating them leads to clearer teaching material.

1. **Avoid meaningless names in code snippets.** I'm thinking specifically of terms like `foo` and `IBar` and `thing`. These should be avoided for all but, perhaps, the simplest and shortest of code examples. I personally find that their use just interferes with grokking the material a bit. Prefer concrete terms instead — e.g., `IVehicle`, `Car`, and `Bus`.

1. **Specify the language of code snippets.** Presuming that the article or video in question is not dedicated to a specific language, it's best not to assume that readers can instantly identity the language in your code snippets. Also, multiple programming languages might look very similar for some shorter snippets. It's best to provide your readers with that clarity upfront.

1. **Repeat code snippets as reminders.** I sometimes read articles that show a code snippet, explain something (e.g., a new language feature), and then show an updated version of the snippet. However, the reader might already have forgotten some details of the original version or might want to do an A-B comparison, leading to inconvenient scrolling back and forth. Consider repeating your original snippet immediately above the updated version as a quick and convenient reminder.

1. **Check code snippet width**. I've encountered several sites in which code snippets' widths exceeded the width of their article containers, meaning users must scroll horizontally for each such snippet. Avoid this by reviewing the actual published article, including at lower resolutions, and updating the snippets if necessary. Check on desktop and mobile devices as possible. (If you ever redesign your site, I'd recommended verifying that your updated design has not introduced this issue.)

1. **Highlight relevant text in larger snippets.** Providing code snippets that are longer than strictly necessary can be useful for showing readers the surrounding context of relevant lines. However, it can easily lead to confusion about what is and isn't directly relevant to your point. Consider adding text comments or formatting to make the most relevant text and lines stand out.

(Note: I might add items to this list occasionally.)
