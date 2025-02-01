# Unicode Normalization Forms and Recursive Path Normalizer (F# Script)

I wrote previously about how, when attempting to copy a large batch of files from my Linux laptop to my M1 MacBook Pro, many files with Japanese filenames failed to copy until I renamed them. As a temporary workaround (and as a programming exercise), I created scripts in both [Ruby](https://codeconscious.github.io/2024/09/05/recursive-random-renaming.html) and [F#](https://codeconscious.github.io/2024/09/11/recursive-random-renaming-redux.html) to randomize their names (since the names were not particularly significant).

I recently returned to this issue and discovered that the underlying issue was as I'd expected: Unicode normalization issues between OSes.

For example, take the following Japanese characters: `ボ` and `ボ`, both of which represent the sound "bo" in Japanese using its katakana script. They appear identical, but their compositions are actually completely different:
- The former is a single "composed" code point, [0x30dc](https://www.compart.com/en/unicode/U+30DC), which represents the entire character as seen and is an example of NFC (Normalization Form Canonical Composition)
- The latter is a combination of the "decomposed" code points `ホ` ([0x30db](https://www.compart.com/en/unicode/U+30db)) and `◌゙` ([0x3099](https://www.compart.com/en/unicode/U+3099)) and is an example of NFD (Normalization Form Canonical Decomposition)

For greatest compatibility between Linux and macOS, it seems the NFC form is best.

I've created a new F# script, [**Recursive Path Normalizer**](https://github.com/codeconscious/scripts/blob/main/fsharp/RecursivePathNormalizer.fsx), that recursively normalizes all directory and file names to NFC form within a given path. Of course, there are other ways to do this, such as [convmv](https://www.j3e.de/linux/convmv/man/)¹, but it was a good chance to work with F# again and craft my own solution. (I adapted a chunk of code from my previous random-name script, which gave me a quick start. I also incorporated [Startwatch](https://codeconscious.github.io/2024/01/08/first-nuget-package.html) as a timer.)

I'm still keeping an eye on things, but this seems to have resolved my copying problem. ✌️

---

¹ Conversion to NFC can be done thusly: `convmv -r -f utf8 -t utf8 --nfc --notest .`.

---

References and other helpful links:
- Unicode.org: [Unicode Normalization Forms](https://unicode.org/reports/tr15/)
- Wikipedia: [Unicode equivalence](https://en.wikipedia.org/wiki/Unicode_equivalence) ([日本語](https://ja.wikipedia.org/wiki/Unicode%E3%81%AE%E7%AD%89%E4%BE%A1%E6%80%A7))
- Nicolas Bouliane: [File names, unicode normalization problems, and how to fix them](https://nicolasbouliane.com/blog/unicode-normalization)
- HackTricks: [Unicode Normalization](https://book.hacktricks.wiki/en/pentesting-web/unicode-injection/unicode-normalization.html)
- monokano: [Unicodeの特殊な文字 “結合文字列”](https://tama-san.com/combining_character_sequence/)
- Jugesuke: [あなたの知らない UTF-8 の世界](https://zenn.dev/jugesuke/articles/e3b92518e21698)
- [Character Code Finder](https://www.mauvecloud.net/charsets/CharCodeFinder.html)
