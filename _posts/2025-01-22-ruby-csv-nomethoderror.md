# Resolving `NoMethodError - undefined method 'collect'` errors during Ruby CSV creation

I ran into 

```rb
CSV.generate(force_quotes: true) do |csv|
  csv << headers
  rows.each do |row|
    csv << row
  end
end
```

This unexpectedly led to the following error upon running it: "NoMethodError - undefined method 'collect' for nil:NilClass:", and I had no idea why.

Luckily, I came across a Japanese article that helped me resolve it: [RubyのCSV作成時に undefined method 'collect' for nil:NilClass エラーが出たときの対処](https://qiita.com/daik/items/542c63741f3a7aede208).

Two fixes are listed, but I used the first, which was to change `csv << row` to `csv << row.values`. This immediately fixed my issue.
