---
title: "Lab - 1"
bookHidden: false
---
# Lab 1 (Week of 14 August)

## Question 1 - "The Last 3"

### Problem Description

Given an integer `n` as input, print the last 3 bits of the number in its binary representation starting with the most significant bit among the three.

{{<hint info>}}
Note: The last three bits are the bits corresponding to the,{{<katex inline>}} 2^2, 2^1 {{</katex>}} and {{<katex inline>}} 2^0 {{</katex>}} positions (in that order)
{{</hint>}}

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23lab1q1)

### Input constraints 

{{<katex block text-center>}}
0 \le n \le 2^{31}
{{</katex>}}

### Input format

The only line of input contains a single integer `n`

### Output Format

Output three space-separated bits denoting the last three bits of the given number starting with the most significant bit among the three.

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `11`         | `0 1 1`       |
| `12`         | `1 0 0`       |

### Solution

```c
#include <stdio.h>

int main(void) {
    int n; scanf("%d", &n);
    printf("%d %d %d\n", !!(n & 1), !!(n & 2), !!(n & 4));
    return 0;
}
```

---

## Question 2 - "Date Formats"

### Problem Description

Given a date in `DD-MM-YY` format, output it in `MM-DD-YY` format.

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23lab1q2)

### Input format

The only line of input contains a valid date in `DD-MM-YY` format.

### Output Format

Output the date in `MM-DD-YY` format with no space separation.

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `25-03-04`         | `03-25-04`       |
| `15-08-23`         | `08-15-23`       |

### Solution

```c
#include <stdio.h>

int main(void) {
    int d, m, y;
    scanf("%d-%d-%d", &d, &m, &y);
    printf("%02d-%02d-%02d\n", m, d, y);
    return 0;
}
```

---
