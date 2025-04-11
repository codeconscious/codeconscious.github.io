# Currying in Ruby

In looking a bit into functional programming in Ruby, I was surprised to learn recently that Ruby has native support for currying.

Here are some examples:

## Option 1: `.curry`

```rb
# Via methods
def add(x, y); x + y; end
add_fifty = method(:add).curry.(50)
add_fifty.(7) # 57
```

```rb
# Via lambdas
list = (1..10)
greater_than = -> (x, y) { y > x }.curry
list.select(&greater_than.(5)) # [6, 7, 8, 9, 10]
list.select(&greater_than.(8)) # [9, 10]

has_a = -> (find, source) { source.include? find }.curry.('a')
has_a.("hello world") # false
has_a.("Is that so?") # true

text_has = -> (source, find) { source.include? find }.curry.('hello world')
text_has.('a') # false
text_has.('e') # true
```

## Option 2: `lambda` in methods

```rb
def multiply(m); lambda { |n| n * m }; end

double = multiply(2)
triple = multiply(3)

double[5] # 10
triple.(5) # 15
```
