# Handling Unsupported Kanji in Shift-JIS (※日本語要約付き）

I ran into a somewhat interesting character encoding–related conundrum at work recently.

Our system generates certain CSVs that are, for business reasons, in the Shift-JIS character encoding. This has been fine until now, but recently an internal user reported failures in that flow.

Upon looking into it, I discovered that the culprit was the Japanese kanji `﨑`. `﨑` is a variant of `崎` (which is very similar, but differs at the upper-right) and is an irregular character not supported in pure Shift-JIS. That incompatibility was causing the CSV generation to raise an exception.

One easy option was to replace the unsupported variant kanji (`﨑`) in the source data with the supported one (`崎`), but that idea was rejected by the reporter.

Ultimately, the reporter agreed that the column containing that character was not actually necessary for this CSV, so we did an emergency update and release to stop the inclusion of that column so we could unblock their work.

Another option: I believe the Ruby gem we use can also replace unsupported characters with a specified alternate at generation time, thus at least allowing CSV generation to complete.

I think these sorts of issues are interesting, but I do rather wish we weren't using Shift-JIS in the first place. But, as they say, them's the breaks.

---

## 日本語の要約

会社のアプリのバックエンドにてShift-JISのCSVを作成する際、Shift-JIS未対応の「[﨑](https://ja.wiktionary.org/wiki/%EF%A8%91)」という文字がコンテンスに新しく含まれたせいで作成が失敗していたことが発覚されました。調べたことによれば「﨑」はShift-JIS対応の「[崎](https://ja.wiktionary.org/wiki/%E5%B4%8E)」の俗字だとのこと。（さらにお読みになりたい方は[「意味解説辞典」の記事](https://meaning-dictionary.com/%E3%80%8C%E5%B4%8E%E3%80%8D%E3%81%A8%E3%80%8C%EF%A8%91%E3%80%8D%E3%81%AE%E9%81%95%E3%81%84%E3%81%A8%E3%81%AF%EF%BC%9F%E5%88%86%E3%81%8B%E3%82%8A%E3%82%84%E3%81%99%E3%81%8F%E8%A7%A3%E9%87%88/)をおすすめします。）

その時は時間に迫られていたので、CSV作成に関連するコードで該当する列をまるごと割愛して直せたのですが、対応方法はそれのみならず、そのような未対応の文字によってエクセプションが起きないよう作成設定のほうで替え玉の文字の設定も可能みたいです。

改めてUTF-8のありがたさを感じさせる事件となりました。
