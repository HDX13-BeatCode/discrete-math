# Simplex Method

Here are the steps:
1. Turn linear programming (LP) problem to a system of linear equations (EQs) by
   adding "slack variables".
2. Set up initial tableau.
   * ["ON"] cells are marked on the leftmost column  (col) when there is only 
     one non-zero cell there.
3. Select the pivot column.
   * Pick the column with greatest minus on p.
   * If no more minus, jump to step 7.
4. Select the pivot in the pivot col
   * Divide the rightmost col ["Ans"] with the respective entry in the pivot col.
   * Choose the smallest of them.
5. Make the values in the pivot column (except the pivot value) to 0.
   * _HINT:_ use row operations (ops): Multiply respective rows and operate them.
   * Replace the ["ON"] cell with the pivot variable.
6. Jump to step 3.
7. Done. You have reached the optimum solution.

## Example 1

Here is the [question source](https://www.zweigmedia.com/RealWorld/tutorialsf4/frames4_3.html).

> Maximize `p = x + 2y + 3z` subject to the constraints:
>
> * `7x + z <= 6`
> * `x + 2y <= 20`
> * `3y + 4z <= 30`

1. Turn linear programming (LP) problem to a system of linear equations (EQs) by
   adding "slack variables".
   * `7x + 0y + 1z + s = 6`
   * `1x + 2y + 0z + t = 20`
   * `0x + 3y + 4z + u = 30`
   * `-1x - 2y - 3z + p = 0`

2. Set up initial table.
   * ["ON"] cells are marked on the leftmost column (col) when there is only
     one non-zero cell there.
     |ON | x  | y  | z  | s  | t  | u  | p  | Ans |
     |---|---:|---:|---:|---:|---:|---:|---:|----:|
     |s  | 7  | 0  | 1  | 1  | 0  | 0  | 0  |   6 |
     |t  | 1  | 2  | 0  | 0  | 1  | 0  | 0  |  20 |
     |u  | 0  | 3  | 4  | 0  | 0  | 1  | 0  |  30 |
     |p  | -1 | -2 | -3 | 0  | 0  | 0  | 1  |   0 |

3. Select the pivot column.
   * Pick the column with greatest minus on p.
     |ON | x  | y  | **z**| s  | t  | u  | p  | Ans |
     |---|---:|---:|-----:|---:|---:|---:|---:|----:|
     |s  |  7 |  0 | **1**| 1  | 0  | 0  | 0  |   6 |
     |t  |  1 |  2 | **0**| 0  | 1  | 0  | 0  |  20 |
     |u  |  0 |  3 | **4**| 0  | 0  | 1  | 0  |  30 |
     |p  | -1 | -2 |**-3**| 0  | 0  | 0  | 1  |   0 |

4. Select the pivot cell in the pivot col
   * Divide the rightmost col ["Ans"] with the respective entry in the pivot col.
     - `6/1 = 6` (this will be used)
     - `20/0 = Infinity`
     - `30/4 = 75`
   * Choose the smallest of them.
     - `[z,s] = 1` is used

5. Make the values in the pivot column (except the pivot cell) to 0.
   * _HINT:_ use row operations (ops): Multiply respective rows and operate them.

     Before:
     |ON | x  | y  |   z  | s  | t  | u  | p  | Ans |
     |---|---:|---:|-----:|---:|---:|---:|---:|----:|
     |s  |  7 |  0 | **1**| 1  | 0  | 0  | 0  |   6 |
     |t  |  1 |  2 |   0  | 0  | 1  | 0  | 0  |  20 |
     |u  |  0 |  3 |   4  | 0  | 0  | 1  | 0  |  30 |
     |p  | -1 | -2 |  -3  | 0  | 0  | 0  | 1  |   0 |

     ```
     > row1: skip, is a pivot row (contains pivot cell)

     > row2: skip, z is already 0

     > row3: row3 - row1*4
           = { 0,  3, 4, 0, 0,  1, 0, 30}
           - {28,  0, 4, 4, 0,  0, 0, 24}
           ------------------------------
           = {-28, 3, 0, -4, 0, 1, 0, 6}

     > row4: row4 + row1*3
           = {-1, -2, -3, 0, 0, 0, 1,  0}
           + {21,  0,  3, 3, 0, 0, 0, 18}
           ------------------------------
           = {20, -2,  0, 3, 0, 0, 1, 18}
     ```
   * Replace the ["ON"] cell with the pivot variable.

     After: 
     |  ON |   x |  y |  z  |  s |  t |  u |  p | Ans |
     |-----|----:|---:|----:|---:|---:|---:|---:|----:|
     |**z**|   7 |  0 |**1**|  1 |  0 |  0 |  0 |   6 |
     |  t  |   1 |  2 |  0  |  0 |  1 |  0 |  0 |  20 |
     |  u  | -28 |  3 |  0  | -4 |  0 |  1 |  0 |   6 |
     |  p  |  20 | -2 |  0  |  3 |  0 |  0 |  1 |  18 |

6. Jump to step 3 ("Select the pivot column").

3. Select the pivot column.
   * Pick the column with greatest minus on p.
     |  ON |   x | **y**|  z  |  s |  t |  u |  p | Ans |
     |-----|----:|-----:|----:|---:|---:|---:|---:|----:|
     |  z  |   7 | **0**|  1  |  1 |  0 |  0 |  0 |   6 |
     |  t  |   1 | **2**|  0  |  0 |  1 |  0 |  0 |  20 |
     |  u  | -28 | **3**|  0  | -4 |  0 |  1 |  0 |   6 |
     |  p  |  20 |**-2**|  0  |  3 |  0 |  0 |  1 |  18 |

4. Select the pivot in the pivot col
   * Divide the rightmost col ["Ans"] with the respective entry in the pivot col.
     - `6/0 = Infinity`
     - `20/2 = 10`
     - `6/3 = 2` (use this)
   * Choose the smallest of them.

5. Make the values in the pivot column (except the pivot value) to 0.
   * _HINT:_ use row operations (ops): Multiply respective rows and operate them.

     Before:
     |  ON |   x |   y  |  z  |  s |  t |  u |  p | Ans |
     |-----|----:|-----:|----:|---:|---:|---:|---:|----:|
     |  z  |   7 |   0  |  1  |  1 |  0 |  0 |  0 |   6 |
     |  t  |   1 |   2  |  0  |  0 |  1 |  0 |  0 |  20 |
     |  u  | -28 | **3**|  0  | -4 |  0 |  1 |  0 |   6 |
     |  p  |  20 |  -2  |  0  |  3 |  0 |  0 |  1 |  18 |

     ```
     > row1: skip, y is already 0

     > row2: row2*3 - row3*2
           = {  3, 6, 0,  0, 3,  0, 0, 60}
           - {-56, 6, 0, -8, 0,  2, 0, 12}
           ------------------------------
           = { 59, 0, 0,  8, 3, -2, 0, 48}

     > row3: skip, is a pivot row (contains pivot cell)

     > row4: row4*3 + row3*2
           = { 60, -6, 0,  9, 0, 0, 3, 54}
           + {-56,  6, 0, -8, 0, 2, 0, 12}
           ------------------------------
           = {  4,  0,  0, 1, 0, 2, 3, 66}
     ```
   * Replace the ["ON"] cell with the pivot variable.

     After: 
     |  ON |   x |  y |  z  |  s |  t |  u |  p | Ans |
     |-----|----:|---:|----:|---:|---:|---:|---:|----:|
     |  z  |   7 |  0 |  1  |  1 |  0 |  0 |  0 |   6 |
     |  t  |  59 |  0 |  0  |  8 |  3 | -2 |  0 |  48 |
     |**y**| -28 |  3 |**0**| -4 |  0 |  1 |  0 |   6 |
     |  p  |   4 |  0 |  0  |  1 |  0 |  2 |  3 |  66 |

6. Jump to step 3 ("Select the pivot column").

3. Select the pivot column.
   * Pick the column with greatest minus on p.
     |  ON |   x |  y |  z  |  s |  t |  u |  p | Ans |
     |-----|----:|---:|----:|---:|---:|---:|---:|----:|
     |  z  |   7 |  0 |  1  |  1 |  0 |  0 |  0 |   6 |
     |  t  |  59 |  0 |  0  |  8 |  3 | -2 |  0 |  48 |
     |  y  | -28 |  3 |  0  | -4 |  0 |  1 |  0 |   6 |
     |  p  |   4 |  0 |  0  |  1 |  0 |  2 |  3 |  66 |
   * If no more minus, jump to step 7 ("Done. You have reached the optimum solution").

7. Done. You have reached the optimum solution.
   Which means, we can get the values for each variables.
   * `x = 0` (not ON)
   * `y = 6/3 = 2`
   * `z = 6/1 = 6`
   * `s = 0` (not ON)
   * `t = 48/3 = 16`
   * `u = 0` (not ON)
   * `p = 66/3 = 22`

   > So, `p` can me maxed with `22 = 0 + 2*2 + 3*6`.

## Example 2 (Case Study)

Translated from ["Soal No. 1" on this site](https://matematikastudycenter.com/kelas-12/72-12-sma-program-linier).

> A parking lot has an area of 1.760 m^2. An average area for a small car is
> 4 m^2 and for a big car is 20 m^2. The parking lot can only fit 200 cars.
> The parking bill is $1.00 for a small car and $2.00 for a big car. If within
> an hour, the parking lot is full and there are no incoming nor outgoing
> vehicles, then what is the maximum revenue from the parking lot that hour?

Let's say:
- `a`: small car
- `b`: big car
- `p`: price

And we have to maximize `p = 1a + 2b` with the following constraints:
- `a + b = 200` (parking lot capacity, and considering the parking lot is full)
- `4a + 20b <= 1760` (parking lot area, may be smaller than the available area)

Let's run the phases:

1. Turn them all into a system of linear EQs, and we got:
   - `a + b + s = 200`
   - `4a + 20b + t = 1760`
   - `-a - 2b + p = 0`

2. Put them in a table:
   | ON |  x |  y | s | t | p |  Ans |
   |----|---:|---:|--:|--:|--:|-----:|
   | s  |  1 |  1 | 1 | 0 | 0 |  200 |
   | t  |  4 | 20 | 0 | 1 | 0 | 1760 |
   | p  | -1 | -2 | 0 | 0 | 1 |    0 |

3. Set the pivot column to `y` because it has the greatest minus on `p`, `-2`.

4. Set the pivot cell. Let's try one at the time.
   - `s = 200/1 = 200`
   - `t = 1760/20 = 88` (use this)

5. Turn `(y,s)` and `(y,p)` into `0` using row ops.
   ```
   row_s = 20*row_s - row_t
         = {20, 20, 20,  0, 0, 4000}
         - { 4, 20,  0,  2, 0, 1760}
         --------------------------
         = {16,  0, 20, -2, 0, 2240}

   row_p = 10*row_p + row_t
         = {-10, -20, 0, 0, 10,    0}
         + {  4,  20, 0, 1,  0, 1760}
         ----------------------------
         = { -6,   0, 0, 1, 10, 1760}
   ```

   And the table becomes:
   | ON |  x |  y |  s |  t |  p |  Ans |
   |----|---:|---:|---:|---:|---:|-----:|
   | s  | 16 |  0 | 20 | -2 |  0 | 2240 |
   | y  |  4 | 20 |  0 |  1 |  0 | 1760 |
   | p  | -6 |  0 |  0 |  1 | 10 | 1760 |

6. We still have one more minus (`-6` on col `x`), so that's our pivot column.

7. Set the pivot cell like before. We get:
   - `s = 2240/16 = 140` (use this)
   - `y = 1760/4 = 440`

8. Turn `(x,y)` and `(x,p)` into `0` using row ops.
   ```
   row_y = 4*row_y - row_s
         = {16, 80,   0,  4, 0, 7040}
         - {16,  0,  20, -2, 0, 2240}
         ----------------------------
         = { 0, 80, -20,  6, 0, 4800}

   row_p = 8*row_p + 3*row_s
         = {-48, 0,  0,  8, 80, 14080}
         + { 48, 0, 60, -6,  0,  6720}
         -----------------------------
         = {  0, 0, 60,  2, 80, 20800}
   ```

   And here's the optimum table:
   | ON |  x |  y |   s |  t |  p |   Ans |
   |----|---:|---:|----:|---:|---:|------:|
   | x  | 16 |  0 |  20 | -2 |  0 |  2240 |
   | y  |  0 | 80 | -20 |  6 |  0 |  4800 |
   | p  |  0 |  0 |  60 |  2 | 80 | 20800 |

9. Finally, find `p` for our revenue:
   `p = 20800/80 = 260`

So, the maximum revenue from the parking lot is $260.
