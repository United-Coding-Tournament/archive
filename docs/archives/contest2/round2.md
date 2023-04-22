# Contest 2 Round 2

---

## Problem 1: Journey to the X 

**Problem Statement**

Bardo is a young, courageous pirate. Upon plundering yet another ship, he finds a set of instructions that appears to lead to a treasure chest. However, the directions to the sweet booty are encoded. There are N lines of directions.

Individual instructions are listed as follows: X and D, where X is the number of units to travel in direction D.

D includes the 4 cardinal directions (North, East, South, West), but also 45° directions between them (North-East, North-West, South-East, South-West)

Bardo wants to know the total distance between his current location and the treasure chest so he knows how much fuel his private helicopter will require to pick him up and drop him off at the right direction.

**Input Specifications**

The first line of the input will contain an integer N (N < 150), which indicates the number of instructions Bardo sees.

The next N lines each contain a positive integer and a string, X (X < 100) and D, separated by a space.

D can be one of the following:
N - North
E - East
S - South
W - West
NE - Northeast
NW - Northwest
SE - Southeast
SW - Southwest

**Output Specifications** 

Output a single number, the distance between Bardo’s current location and the treasure chest on the map, rounded to the nearest 2 decimal places.

<details>
<summary>Click here to view the input string.</summary>
<br>

```
60
16 NW
91 N
77 E
45 SW
25 SW
86 N
3 E
5 E
2 SW
6 W
14 NW
7 N
89 SE
140 S
183 N
155 S
30 N
106 E
45 NW
23 SW
89 NE
2 N
6 SE
5 N
6 W
14 N
14 S
67 W
88 N
9 SE
80 SE
13 SW
44 NE
17 N
47 NW
85 S
6 E
66 SE
33 S
15 N
83 W
33 NW
77 NE
41 N
63 W
15 SE
6 NE
91 N
51 N
13 W
23 N
87 S
5 SE
7 NW
87 NW
6 NE
45 SE
46 SW
9 SW
7 NW
```

</details>

<br>


<details>
<summary>Click here to view the correct answer.</summary>
<br>

```
233.88
```

</details>

<br> 

<details>
<summary>Click here to view the Python 3 solution.</summary>
<br>

```python
import math

n = int(input())

#Used coordinate approach to help keep track of direction
coord = [0,0]

def moveAround(coord, x, d):
    if d == "N":
        coord[1] += x
    elif d == "E":
        coord[0] += x
    elif d == "S":
        coord[1] -= x
    elif d == "W":
        coord[0] -= x

    if d == "NE":
        coord[0] += x/math.sqrt(2)
        coord[1] += x/math.sqrt(2)
    elif d == "NW":
        coord[0] -= x/math.sqrt(2)
        coord[1] += x/math.sqrt(2)
    elif d == "SE":
        coord[0] += x/math.sqrt(2)
        coord[1] -= x/math.sqrt(2)
    elif d == "SW":
        coord[0] -= x/math.sqrt(2)
        coord[1] -= x/math.sqrt(2)
    return coord

def calculateDistance(x, y): 
    return (x**2+y**2)**(1/2) #Change coordinates into distance

for i in range(n):
    x, d = input().split()
    coord = moveAround(coord, int(x), d)

print(f"{round(calculateDistance(coord[0],coord[1]),2):.2f}")
```

</details>

<br>

---

## Problem 2: Dating Schedule

**Problem Statement**

Tong Tong is a very popular man, and receives many date requests. He wants to date as many people as possible. When he dates someone, the date must completely finish before proceeding to the next date. Given n dates, their respective starting times, and their respective ending times, find the maximum number of dates Tong Tong can have.

**Input Specifications**

The first line has one integer, n = 1000, the number of dates.
The next n lines each have two space separated integers, t1 and t2, the starting and ending times of each date respectively, with $0 \leq t_1 < t_2 \leq  24$.

**Output Specifications** 

Output a single integer, the maximum number of dates Tong Tong can have.

**Example**

Suppose his n dates are the following:

0 18

2 4

3 8

5 11

The maximum number of dates he may have is 2.


<details>
<summary>Click here to view the input string.</summary>
<br>

