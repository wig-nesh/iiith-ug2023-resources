---
title: "Assignment - 2"
bookHidden: false
---
# Assignment 2

## Question 1 - "Doubling Investments"

### Problem Description

*Mitansh is world’s best investor.  Whatever the amount he has today, it doubles on the next day.*

Initially he starts, with amount zero. Each day in the morning, he can choose to invest {{<katex>}}\$x{{</katex>}} more in addition to his previous amount {{<katex>}}\$y{{</katex>}}. And on next day, his total amount becomes {{<katex>}}\$2(x+y){{</katex>}}. 

However, he wants to get exactly {{<katex>}}\$z{{</katex>}} on some day. 

What is the minimum amount of money he needs to invest, in order to get {{<katex>}}\$z{{</katex>}} at some moment?

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q1)

### Input Format

The first and only line of input contains a single integer {{<katex>}}z{{</katex>}} which denotes the desired amount.

### Input constraints

-   {{<katex>}}0 \le z \le 10^9{{</katex>}}

### Output Format 

On a single line, output the minimum amount of money that needs to be invested, in order to get exactly {{<katex>}}\$z{{</katex>}} on some day.

### Sample inputs and outputs

**Sample Input 1**

    7

**Sample Output 1**

    3
    
**Explanation:** Mitansh will invest {{<katex>}}\$1{{</katex>}} on the {{<katex>}}1^{st}{{</katex>}}, {{<katex>}}2^{nd}{{</katex>}} and {{<katex>}}3^{rd}{{</katex>}} days. At the beginning of the second day he has {{<katex>}}\$2{{</katex>}} (thanks to the {{<katex>}}\$1{{</katex>}} doubling). He invests {{<katex>}}\$1{{</katex>}} again, leading to the amount being {{<katex>}}\$3 \times 2 = \$6{{</katex>}} at the beginning of the third day. He again invests {{<katex>}}\$1{{</katex>}} to obtain the desired amount of {{<katex>}}\$7{{</katex>}}.

**Sample Input 2**

    16

**Sample Output 2**

    1
    
**Explanation:** Mitansh invests {{<katex>}}\$1{{</katex>}} on the first day which doubles four times to obtain {{<katex>}}\$16{{</katex>}}.

**Sample Input 3**

    0

**Sample Output 3**

    0

### Solution

```c
#include <stdio.h>

int main() {
    int n, count = 0;
    scanf("%d", &n);
    while(n != 0) {
        count += (n % 2);
        n /= 2;
    }
    printf("%d\n", count);
    return 0;
}

```

---

## Question 2 - "Rotate Edges"

### Problem Description

*Kitansh Mayathwal was thinking of an easy problem which he can apply MOSS on. He came up with this problem.*

You are given a grid with {{<katex>}}N{{</katex>}} rows and {{<katex>}}N{{</katex>}} columns. An integer {{<katex>}}A_{i,j}{{</katex>}} is written on the square at the {{<katex>}}i{{</katex>}}-th row from the top and {{<katex>}}j{{</katex>}}-th column from the left. Here, it is guaranteed that {{<katex>}}A_{i,j}{{</katex>}} is either 0 or 1.

An integer {{<katex>}}D{{</katex>}} is also given as input. It is guaranteed that {{<katex>}}D{{</katex>}} is either 0 or 1. 

If {{<katex>}}D = 0{{</katex>}}, shift the integers written on the outer squares anticlockwise by one square each, and print the resulting grid.

If {{<katex>}}D = 1{{</katex>}}. shift the integers written on the outer squares clockwise by one square each, and print the resulting grid.

Here, the outer squares are those for which at least one of the following conditions is true:
- The square is present on the first row
- The square is present on the {{<katex>}}N{{</katex>}}-th row
- The square is present on the first column
- The square is present on the {{<katex>}}N{{</katex>}}-th column

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q2)

### Input Format

The first line of input contains a single integer {{<katex>}}N{{</katex>}} that denotes the size of the grid. The next {{<katex>}}N{{</katex>}} lines describe the grid.

The {{<katex>}}i^{th}{{</katex>}} line describes the {{<katex>}}i^{th}{{</katex>}} row of the grid, {{<katex>}}A_{i, 1}, A_{i, 2}, \dots, A_{i, N}{{</katex>}}.

The final line of input contains a single integer {{<katex>}}D{{</katex>}} which denotes the direction of rotation.

