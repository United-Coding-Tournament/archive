# Contest 1 Round 2 

---

## Problem 1: Adventures of a Knight

**Problem Statement**

A knight starts on a square on a $n$x$n$ chess board, numbered from 0 to $n - 1$, given as a 2d array. A knight starts on the position ($x$, $y$). A knight moves in the shape of an L, i.e. 2 moves up, 1 move right; 2 moves down, 1 move left; etc. Which squares can the knight reach in at most $m$ moves?

Print out each square of the chess board left to right, top to bottom, in a single line, 1 being the square the knight can move to, 0 being a square the knight can never reach.

**Input Specifications**

The first line has one integer, $n = 64$, the dimensions of the board.

The next line has two space separated integers, $x = y = 31$, the starting position of the knight on the chessboard.

The final line has one integer, $m = 12$, the maximum number of moves the knight may make.

**Output Specifications**

Output a string of 0s and 1s, whether a square on the chess board is occupied by a knight or not, from left to right, top to bottom.

**Example:** If the chess board is 4x4, the knight starts at (3,3) and can move 1 move at most, then the chess board would look like this:

$$\text{0 1 0 1}$$
$$\text{1 0 0 0}$$
$$\text{0 0 1 0}$$
$$\text{1 0 0 0}$$

And you would print out each element in each row from left to right for each row from top to bottom, that is, `0101100000101000`.

<details>
<summary>Click here to view the input.</summary>
<br>

```
64
31 31
12
```
</details>

<br>

<details>
<summary>Click here to view the correct answer.</summary>
<br>

```
0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000010101010101010101010101010000000000000000000000000000000000000010101010101010101010101010100000000000000000000000000000000000010111111111111111111111111101000000000000000000000000000000000010111111111111111111111111111010000000000000000000000000000000010111111111111111111111111111110100000000000000000000000000000010111111111111111111111111111111101000000000000000000000000000010111111111111111111111111111111111010000000000000000000000000010111111111111111111111111111111111110100000000000000000000000010111111111111111111111111111111111111101000000000000000000000010111111111111111111111111111111111111111010000000000000000000010111111111111111111111111111111111111111110100000000000000000010111111111111111111111111111111111111111111101000000000000000010111111111111111111111111111111111111111111111010000000000000000111111111111111111111111111111111111111111111110000000000000000101111111111111111111111111111111111111111111110100000000000000001111111111111111111111111111111111111111111111100000000000000001011111111111111111111111111111111111111111111101000000000000000011111111111111111111111111111111111111111111111000000000000000010111111111111111111111111111111111111111111111010000000000000000111111111111111111111111111111111111111111111110000000000000000101111111111111111111111111111111111111111111110100000000000000001111111111111111111111111111111111111111111111100000000000000001011111111111111111111111111111111111111111111101000000000000000011111111111111111111111111111111111111111111111000000000000000010111111111111111111111111111111111111111111111010000000000000000111111111111111111111111111111111111111111111110000000000000000101111111111111111111111111111111111111111111110100000000000000001111111111111111111111111111111111111111111111100000000000000001011111111111111111111111111111111111111111111101000000000000000011111111111111111111111111111111111111111111111000000000000000010111111111111111111111111111111111111111111111010000000000000000111111111111111111111111111111111111111111111110000000000000000101111111111111111111111111111111111111111111110100000000000000001111111111111111111111111111111111111111111111100000000000000001011111111111111111111111111111111111111111111101000000000000000011111111111111111111111111111111111111111111111000000000000000010111111111111111111111111111111111111111111111010000000000000000101111111111111111111111111111111111111111111010000000000000000001011111111111111111111111111111111111111111010000000000000000000010111111111111111111111111111111111111111010000000000000000000000101111111111111111111111111111111111111010000000000000000000000001011111111111111111111111111111111111010000000000000000000000000010111111111111111111111111111111111010000000000000000000000000000101111111111111111111111111111111010000000000000000000000000000001011111111111111111111111111111010000000000000000000000000000000010111111111111111111111111111010000000000000000000000000000000000101111111111111111111111111010000000000000000000000000000000000001010101010101010101010101010000000000000000000000000000000000000010101010101010101010101010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
```

</details>
<br>

<details>
<summary>Click here to view the C++ solution.</summary>
<br>