```
61000
22 24
8 15
17 24
0 9
6 24
0 14
15 24
8 24
17 24
22 24
6 10
11 24
4 13
3 10
11 19
19 24
23 24
1 23
11 20
17 24
5 18
19 24
18 24
14 24
12 20
17 24
3 14
2 13
10 13
7 21
15 24
3 18
10 22
19 24
9 16
9 11
4 17
0 10
23 24
3 8
12 21
10 24
9 24
16 24
11 22
17 24
13 24
19 24
14 24
21 24
7 24
14 23
19 23
20 24
19 24
15 19
16 24
4 23
6 24
0 21
10 24
1 3
9 11
22 24
22 24
9 20
5 24
6 15
13 19
12 24
16 24
7 24
10 24
4 24
19 24
18 24
10 24
18 21
12 24
20 22
3 8
5 24
10 17
18 24
11 14
9 11
9 16
16 24
19 24
0 23
7 17
13 23
15 18
17 24
14 24
7 24
10 21
3 24
13 24
6 19
18 24
13 24
17 21
14 24
23 24
11 24
17 23
2 9
2 5
7 24
14 24
16 24
1 16
8 24
20 24
16 24
4 13
19 24
15 24
8 15
4 6
19 24
6 23
9 11
5 24
23 24
5 14
19 24
21 24
13 24
15 24
2 24
5 15
3 11
6 24
12 17
22 24
9 13
11 21
1 23
1 21
21 24
15 21
14 20
5 19
6 13
10 24
13 24
2 4
10 17
8 24
13 15
22 24
1 24
1 24
14 24
19 24
16 24
15 24
0 10
15 19
4 20
22 24
16 24
2 24
6 24
17 24
12 23
13 24
19 24
19 24
18 24
12 17
17 24
4 6
10 18
14 24
15 24
14 24
16 24
12 24
1 21
16 24
14 24
10 24
13 24
19 21
9 22
21 24
21 24
2 24
19 24
16 24
3 24
12 18
23 24
19 24
4 14
19 24
11 23
10 23
0 18
8 24
16 24
22 24
15 24
23 24
12 22
4 24
4 16
14 24
11 24
3 24
22 24
0 6
19 24
2 9
10 24
14 24
17 24
15 24
18 24
20 24
15 23
15 24
22 24
7 13
5 14
16 24
20 24
18 22
12 17
16 24
19 24
13 17
4 11
2 7
0 16
4 8
5 9
2 9
0 4
16 24
11 13
20 24
7 24
2 14
12 24
10 24
9 16
17 24
6 24
15 17
7 17
6 18
18 24
15 17
1 6
13 24
12 24
12 24
12 16
0 7
7 24
21 24
7 19
5 8
6 13
8 24
9 13
22 24
17 24
11 24
5 7
5 19
0 2
0 9
5 9
9 11
3 24
9 24
12 23
8 24
4 18
12 23
10 24
15 24
8 18
13 24
20 24
20 24
13 15
5 21
4 17
2 12
12 20
18 24
1 12
2 9
4 20
8 15
3 20
10 23
2 10
12 15
7 22
9 17
16 24
21 24
15 24
1 24
9 12
6 12
7 24
15 18
10 23
0 21
20 22
2 15
13 17
18 24
1 15
15 24
10 24
16 24
14 24
22 24
10 12
6 24
19 24
15 24
22 24
10 16
5 19
10 24
10 17
3 5
23 24
19 24
14 20
15 18
18 24
17 24
17 24
19 24
21 24
5 12
13 24
9 23
11 24
18 24
15 24
19 24
6 19
18 24
22 24
16 24
17 24
2 8
3 23
6 21
3 15
5 17
13 24
21 24
14 16
9 24
12 23
5 24
8 22
11 24
9 22
22 24
20 24
9 18
9 24
20 24
10 24
2 5
4 21
16 24
22 24
12 24
6 21
4 20
0 9
3 9
1 12
2 7
0 21
7 24
23 24
12 15
20 24
18 24
17 19
11 22
14 24
19 24
14 24
7 18
7 12
20 24
6 24
3 17
11 20
5 19
3 14
8 14
15 24
9 24
0 3
17 21
5 24
20 23
7 9
14 22
7 24
0 15
7 24
10 23
23 24
17 24
19 24
2 4
23 24
10 24
5 15
4 24
2 12
15 21
1 24
16 24
16 24
17 24
5 24
4 17
16 18
3 17
9 24
17 24
16 24
16 24
12 15
5 21
8 24
13 24
23 24
16 24
4 6
7 24
10 24
21 24
1 14
19 24
23 24
13 24
15 24
11 16
20 24
22 24
2 4
0 14
10 23
17 24
2 18
7 17
12 24
20 24
6 15
2 24
7 12
3 22
13 17
23 24
19 24
12 24
8 24
8 24
17 24
5 8
11 24
9 24
1 18
15 24
5 12
5 24
6 14
13 24
5 11
20 24
21 24
0 18
5 7
7 9
2 7
6 17
5 15
6 21
17 24
11 24
13 24
5 16
23 24
13 24
19 24
3 6
9 16
5 13
23 24
23 24
23 24
23 24
11 24
8 12
11 24
2 24
23 24
20 24
13 24
0 3
8 18
13 24
14 24
0 22
4 13
15 24
20 24
14 24
17 24
0 14
17 21
0 14
6 14
14 18
13 19
3 24
10 24
3 11
17 22
9 15
11 18
23 24
23 24
11 24
6 24
17 24
0 5
21 24
12 24
14 17
9 24
2 19
20 24
7 15
17 24
18 24
3 12
21 24
16 18
14 17
10 23
22 24
20 24
16 24
15 22
22 24
8 24
19 24
3 5
22 24
2 19
22 24
15 20
18 24
0 10
1 14
19 24
8 16
17 24
1 4
9 22
5 24
1 12
10 24
3 12
4 20
0 19
18 22
14 24
10 22
11 21
14 24
11 14
9 22
10 24
8 24
4 22
16 24
21 24
8 23
13 17
16 24
17 24
2 19
23 24
2 6
17 24
0 10
21 24
21 24
1 20
1 4
0 17
5 24
19 24
11 24
4 9
13 21
10 24
1 4
8 24
9 17
1 23
11 18
18 22
1 9
7 14
19 24
14 20
0 9
15 24
16 24
4 24
19 24
16 24
20 24
23 24
9 17
12 24
15 19
8 24
21 24
15 24
4 16
20 24
10 24
14 24
2 21
17 24
21 24
3 16
0 17
12 20
13 22
0 2
16 24
9 24
0 15
17 24
2 12
3 13
9 24
8 24
5 21
19 24
21 24
20 24
13 23
18 24
5 11
7 19
14 18
3 15
12 21
14 24
0 23
15 22
18 24
3 20
7 24
10 16
10 17
1 14
9 13
16 23
9 11
23 24
18 23
8 24
22 24
16 24
23 24
23 24
22 24
13 24
19 24
19 24
15 20
18 24
19 24
4 19
6 14
22 24
0 8
8 23
10 24
17 24
2 4
7 16
0 5
10 12
16 19
22 24
3 11
4 21
18 24
6 20
4 23
4 6
23 24
14 17
20 24
14 22
2 24
9 24
11 13
23 24
2 8
9 19
8 19
5 24
8 24
16 24
7 24
11 24
15 23
22 24
15 17
20 24
4 19
9 14
0 4
9 23
14 24
18 21
20 24
10 20
14 17
8 24
15 18
4 23
21 24
12 18
6 24
4 6
22 24
7 14
8 24
9 19
21 24
20 24
21 24
7 22
5 15
8 24
2 8
14 23
6 22
10 16
15 18
9 24
21 24
12 22
22 24
10 19
20 24
4 11
12 24
7 24
17 24
4 21
1 20
23 24
8 24
5 9
19 24
17 24
4 6
19 21
2 13
19 24
19 24
16 22
15 24
19 24
4 9
20 24
19 24
1 8
3 14
0 13
23 24
0 4
8 21
0 15
14 24
17 24
23 24
8 21
15 18
15 24
4 8
18 24
19 24
14 24
19 24
9 24
15 24
6 24
11 24
6 23
22 24
13 24
15 24
19 24
7 24
2 21
13 24
14 24
18 24
22 24
23 24
8 24
18 24
23 24
16 24
14 24
6 8
0 22
8 18
9 22
1 14
2 23
11 24
22 24
20 24
11 24
15 24
21 24
6 8
11 14
6 22
21 24
14 24
12 24
5 21
16 24
10 12
11 24
15 24
23 24
4 21
0 13
18 22
10 21
13 24
18 24
10 23
12 23
5 24
12 24
0 3
18 24
2 22
3 23
1 9
4 24
17 24
9 24
22 24
6 20
14 24
12 24
11 15
3 11
15 20
7 15
22 24
15 24
4 24
1 11
7 17
19 24
19 24
5 24
19 24
5 12
4 15
1 6
4 23
3 22
23 24
19 24
19 24
21 24
22 24
18 24
14 16
9 20
19 22
0 18
18 24
10 24
15 24
2 17
0 11
16 24
14 24
20 24
22 24
16 21
18 24
5 8
22 24
7 16
16 24
22 24
14 24
20 24
16 24
16 24
17 24
5 14
8 19
5 11
16 24
9 24
8 24
23 24
17 24
18 24
7 21
9 21
8 15
14 22
0 10
18 24
23 24
17 24
22 24
19 24
16 24
21 24
1 13
2 9
17 21
3 11
17 24
8 12
3 11
16 24
2 7
13 24
13 24
5 24
8 23
19 24
5 16
5 13
5 12
19 21
19 24
15 24
7 20
10 24
20 24
5 13
9 24
12 20
5 21
17 21
13 16
9 16
18 24
11 24
19 21
11 21
14 19
6 23
19 24
11 22
4 8
1 16
15 23
13 24
20 24
1 16
1 12
18 24
```

