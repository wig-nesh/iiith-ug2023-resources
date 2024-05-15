---
title: "Week - 2"
bookHidden: false
---
# Practice problems for week - 2 (Week of 21 August)

## Question 1

### Problem Description
You are given a `3 x 3` grid filled with integers **1 to 9**, in the following way:

<div align="center">

| 1 | 2 | 3 |
| - | - | - |
| 4 | 5 | 6 |
| 7 | 8 | 9 |

</div>

You will be given two natural numbers `A` and `B`, both between 1 and 9. Your task is to find out if the two small squares with `A` and `B` written on them are horizontally adjacent.

### Input constraints 

A and B are natural numbers and
{{<katex block text-center>}}
1 \le A,B \le 9
{{</katex>}}
<br>
{{<katex block text-center>}}
A \le B
{{</katex>}}

### Input format

The only line of input contains two space-separated natural numbers `A` and `B`

### Output Format

Print `YES` if the two squares are horizontally adjacent, and `NO` otherwise.

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `5 6`         | `YES`       |
| `6 7`         | `NO`       |

### Solution

```c
#include <stdio.h>

int main() {
    int A, B;
    scanf("%d %d", &A, &B);

    if ((A - 1) % 3 == (B - 1) % 3) 
        printf("YES\n");
    else 
        printf("NO\n");
    return 0;
}
```

---

## Question 2

### Problem Description

Shiven was given a problem to solve as assignment. In the problem, he was given two numbers `n` and `s`. He was asked to create a sequence of `n` **non-negative integers** such that the median of the sequence is **as large as possible** and that sum of all numbers of the sequence is `s`. Can you help Shiven find the maximum possible median of such a sequence?



**Note:** The definition of the median is the {{<katex inline>}}  \left\lceil \frac{n}{2}\right\rceil^{th} {{</katex>}}   element of a sequence
noted in the ascending order

### Input constraints 

{{<katex block text-center>}}
1 \le n \le 10^{8}
{{</katex>}}

### Input format

The only line of input contains two space-separated integers `n` and `s`

### Output Format

Output a single integer that is the **maximum median** of such a sequence.

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `7 17`         |`4`       |

### Solution

```c
#include <stdio.h>

int main()
{
    int n, s;
    printf("Enter two numbers: ");
    scanf("%d %d", &n, &s);
    int m = n / 2 + 1;
    int ans = s / m;
    printf("The maximum value of median is: %d\n", ans);
    return 0;
}
```

---
