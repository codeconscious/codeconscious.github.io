# Leveraging Monoids For Associative Binary Operations in Haskell

In [my Haskell practice project](https://github.com/codeconscious/days-away), I had the following function:

```haskell
printSummaries :: ColumnWidths -> [RowSummary] -> IO ()
printSummaries colWidths summaries = do
    mapM_ (putStrLn . showWithColumns colWidths) $
        sortBy (comparing category) summaries
```

The sorting on the last line is the focus of this post.

I decided I wanted to try sorting by both `category` and, within each `category`, `summary` as well. However, I had trouble figuring out how to accomplish this on my own. (I was originally thinking of a nested anonymous function, which might have worked, but I didn't dig too deeply in part due to issues with the Haskell Language Server making it frustrating to test various solutions easily. That might be the topic of a future post.)

Ultimately, I decided to save time and just ask an LLM. The suggestion I got back was quite illuminating:

```haskell
printSummaries :: ColumnWidths -> [RowSummary] -> IO ()
printSummaries colWidths summaries = do
    mapM_ (putStrLn . showWithColumns colWidths) $ 
        sortBy (comparing category <> comparing summary) summaries
```

Why does the operator [`<>`](https://hackage-content.haskell.org/package/base-4.22.0.0/docs/Prelude.html#g:9) work? Because "`Ord` instances form a monoid where comparison results can be combined."

Aha, monoids are in play! Both [semigroups](https://wiki.haskell.org/Data.Semigroup) and [monoids](https://wiki.haskell.org/Monoid) allow for associative binary operations, but it didn't occur to me that sorting operations could be joined like this.

Very nice! That would have taken me quite a while to figure out on my own, and this practical example furthered my understanding of semigroups and monoids some too, thanks to the follow-up study and review I did. Reading about them is one thing, but practical experience really helps and illustrates the value of practice projects like this.
