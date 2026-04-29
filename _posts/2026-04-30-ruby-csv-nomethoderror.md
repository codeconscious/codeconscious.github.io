# Ruby: Resolving `NoMethodError - undefined method 'collect'` errors during CSV creation

I had the following Ruby code:

```rb
CSV.generate(force_quotes: true) do |csv|
  csv << headers
  rows.each do |row|
    csv << row
  end
end
```

Running it unexpectedly led to the following error:

> NoMethodError - undefined method 'collect' for nil:NilClass:

I had no idea why, but luckily, I came across a Japanese article that helped me resolve it: [RubyのCSV作成時に undefined method 'collect' for nil:NilClass エラーが出たときの対処](https://qiita.com/daik/items/542c63741f3a7aede208).

While two fixes are listed, the first one—changing `csv << row` to `csv << row.values`—immediately resolved the issue for me.
