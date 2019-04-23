# Transportation Problem

Taken from this video.

> A company has two production centers (PC) in USA, Boston and Toronto.
> Boston PC is able produce 300 items a day, while Toronto PC can make 500.
> All of the produced items will be shipped to 3 distribution centers (DC),
> where it demands 200, 300, and 250 items respectively.
>
> The following is the table of product shipping costs from PC to DC.
>
> | PC\\DC  | 1 | 2 | 3 |
> |---------|---|---|---|
> | Boston  | 5 | 6 | 4 |
> | Toronto | 6 | 3 | 7 |
>
> Please help the company to minimize their expenses considering that
> the production cost in Boston is $20 and Toronto is $18.

That table above can be expanded to fit all the descriptions above.

| PC (cost) \\ DC  | 1   | 2   | 3   | Supply |
|------------------|----:|----:|----:|-------:|
| Boston ($20)     |   5 |   6 |   4 |    300 |
| Toronto ($18)    |   6 |   3 |   7 |    500 |
| Demand           | 200 | 300 | 250 |        |

Let's set our variables first.
  - `PCB` and `PCT` are production centers in Boston and Toronto respectively.
  - `DC1`, `DC2`, and `DC3` are the respective distribution centers.
  - For `i` in (`B` for Boston and `T` for Toronto) and `j` in (`1`, `2`, `3`
    for each DC), `ij` is a variable of items shipped from `i` to `j`.
    Example, `T2` is a variable that tells the number of items shipped from
    Toronto to DC2.

Just like in [Example 3](#example-3-minimization), we will transpose the table
tutn our minimization into maximization. And here is the transposed table:

Before:

| P\\D | 1   | 2   | 3   | Sup |
|------|----:|----:|----:|----:|
| B    |   5 |   6 |   4 | 300 |
| T    |   6 |   3 |   7 | 500 |
| Dmd  | 200 | 300 | 250 |     |

After

| P\\D  |   B |   T | Dmd |
|-------|----:|----:|----:|
| 1     |   5 |   6 |  20 |
| 2     |   6 |   3 | 300 |
| 3     |   4 |   7 | 250 |
| Sup   | 300 | 500 |     |
