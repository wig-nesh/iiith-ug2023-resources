---
title: "Mid-Sem Lab Exam"
bookHidden: false
---
# Mid-Sem Lab Exam

## Question 1 - "Voting"

### Problem Description

*The Elections for the new academic year are in full swing!*

There are {{<katex>}}N{{</katex>}} students in the college and two candidates for the current elections (where {{<katex>}}N{{</katex>}} is guaranteed to be an odd number). The students cast their votes in the form of {{<katex>}}0s{{</katex>}} or {{<katex>}}1s{{</katex>}} where the {{<katex>}}i^{th}{{</katex>}} vote ({{<katex>}}1 <= i <= N{{</katex>}}) being {{<katex>}}1{{</katex>}} represents a vote to candidate A and it being {{<katex>}}0{{</katex>}} represents a vote for candidate B.

A candidate wins the elections if they have the strict majority. That is, if the number of votes cast for them is strictly greater than the number of votes cast for the other candidate.

Output `Yes` if candidate A wins the elections and `No` otherwise.

[Link to problem on OJ](http://oj-test.iiit.ac.in/problem/cpro23midq1)

### Input constraints 

- {{<katex block>}} 1 \le N \le 99 {{</katex>}}
- {{<katex>}} N \text{ is an odd number} {{</katex>}}
- {{<katex>}} V_i = \{0, 1\} {{</katex>}}

### Input format

The first line of input contains {{<katex>}}N{{</katex>}}, the number of students. Then, {{<katex>}}N{{</katex>}} line follows.

The {{<katex>}}i^{th}{{</katex>}} line contains a single integer {{<katex>}}V_i = \{0, 1\}{{</katex>}} where {{<katex>}}1{{</katex>}} represents a vote for candidate A and {{<katex>}}0{{</katex>}} represents a vote for candidate B.

### Output Format

Output `Yes` if candidate A wins the elections and `No` otherwise.

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `3` <br> `1` <br> `0` <br> `1`         | `Yes`       |

**Explanation:** There are {{<katex>}}2{{</katex>}} votes for candidate A and {{<katex>}}1{{</katex>}} vote for candidate B. Therefore, candidate A has the majority and wins the elections.

| Sample Input | Sample Output |
| ------------ | ------------- |
| `5` <br> `0` <br>    `0` <br>    `1` <br>    `0` <br>    `1`         | `No`       |


**Explanation:** There are {{<katex>}}2{{</katex>}} votes for candidate A and {{<katex>}}3{{</katex>}} votes for candidate B. Therefore, candidate B has the majority and wins the elections.

### Solution

```c
#include <stdio.h>

int main() {
    int n; scanf("%d", &n);
    int a = 0, b = 0;
    for (int i = 0; i < n; i++) {
        int x; scanf("%d", &x);
        if (x) a++;
        else b++;
    }
    if (a > b) printf("Yes\n");
    else printf("No\n");
    return 0;
}
```

---

## Question 2 - "Jump Back"

### Problem Description

There are {{<katex>}}N{{</katex>}} trees in the forest, numbered Tree 1, Tree 2,..., Tree {{<katex>}}N{{</katex>}}.

Tree 1, is a special tree which is home to the entire forest. Each tree {{<katex>}}i{{</katex>}} ({{<katex>}}2 \le i \le N{{</katex>}}), has a parent tree {{<katex>}}T_i{{</katex>}} from which it grew. It is guaranteed that {{<katex>}}T_i < i{{</katex>}}. 

You are currently on tree {{<katex>}}N{{</katex>}} and want to reach tree {{<katex>}}1{{</katex>}}. However, from a given tree, you can only jump to its parent tree (unless you are already on tree {{<katex>}}1{{</katex>}}, in which case you have already reached the destination). 

For example, consider the input {{<katex>}}[1 1 2 4]{{</katex>}} which means, {{<katex>}}T_2 = 1, T_3 = 1, T_4 = 2, T_5 = 4{{</katex>}} (note that tree {{<katex>}}1{{</katex>}} has no parent tree). Starting from tree {{<katex>}}5{{</katex>}}, the only option is to jump to tree 4, its parent. Similarly, from tree 4, you jump to tree 2. Finally, from tree 2 you jump to tree 1, taking a total of 3 jumps to go from tree 5 to tree 1.

Find the number of jumps that you need to make in order to reach tree {{<katex>}}1{{</katex>}} starting from tree {{<katex>}}N{{</katex>}}. It can be shown that you can reach it in a finite number of jumps.

[Link to problem on OJ](http://oj-test.iiit.ac.in/problem/cpro23midq2)

### Input constraints 

- {{<katex>}}2 \le N \le 50{{</katex>}}
- {{<katex>}}1 \le T_i < i{{</katex>}} ({{<katex>}}2 \le i \le N{{</katex>}})

### Input format

The first line of input contains a single integer {{<katex>}}N{{</katex>}}, the number of trees.

The following line contains {{<katex>}}N - 1{{</katex>}} space separated integers, {{<katex>}}T_2, T_3, \dots, T_N{{</katex>}} where {{<katex>}}T_i{{</katex>}} denotes the parent of the {{<katex>}}i^{th}{{</katex>}} tree.

### Output Format

Output a single integer denoting the number of jumps required to go from tree {{<katex>}}N{{</katex>}} to tree {{<katex>}}1{{</katex>}}.

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `3` <br>   `1 2`         | `2`       |


| Sample Input | Sample Output |
| ------------ | ------------- |
| `5` <br>    `1 1 2 4`        | `3`       |


### Solution

```c
#include <stdio.h>

int main() {
    int n; scanf("%d", &n);
    int a[n];
    a[0] = -1;
    for (int i = 1; i < n; i++) {
        scanf("%d", &a[i]);
        a[i]--;
    }
    int curr = n - 1, ans = 0;
    while (curr != -1) {
        ans++;
        curr = a[curr];
    }
    printf("%d\n", ans - 1);
    return 0;
}
```

---

## Question 3 - "Max AND"

### Problem Description

In this problem, we use the symbol `^` to denote the  **bitwise AND** operation, and the symbol `v` to denote the  **bitwise OR** operation.

Given an array of integers {{<katex>}}A{{</katex>}} of length {{<katex>}}N{{</katex>}}, {{<katex>}}A_1, A_2, \dots, A_N{{</katex>}}. Define a "set operation" as the following:

- Select any index {{<katex>}}i{{</katex>}} where {{<katex>}}1 \le i \le N{{</katex>}} and set the {{<katex>}}j^{th}{{</katex>}} bit of {{<katex>}}A_i{{</katex>}} where {{<katex>}}j{{</katex>}} is any integer between {{<katex>}}0{{</katex>}} and {{<katex>}}30{{</katex>}} inclusive. In other words, replace {{<katex>}}A_i{{</katex>}} with {{<katex>}}A_i{{</katex>}} `v` {{<katex>}}2^j{{</katex>}}.

You are also given a non-negative integer {{<katex>}}K{{</katex>}}. You can perform  **at most** {{<katex>}}K{{</katex>}} operations on the given array. After doing so, output the maximum possible value of {{<katex>}}A_1{{</katex>}} `^` {{<katex>}}A_2{{</katex>}} `^` {{<katex>}}\dots{{</katex>}} `^` {{<katex>}}A_N{{</katex>}}. 

[Link to problem on OJ](http://oj-test.iiit.ac.in/problem/cpro23midq3)

### Input constraints 

- {{<katex>}}1 \le N \le 2 \times 10^5{{</katex>}}
- {{<katex>}}0 \le K \le 10^9{{</katex>}}
- {{<katex>}}0 \le A_i < 2^{31}{{</katex>}}

### Input format

The first line of input contains two space separated integers {{<katex>}}N{{</katex>}} and {{<katex>}}K{{</katex>}}, denoting the length of the array and the maximum number of operations that can be performed respectively.

The second line contains {{<katex>}}N{{</katex>}} space separated integers {{<katex>}}A_1, A_2, \dots, A_N{{</katex>}} that denote the initial array.

### Output Format

Output the maximum possible value of the bitwise AND of the entire array after performing at most {{<katex>}}K{{</katex>}} operations.

### Sample input and output

| Sample Input | Sample Output |
| ------------ | ------------- |
| `3 2` <br>    `2 1 1`         | `2`       |

**Explanation:** We set the {{<katex>}}j = 1{{</katex>}} bit (that is, the bit corresponding to {{<katex>}}2^1{{</katex>}}) for {{<katex>}}A_2{{</katex>}} and {{<katex>}}A_3{{</katex>}}. This requires {{<katex>}}2 \le K{{</katex>}} operations. After doing so, the array now looks like {{<katex>}}[2, 3, 3]{{</katex>}}, giving us a bitwise AND value of {{<katex>}}2{{</katex>}} which can be shown is the maximum possible value for the given input.

| Sample Input | Sample Output |
| ------------ | ------------- |
| `7 0`
    `4 6 6 28 6 6 12`         | `4`       |


**Explanation:** Here, {{<katex>}}K = 0{{</katex>}}. So, we cannot perform any operations. Hence, the bitwise AND of the initial array, {{<katex>}}4{{</katex>}} is our final answer.

### Solution

```c
#include <stdio.h>

int main() {
    int n, k; scanf("%d %d", &n, &k);
    int cnt[31] = {0};
    for (int i = 0; i < n; i++) {
        int x; scanf("%d", &x);
        for (int j = 0; j < 31; j++, x /= 2) {
            cnt[j] += (x & 1);
        }
    }
    int ans = 0;
    for (int i = 30; i >= 0; i--) {
        if (k >= n - cnt[i]) {
            ans |= (1 << i);
            k -= (n - cnt[i]);
        }
    }
    printf("%d\n", ans);
    return 0;
}
```

---