```cpp
// Recursively calculate the knight's moves from last jump

#include <bits/stdc++.h>

using namespace std;

int main() {
    int dimensions;
    int x,y;
    int move;

    ifstream infile;
    infile.open("input.txt");

    infile >> dimensions >> x >> y >> move;

    infile.close();

    vector<vector<int>> board(dimensions, vector<int> (dimensions, 0));

    board[x][y] = 1;

    // Storing all possible ways the knight can move
    vector<vector<int>> moves {{2, 1}, {2, -1}, {-2, 1}, {-2, -1}, {1, 2}, {1, -2}, {-1, 2}, {-1, -2}};

    int cnt = 0;

    // Repeat for the number of moves required
    for (int i = 0; i < move; ++i) {
        for (int j = 0; j < dimensions; ++j) {
            for (int k = 0; k < dimensions; ++k) {
                // Mark the squares the knight can move as 2 
                // That way we don't move on a square that just got marked
                if (board[j][k] == 1) {
                    for (auto c : moves) {
                        if (0 <= j + c[0] && j + c[0] < dimensions && 0 <= k + c[1] && k + c[1] < dimensions) {
                            board[j + c[0]][k + c[1]] = 2;
                        }
                    }
                }
            }
        }
        // We then set all the new squares back to 1
        for (int j = 0; j < dimensions; ++j) {
            for (int k = 0; k < dimensions; ++ k) {
                if (board[j][k] == 2) {
                    board[j][k] = 1;
                }
            }
        }
    }

    for (int i = 0; i < dimensions; ++i) {
        for (int j = 0; j < dimensions; ++ j) {
            cout << board[i][j];
        }
    }
}
```

</details>

--- 

## Problem 2: A Way Home

**Problem Statement**

Alice wishes to return home. She starts at the top left square and must travel to the bottom right square on a $m$ by $n$ grid. She is tired, so she will take the shortest path possible. However, there are some blocks she cannot pass through. How many ways can she reach her home?

**Input Specifications**

The first line has two space separated integers, the number of rows,$m = 70$, and the number of columns, $n = 45$.

The next $m$ lines have $n$ space separated integers each, either 0 or -1.

**Output Specifications**

Output a single integer, the number of ways Alice can reach home modulo 1000000. Note that the number of ways may exceed $2^{31} - 1$.

<details>
<summary>Click here to view the input.</summary>
<br>

```
70 45
0 0 0 0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
-1 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 0 -1 -1 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 0 0 -1 -1 0 0 0 
0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 -1 0 0 -1 0 0 0 -1 0 -1 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 0 
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 -1 -1 0 0 0 0 0 -1 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 
0 0 -1 0 0 -1 0 0 0 0 -1 0 0 -1 0 -1 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 -1 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 -1 
-1 -1 0 0 -1 0 0 0 0 0 0 -1 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 
-1 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 0 -1 0 0 
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 -1 0 0 -1 0 0 -1 0 0 0 0 0 0 0 -1 -1 0 0 0 
0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 -1 0 0 0 
0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 -1 0 0 -1 -1 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 
0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 -1 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 -1 0 -1 0 -1 0 0 0 0 
0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 -1 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 -1 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 -1 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 -1 0 0 0 0 -1 -1 0 0 0 -1 0 0 0 0 -1 -1 -1 
0 0 0 0 0 0 0 0 0 -1 0 -1 0 0 0 -1 0 -1 0 0 0 -1 0 0 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 -1 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 -1 0 -1 0 0 0 0 0 0 
-1 0 0 -1 0 0 0 -1 0 0 0 0 -1 0 -1 0 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 -1 0 0 0 0 0 -1 0 0 0 0 0 0 0 
0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 -1 0 0 -1 0 -1 
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 0 
-1 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 -1 0 0 0 0 -1 0 0 0 0 0 0 
0 0 0 0 0 0 -1 0 -1 0 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 
0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 -1 0 0 -1 0 0 0 0 -1 -1 0 -1 
0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 -1 
0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 
0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 
-1 0 0 0 -1 -1 0 0 0 -1 0 -1 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 0 -1 0 0 0 -1 0 -1 0 
0 0 -1 0 0 0 0 0 0 0 -1 0 -1 -1 0 -1 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 -1 -1 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 -1 0 0 0 
0 -1 0 0 -1 0 0 -1 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 -1 0 0 -1 0 0 -1 0 0 0 0 0 0 -1 0 0 0 0 
0 0 -1 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 
0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 -1 -1 0 0 0 0 0 0 0 -1 0 -1 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 -1 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 -1 0 -1 0 0 0 0 0 0 
-1 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 -1 0 0 0 -1 -1 0 0 0 0 0 0 0 0 -1 0 0 -1 0 0 0 0 
0 0 0 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 
-1 0 0 -1 0 0 0 0 0 -1 -1 -1 0 0 -1 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 -1 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 
-1 0 0 0 0 0 -1 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 -1 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 
0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 -1 -1 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 -1 0 0 0 0 0 0 0 -1 
0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 
-1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 -1 
0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 
0 -1 0 0 -1 0 0 0 0 0 -1 0 -1 0 0 0 0 0 -1 -1 -1 0 0 0 0 -1 -1 -1 0 0 0 0 0 0 0 0 0 -1 -1 -1 0 0 0 0 0 
0 0 0 -1 0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 0 0 -1 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 -1 0 -1 -1 -1 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 -1 0 -1 0 0 -1 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 -1 0 0 
0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 
0 -1 0 0 0 0 0 0 0 0 -1 0 0 -1 0 -1 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 
0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 -1 0 0 -1 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 
-1 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
-1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 -1 0 0 0 0 
0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 
0 0 0 0 0 -1 0 -1 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 -1 0 0 0 -1 0 -1 0 0 0 -1 0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 
0 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 
0 0 0 0 0 -1 0 0 0 -1 0 0 0 0 0 0 -1 0 0 0 -1 -1 0 0 0 -1 0 0 0 0 0 -1 0 0 0 0 0 0 0 -1 0 0 0 -1 0 
-1 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 0 -1 -1 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 
0 0 0 0 -1 0 0 -1 0 0 0 -1 0 0 0 0 0 -1 0 0 0 0 0 0 0 0 0 0 0 -1 0 0 0 0 0 0 -1 -1 0 0 0 0 0 -1 0 
```
</details>