</details>

<br>


<details>
<summary>Click here to view the correct answer.</summary>
<br>

```
11
```

</details>

<br> 

<details>
<summary>Click here to view the C++ solution.</summary>
<br>

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int n;
    vector<vector<int>> schedule;

    ifstream infile;
    infile.open("input.txt");

    infile >> n;

    for (int i = 0; i < n; ++i) {
        int val1, val2;
        infile >> val1 >> val2;
        schedule.push_back({val1, val2});
    }

    infile.close()

    sort(schedule.begin(), schedule.end(), [] (const vector<int> &a, const vector<int> &b) {return a[1] < b[1];});

    int last = schedule[0][1];
    int res = 1;

    for (int i = 1; i < n; ++i) {
        if (schedule[i][0] >= last) {
            last = schedule[i][1];
            ++res;
        }
    }

    cout << res << endl;
}
```

</details>

<br>

---

## Problem 3: A Grand Starfall

**Problem Statement**

Pantheon is about to cast Grand Starfall. He may only cast Grand Starfall once. There are n minions on Summoner's Rift, the ith of which has hi hit points. It is guaranteed that hi is at most m and is a positive integer. The time, t, begins at t = 0 seconds and increments by 1. At the beginning of the kth second, the ith minion has hi - k hit points left. If the minion has 0 (or less) hit points, it is dead. During the kth second, Pantheon may use Grand Starfall. When Pantheon uses Grand Starfall, every minion takes k + 1 damage immediately. For each minion Pantheon kills using Grand Starfall, he gains 5 gold. What is the earliest time Grand Starfall can be cast to maximize Pantheon's gold gains? 

**Input Specifications**

The first line has two space separated integers, n = 1000000, the number of minions, followed by m = 1000, the maximum hit points a minion can have.
The next line has n space separated integers, h1, h2, h3, … , hn, the hit points of each minion, with 0 < hi ≤ m for 1 ≤ i ≤ n.

**Output Specifications** 

Output a single integer, the earliest time t Grand Starfall can be cast to maximize Pantheon's gold gains.

**Example**

Suppose these are the minions and their health points:
1, 8, 3, 4, 5, 7, 2
Then the earliest time t to cast Grand Starfall such that gold gains are maximized is t = 2. The minions that Pantheon kills would be the 3rd, 4th, and 5th minions.

<details>
<summary>Click here to view the input string.</summary>
<br>

```
[VERY LARGE - ADD AS TXT FILE]
```

</details>

<br>


<details>
<summary>Click here to view the correct answer.</summary>
<br>

```
499
```

</details>

<br> 

<details>
<summary>Click here to view the C++ solution.</summary>
<br>

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int n;
    int m;

    ifstream infile;
    infile.open("input.txt");

    infile >> n >> m;

    vector<int> prefix_creation(m + 1, 0);
    vector<int> minions(m + 1, 0);

    for (int i = 0; i < n; ++i) {
        int temp;
        infile >> temp;
        ++prefix_creation[temp];
    }

    infile.close();

    for (int i = 1; i <= m; ++i) {
        minions[i] = minions[i - 1] + prefix_creation[i];
    }

    int best = 0;

    for (int t = 1; t <= m; ++t) {
        if ((minions[min(m, 2 * t + 1)] - minions[t]) > (minions[min(m, 2 * best + 1)] - minions[best])) {
            best = t;
        }
    }

    cout << best << endl;
}
```
</details>