In other words, the input is in the following format

    N
    A_1,1 A_1,2 ... A_1,N
    A_2,1 A_2,2 ... A_2,N
    ...
    A_N,1 A_N,2 ... A_N,N
    D

### Input constraints

-   {{<katex>}}2 \le N \le 100{{</katex>}}
-   {{<katex>}}0 \le A_{i, j} \le 1 (1 \le i, j \le N){{</katex>}}
-   {{<katex>}}0 \le D \le 1{{</katex>}}

### Output Format 

Output the appropriately rotated grid {{<katex>}}B{{</katex>}} in the following format:

    B_1,1 B_1,2 ... B_1,N
    B_2,1 ...
    ...
    B_N,1 B_N,2 ... B_N,N

### Sample inputs and outputs

**Sample Input 1**

    3
    1 1 1
    0 1 0
    1 0 1
    1

**Sample Output 1**

    0 1 1
    1 1 1
    0 1 0
    

**Sample Input 2**

    3
    1 1 1
    0 1 0
    1 0 1
    0
    

**Sample Output 2**

    1 1 0 
    1 1 1 
    0 1 0

### Solution

```c

#include <stdio.h>

int main() {
    int n; scanf("%d", &n);
    int a[n][n];
    for (int i = 0; i < n; i++) for (int j = 0; j < n; j++) scanf("%d", &a[i][j]);
    int d; scanf("%d", &d);
    int b[n][n];
    if (d) {
        for (int j = 1; j < n; j++) b[0][j] = a[0][j - 1];
        for (int i = 1; i < n; i++) b[i][n - 1] = a[i - 1][n - 1];
        for (int j = 0; j < n - 1; j++) b[n - 1][j] = a[n - 1][j + 1];
        for (int i = 0; i < n - 1; i++) b[i][0] = a[i + 1][0];
    } else {
        for (int j = 0; j < n - 1; j++) b[0][j] = a[0][j + 1];
        for (int i = 0; i < n - 1; i++) b[i][n - 1] = a[i + 1][n - 1];
        for (int j = 1; j < n; j++) b[n - 1][j] = a[n - 1][j - 1];
        for (int i = 1; i < n; i++) b[i][0] = a[i - 1][0];
    }
    for (int i = 1; i <= n - 2; i++) for (int j = 1; j <= n - 2; j++) b[i][j] = a[i][j];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) printf("%d ", b[i][j]);
        printf("\n");
    }
    return 0;
}

```


---

## Question 3 - "Open Doors"

### Problem Description

Madhav is a very lazy boy. He doesn’t like to do sports. So our PEC instructor has assigned him a task which he should complete in an hour. 
There are {{<katex>}}n{{</katex>}} doors which are all closed initially. Madhav should perform {{<katex>}}n{{</katex>}} iterations. In the {{<katex>}}i^\text{th}{{</katex>}} iteration he starts from {{<katex>}}i^\text{th}{{</katex>}} door and goes to each multiple of {{<katex>}}i{{</katex>}} untill {{<katex>}}n{{</katex>}} i.e. {{<katex>}}(i, 2*i, 3*i…..){{</katex>}} and toggles the door. Here toggles means if the door is open, he will close it and if it is closed he will open it. 

After all {{<katex>}}n{{</katex>}} iterations he has to tell which all doors are still opened. As Madhav is smart, he tries to solve this task using some program. Can you help him with this task ?

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q3)

### Input Format

You will be given only one integer {{<katex>}}n{{</katex>}} which are the number of doors. 

### Input constraints

{{<katex>}}1 \leq  n \leq 10^{10}{{</katex>}}

Subtask 1 :  (45 points)

{{<katex>}}1 \leq  n \leq 10^3{{</katex>}}

Subtask 2 : (55 points)

Original Constraints

### Output Format 

Print the open door numbers in increasing order.

### Sample inputs and outputs

**Sample Input 1**

    1
    

**Sample Output 1**

    1

**Sample Input 2**

    4
    

**Sample Output 2**

    1 4

### Solution

```c
#include<stdio.h>

int main() {
    long long n;
    scanf("%lld", &n);
    for(int i = 1; 1ll * i * i <= n; i++)
        printf("%lld ", i * i);
    printf("\n");
    return 0;
}

```


---

## Question 4 - "Count Palindromes"

### Problem Description

Given an array {{<katex>}}A{{</katex>}} of length {{<katex>}}N{{</katex>}}, count the number of **non-empty subarrays** which are palindromes.

