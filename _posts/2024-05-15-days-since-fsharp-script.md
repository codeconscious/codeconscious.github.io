# DaysSince F# script

I've created my second F# script! (The first one was [my "enquoten" script](https://codeconscious.github.io/2024/04/02/fsharp-enquoten-script.html).) This one takes in a CSV of labelled dates and calculates (1) how many days have elapsed since and (2) the next thousand-day milestone.

It was a good chance to apply a few things I've learned thus far in this journey. Plus, maybe it's kind of interesting to enter birthdays and see how see, for example, that a friend is coming up on their 15,000th day of life. 😄

<script src="https://gist.github.com/codeconscious/15b4742a1903d89ac24eef84985488c5.js"></script>

## Example

For a file containing the following input:

```
.NET Release Dates, 8, 2023 Nov 14
.NET Release Dates, 7, 2022 Nov 8
.NET Release Dates, 6.0, 2021 Nov 8
.NET Release Dates, 5.0, 2020 Nov 10
.NET Release Dates, Core 3.1, 2019 Dec 3
.NET Release Dates, Core 3.0, 2019 Sep 23
.NET Release Dates, Core 2.2, 2018 Dec 4
.NET Release Dates, Core 2.1, 2018 May 30
.NET Release Dates, Core 2.0, 2017 Aug 14
.NET Release Dates, Core 1.1, 2016 Nov 16
.NET Release Dates, Core 1.0, 2016 Jun 27
```

The output will appear thusly:

```
.NET RELEASE DATES
------------------
Core 1.0  | 2016-06-27  | 2,880 | 3,000 in 120 days on 2024-09-12
Core 1.1  | 2016-11-16  | 2,738 | 3,000 in 262 days on 2025-02-01
Core 2.0  | 2017-08-14  | 2,467 | 3,000 in 533 days on 2025-10-30
Core 2.1  | 2018-05-30  | 2,178 | 3,000 in 822 days on 2026-08-15
Core 2.2  | 2018-12-04  | 1,990 | 2,000 in 10 days on 2024-05-25
Core 3.0  | 2019-09-23  | 1,697 | 2,000 in 303 days on 2025-03-14
Core 3.1  | 2019-12-03  | 1,626 | 2,000 in 374 days on 2025-05-24
5.0       | 2020-11-10  | 1,283 | 2,000 in 717 days on 2026-05-02
6.0       | 2021-11-08  |   920 | 1,000 in 80 days on 2024-08-03
7         | 2022-11-08  |   555 | 1,000 in 445 days on 2025-08-03
8         | 2023-11-14  |   184 | 1,000 in 816 days on 2026-08-09
```
