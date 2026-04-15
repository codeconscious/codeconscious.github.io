A bit over a year ago, [I posted about Unicode normalization forms](https://codeconscious.github.io/2025/02/01/recursive-path-normalizer.html), mainly in a .NET context.

Today, I happened to learn how this is done in Ruby from a coworker's pull request.

```ruby
"ボ".unicode_normalize(:nfkc) == "ボ".unicode_normalize(:nfkd)
=> false
```

Documentation: [https://apidock.com/ruby/v2_5_5/String/unicode_normalize](https://apidock.com/ruby/v2_5_5/String/unicode_normalize)
