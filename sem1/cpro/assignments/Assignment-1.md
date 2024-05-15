---
title: "Assignment - 1"
bookHidden: false
---
# Assignment 1

## Question 1

### Problem Description

Given an integer `n` as input, print its binary representation starting with the most significant bit, i.e. don't print the `0`'s before the first `1`.

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q1)

### Input constraints 

{{<katex block text-center>}}
0 \le n \le 2^{30}
{{</katex>}}

### Input format

The only line of input contains a single integer `n`

### Output Format

Output a continous stream of bits of `n` starting from the most significant bit.

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `11`         | `1011`       |
| `0`         | `0`       |

### Solution

```c
#include <stdio.h>
 
int main() {
  int x;
  scanf("%d", &x);
  
  if (x==0){
    printf("0");
    return 0;
  }
 
  int mask = 1 << 30;
  int flag_first_one = 0;
 
  while (mask) {
    if (x & mask) {
      printf("1");
      flag_first_one = 1;
    } else if (flag_first_one) {
      printf("0");
    }
    mask >>= 1;
  }
 
  return 0;
}

```

---

## Question 2

### Problem Description

Given an integer `n` between `2` and `100` as input, print all prime numbers from `1` to `n` (including `n`) in ascending order.

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q2)

### Input constraints 

{{<katex block text-center>}}
2 \le n \le 100
{{</katex>}}

### Input format

The only line of input contains a single integer `n`.

### Output Format

Output all primes that are less than or equal `n` in ascending order separated by spaces

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `2`         | `2`       |
| `6`         | `2 3 5`       |

### Solution

```c
#include <stdio.h>
 
int main() {
  int n;
  scanf("%d", &n);
 
  for (int i = 2; i <= n; i++) {
    if (i == 2 || i == 3 || i == 5 || i == 7) {
      printf("%d ", i);
    } else if (i % 2 != 0 && i % 3 != 0 && i % 5 != 0 && i % 7 != 0) {
      printf("%d ", i);
    }
  }
 
  return 0;
}
```

---


## Question 3

### Problem Description

You are given `width` and `height` of a rectangle and you need to print that rectangle.  
Look at samples for more clarity.  
The corners are to be represented by `'o'`.  
The vertical sides are represented by `'|'`  
The horizontal sides are represented by `'-'`  
The `'o'` counts towards both height and width.  

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q3)

### Input constraints 

{{<katex block text-center>}}
1\leq width\leq 1000, 1\leq height\leq1000
{{</katex>}}

### Input format

Two space separated integers, `width` and `height`.

### Output Format

Print the rectangle with the given `width` and `height`.

### Sample input and output


| Sample Input | Sample Output |
| ------------ | ------------- |
| `4 5`        | ` o--o`<br> `\|   \|`<br> `\|   \|`<br> `\|   \|`<br>   `o--o`              |
| `1 1`         | `o`       |
| `1 3`         | `o`<br>`\|`<br>`o`       |
|  `3 2`        |     `o-o`<br>`o-o`  |

### Solution

```c
#include <stdio.h>

int main() {
    int width, height;
    scanf("%d %d", &width, &height);
    for (int i = 1; i <= height; i++) {
        for (int j = 1; j <= width; j++) {
            if ((i == 1 && (j == 1 || j == width)) || (i == height && (j == 1 || j == width)))
                printf("o");
            else if (j == 1 || j == width) 
                printf("|");
            else if (i == 1 || i == height) 
                printf("-");
            else 
                printf(" ");
        }
        printf("\n");
    }
    return 0;
}
```

---


## Question 4

### Problem Description

You are given three integers `n`, `x` and `y`. You need to print the first `n` terms of the sequence `S` which starts with {{<katex inline>}}S_1=x{{</katex>}} and {{<katex inline>}}S_2=y{{</katex>}} and further terms are derived from the relation  {{<katex inline>}}S_i = S_{i-1} + S_{i-2}{{</katex>}}.

{{<hint info>}}
The first `n` values of `S` are guaranteed to fit in `int`
{{</hint>}}

[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q4)

### Input constraints 

{{<katex block text-center>}}
1 \le n < 50
{{</katex>}}
<br>
{{<katex block text-center>}}
0\leq x,y\leq 1e5
{{</katex>}}
{{<katex block text-center>}}
{{</katex>}}


### Input format

The only line of input contains 3 space separated integers `n`, `x` and `y`.

### Output Format

Output one line containing `n` space-seperated integers, denoting the first `n` terms of the sequence `S`.

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `5 1 2`         | `1 2 3 5 8`       |

### Solution

```c
#include <stdio.h>

int main(){
    int n, x, y;
    scanf("%d %d %d", &n, &x, &y);

    for (int i = 1; i <= n; i++) {
        if(i == 1)printf("%d ", x);
        else if(i == 2)printf("%d ", y);
        else{
        int z = x + y;
        printf("%d ", z);
        x = y;
        y = z;
        }
    }

    return 0;
}
```
---


## Question 5

### Problem Description

Kushagra is in love with pairs. He has a list of numbers where each number has a duplicate pair. Unfortunately, there is one number that does not have a pair. Help him figure out which number it is.


[Link to problem on OJ](http://oj.iiit.ac.in/problem/cpro23a1q5)

### Input constraints 


{{<katex block text-center>}}
3 \le n \le 10^{6}
{{</katex>}}
<br>
{{<katex block text-center>}}
1 \le A_i \le 10^{9}
{{</katex>}}
{{<katex block text-center>}}
{{</katex>}}


### Input format

The first line contains an integer `n` denoting the numbers present in the list.

The second line contains n space-separated integers {{<katex inline>}}[A_0, A_1, A_2,... A_{n-1}]{{</katex>}}.

### Output Format

A single integer, the number in the array without a pair

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| ` 5`<br> `4 5 6 4 5`         | `6`       |
| ` 7`<br> ` 3 3 3 3 3 2 2`         | `3`       |

### Solution

```c
#include <stdio.h>

int main()
{
	int n;
	scanf("%d", &n);
	int ans = 0;
	for(int i = 1; i <= n; i++)
	{
		int x;
		scanf("%d", &x);
		ans ^= x;
	}
	printf("%d\n", ans);
}
```

---