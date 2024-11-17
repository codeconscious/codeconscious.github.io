# Ruby on Rails: `simple_format()`

Last week, when working out how to render the line breaks from certain input into HTML emails, I stumbled upon [the `simple_format` method](https://apidock.com/rails/ActionView/Helpers/TextHelper/simple_format) in [the `ActionView::Helpers::TextHelper` class](https://apidock.com/rails/ActionView/Helpers/TextHelper). Per its own description, it "[r]eturns text transformed into HTML using simple formatting rules," and it optionally sanitizes the input as well. Using it solved the problem for me.

One caveat: The text will be surrounded with an HTML tag pair, and there is no way to opt out. You can specify custom tags if you wish; otherwise, `<p>` will be used by default. Where I was inserting the method, I needed to avoid a block-level element, so I ended up using `<span>` tags, which felt like a decent way to skirt the issue.

Since a worker mentioned that he was unfamiliar with this method, I thought it might be worth mentioning here.