<br>

<details>
<summary>Click here to view the correct answer.</summary>
<br>

```
205646
```

</details>
<br>

<details>
<summary>Click here to view the C++ solution.</summary>
<br>

```cpp
// Assume the optimized path only requires downwards and rightwards movement and use Pascal's Triangle.

#include <bits/stdc++.h>

using namespace std;

int main() {
    int m,n;

    ifstream infile;
    infile.open("input.txt");

    infile >> m >> n;

    vector<vector<long long int>> land;

    for (int i = 0; i < m; ++i) {
        vector<long long int> temp_v;
        for (int j = 0; j < n; ++j) {
            long long int temp;
            infile >> temp;
            temp_v.push_back(temp);
        }
        land.push_back(temp_v);
    }

    infile.close();

    land[0][0] = 1;

    // We use Pascal's Triangle to solve
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            // We don't perform calculations on blocks
            if (land[i][j] == -1) continue;
            // Each time we add the square directly above and to the left unless there is a block; then we only add from the square without a block
            // We also make sure the indices are within bounds
            if (i - 1 >= 0 && j - 1 >= 0) {
                if (land[i - 1][j] != -1 && land[i][j - 1] != -1) {
                    land[i][j] = (land[i - 1][j] + land[i][j - 1]) % 1000000;
                }
                else if (land[i - 1][j] != -1) {
                    land[i][j] = land[i - 1][j];
                }
                else if (land[i][j - 1] != -1) {
                    land[i][j] = land[i][j - 1];
                }
            }
            // Here we are performing calculations for the first row and first column
            else if (i - 1 >= 0) {
                if (land[i - 1][j] != -1) land[i][j] = land[i - 1][j];
            }
            else if (j - 1 >= 0) {
                if (land[i][j - 1] != -1) land[i][j] = land[i][j - 1];
            }
        }
    }
    // We are lucky here since going only down and right has valid paths
    // If the answer was 0, that means the optimized path potentially requires you to go up or left, or there is no path
    cout << land[m - 1][n - 1] << endl;
} 
```

</details>

--- 

## Problem 3: Joe on the Transpo

**Problem Statement**

Joe is going to Merivale High School on the OC Transpo. In the city that Joe lives in, there are 100 bus stops, numbered from 1 to 100, and 300 bidirectional roads with length of 1 unit, where a road connects bus stop `x` to bus stop `y`. Joe knows that his bus needs to stop at bus stop 50. Given the locations of the roads,it is your job to help Joe find the shortest path from bus stop 1 to bus stop 100, such that this path passes through bus stop 50. 

<details>
<summary>Click here to view the input.</summary>
<br>