Note that two subarrays are considered to be different if they either start at different indices or end at different indices. The actual elements in the two subarrays do not influence this.

A subarray is a contiguous segment of the array which can be obtained be deleting one or more elements from the beginning or the end of the array.

An array is said to be a palindrome if it reads the same backwards and forwards. For example, {{<katex>}}[1, 2, 2, 1], [1], [1, 2, 1]{{</katex>}} are all palindromic arrays.

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q4)

### Input Format

The first line of input contains a single integer {{<katex>}}N{{</katex>}} that denotes the size of the array.

The second line of input contains {{<katex>}}N{{</katex>}} space-separated integers {{<katex>}}A_1, A_2, \dots, A_N{{</katex>}} that describe the array.

### Input constraints

-   {{<katex>}}1 \le N \le 100{{</katex>}}
-   {{<katex>}}0 \le A_i \le 10^9{{</katex>}}

### Output Format 

Output a single positive that denotes the count of the non-empty palindromic subarrays

### Sample inputs and outputs

**Sample Input 1**

    4
    1 2 2 1

**Sample Output 1**

    6
    
**Explanation:** The subarrays satisfying the given conditions are: {{<katex>}}[1], [2], [2], [1], [2, 2], [1, 2, 2, 1]{{</katex>}}

### Solution

```c
#include <stdio.h>

int main() {
    int n; scanf("%d", &n);
    int a[n];
    for (int i = 0; i < n; i++) scanf("%d", &a[i]);
    int ans = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            int good = 1;
            int p = i, q = j;
            while (p < q) {
                if (a[p] != a[q]) {
                    good = 0;
                    break;
                }
                p++, q--;
            }
            ans += good;
        }
    }
    printf("%d\n", ans);
    return 0;
}

```


---

## Question 5 - "PEC woes"

### Problem Description

As you all know, no student in IIIT likes PEC because they make us do some strange things. Once, they assigned a task to Pratham. They spread some rectangles sheets on the football ground and asked Pratham to calculate the total area covered by the rectangular sheets. 

So, the task is like you are given some rectangles which are parallel to X or Y axis. Specifically, the i-th sheet covers all points {{<katex>}}(x, y){{</katex>}} that satisfy  {{<katex>}}a_i≤x≤b_i{{</katex>}}  and {{<katex>}}c_i≤y≤d_i{{</katex>}}.
You have to calculate the total area which is covered by the rectangular sheets.

You have to calculate the total area which is covered by the recatngular sheets. For more explanation, read the sample test case.

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q5)

### Input Format

First line contains an integer N which denotes the total number of rectangular sheets. 

The following N lines contain : {{<katex>}}a_i{{</katex>}}   {{<katex>}}b_i{{</katex>}}  {{<katex>}}c_i{{</katex>}}  {{<katex>}}d_i{{</katex>}}

### Input constraints

- {{<katex>}}1 \leq N \leq 100{{</katex>}}
- {{<katex>}}0 \leq a_i < b_i \leq 100{{</katex>}}
- {{<katex>}}0 \leq c_i < d_i \leq 100{{</katex>}}

### Output Format 

Output a single integer the area covered by rectangular sheets. 

### Sample inputs and outputs

**Sample Input 1**

    3
    0 5 1 3
    1 4 0 5
    2 5 2 4

**Sample Output 1**

    20
    
**Explanation:** For an explanation of the sample input 1, refer to [this](https://drive.google.com/file/d/1ffWW1G-lHxW_TfWDgwemVMtr-PdOOY2Z/view?usp=sharing)  link. We can count that the sheets cover 20 squares.
    
**Sample Input 2**

    3
    0 1 0 1
    0 3 0 5
    5 10 0 10

**Sample Output 2**

    65

### Solution

```c
#include <stdio.h>
#include <string.h>

int main() {
    int n; scanf("%d", &n);
    const int MAX_N = 101;
    int g[MAX_N][MAX_N];
    memset(g, 0, sizeof(g));
    while (n--) {
        int a, b, c, d;
        scanf("%d %d %d %d", &a, &b, &c, &d);
        for (int i = c; i < d; i++) for (int j = a; j < b; j++) g[i][j] = 1;
    }
    int ans = 0;
    for (int i = 0; i <= 100; i++) for (int j = 0; j <= 100; j++) ans += g[i][j];
    printf("%d\n", ans);
    return 0;
}

```

---