# FP in Ruby: Composition

One of my goals for 2026 is to have more fun working with Ruby on Rails, and leveraging what I'm learning about functional programming (FP) in Ruby seems like a good way to start.

On that note, I unexpectedly learned something pleasantly surprising last week: Ruby supports method and Proc composition via `<<` and `>>`!

Here's an example using lambdas:

```rb
strip_whitespace = ->(s) { s.gsub(/\s/, '') }
strip_punctuation = ->(s) { s.gsub(/[[:punct:]]/, '') }
to_lower = ->(s) { s.downcase }

strip = strip_whitespace >> strip_punctuation >> to_lower

strip.("  Hello, world!   ")
=> "helloworld"
```

(In the last command, `.()` is syntactic sugar for `.call()`. The latter is likely more idiomatic, but I'm recently rather fond of the former shorter version. It almost feels like a custom operator, à la F#.)

This works with methods too, though things get clunkier due to need to call `method`:


```rb
# These are methods using the newer "end-less" syntax.
def strip_whitespace(s) = s.gsub(/\s/, '')
def strip_punctuation(s) = s.gsub(/[[:punct:]]/, '')
def to_lower(s) = s.downcase

strip = method(:strip_whitespace) >>
          method(:strip_punctuation) >>
          method(:to_lower)

strip.("  Hello, world!   ")
=> "helloworld"
```

Quite neat. I'll keep an eye out for places where composition like this might be helpful.