```
1 42
42 68
68 35
35 70
70 25
25 79
79 59
59 63
63 65
65 6
6 46
46 82
82 28
28 62
62 92
92 96
96 43
43 37
37 5
5 3
3 54
54 93
93 83
83 22
22 17
17 19
19 48
48 27
27 72
72 39
39 13
13 100
100 36
36 95
95 4
4 12
12 23
23 34
34 74
74 69
69 45
45 58
58 38
38 60
60 24
24 30
30 91
91 89
89 7
7 41
41 49
49 47
47 71
71 51
51 2
2 94
94 85
85 55
55 57
57 67
67 77
77 32
32 9
9 40
40 16
16 31
31 78
78 87
87 73
73 98
98 56
56 75
75 53
53 8
8 88
88 84
84 10
10 14
14 11
11 21
21 97
97 29
29 18
18 15
15 52
52 50
50 20
20 99
99 90
90 86
86 44
44 81
81 80
80 76
76 33
33 26
26 61
61 64
64 66
78 88
26 75
30 28
24 29
3 21
24 63
38 97
96 62
65 26
3 61
31 17
12 27
12 72
54 48
91 21
89 25
41 64
63 52
1 30
59 14
66 79
78 8
59 1
4 40
58 61
78 25
14 9
2 88
61 51
94 29
6 85
12 41
36 5
73 57
24 51
57 86
27 17
27 58
70 72
97 62
18 23
18 13
86 97
24 42
60 66
97 33
54 56
85 63
55 35
58 73
33 70
8 64
12 84
68 36
76 49
24 39
55 43
42 12
60 76
22 26
27 71
6 35
51 84
80 99
38 35
57 35
77 94
63 6
82 49
14 1
56 42
43 56
12 63
53 79
97 44
41 74
76 14
19 73
18 11
13 33
70 96
41 32
86 89
98 91
91 90
54 46
45 41
36 59
93 60
4 82
76 30
93 9
50 98
62 57
68 28
30 42
14 41
2 75
16 78
14 84
25 93
93 2
71 60
28 29
76 85
99 87
88 71
5 48
22 4
7 64
11 64
90 72
65 41
20 43
92 14
19 5
51 33
76 6
99 23
85 48
72 49
14 65
46 76
47 13
70 79
20 63
66 45
46 41
19 9
2 71
33 24
53 73
2 64
24 4
1 28
16 70
29 66
48 44
44 89
10 38
50 64
89 82
9 43
22 61
55 59
47 89
50 91
31 44
49 21
37 68
36 84
86 27
54 39
25 30
24 49
58 60
45 67
19 56
56 26
50 2
85 97
65 16
76 43
43 14
49 97
27 73
74 7
5 30
27 6
76 13
66 94
15 42
57 95
37 53
83 39
16 56
31 32
26 42
38 12
91 87
63 51
94 35
17 54
9 53
34 63
4 55
4 35
49 57
18 25
1 29
19 81
51 59
62 56
4 65
44 77
3 10
90 62
83 49
75 54
32 24
9 60
```
</details>

<br>

<details>
<summary>Click here to view the correct answer.</summary>
<br>

```
8
```

</details>
<br>

<details>
<summary>Click here to view the C++ solution.</summary>
<br>

```cpp
#include<bits/stdc++.h>
using namespace std;

//create distance and visited arrays (keeps track of distance to bus stop and if bus stop has been visited respectively)
int dist[200];
bool visited[200];
//queue for BFS
queue<int> q;
//adjacency list
vector<int> adj[302];

int bfs(int s, int e){
    //set distance to large value, visited to 0
    for(int i = 1; i <= 150; ++i){
        dist[i] = 10000;
        visited[i] = 0;
    }
    q.push(s);
    visited[s] = 1;
    dist[s] = 0;
    while(!q.empty()){
        int t = q.front(); q.pop();
        for(auto a: adj[t]){
            if(visited[a]) continue;
            visited[a] = 1;
            //update distance
            dist[a] = dist[t]+1;
            q.push(a);
        }
    }
    return dist[e];
}

int main(){
    freopen("transpo.in", "r", stdin);
    freopen("transpo.out", "w", stdout);
    for(int i = 0; i < 300; ++i){
        int a, b;
        cin >> a >> b;
        //create adjacency list
        adj[a].push_back(b);
        adj[b].push_back(a);
    }
    //output sum of two bfs
    cout << bfs(1, 50)+bfs(50, 100);

}
```

</details>

--- 