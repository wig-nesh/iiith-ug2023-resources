---
title: "Week - 6"
bookHidden: false
---
# Practice problems for week 6

## Question 1 - "Non-Fancy Trains"

### Problem Description 
There are {{<katex>}}n{{</katex>}} stations numbered {{<katex>}}1, 2, ... n{{</katex>}}. Stations {{<katex>}}i{{</katex>}} and {{<katex>}}j{{</katex>}} are connected via a train ({{<katex>}}1 \le i, j \le n{{</katex>}}) iff {{<katex>}}|i - j| \le 2{{</katex>}}. The price of such a train would be {{<katex>}}|a_i - a_{j}|{{</katex>}} where {{<katex>}}a_i{{</katex>}} is an input array denoting the ratings of stations. If you travel optimally, find the minimum cost to travel form station {{<katex>}}1{{</katex>}} to station {{<katex>}}n{{</katex>}}.

### Input Format 

The first line of input contains a single integer {{<katex>}}n{{</katex>}} denoting the number of stations.

The second line contains {{<katex>}}n{{</katex>}} space-seperated integers, {{<katex>}}a_i{{</katex>}}.

### Input constraints 

-   {{<katex>}}2 \le n \le 10^5{{</katex>}}
-   {{<katex>}}1 \le a_i \le 10^4{{</katex>}}

### Output Format 

Print one integer, the minimum cost to travel from station {{<katex>}}1{{</katex>}} to station {{<katex>}}n{{</katex>}}.

### Sample Input 1 

    4
    10 30 40 20


### Sample Output 1

    30

### Sample Explanation
One valid path is to go through the stations {{<katex>}}1 \rightarrow 2 \rightarrow 4{{</katex>}}, which incurs the cost {{<katex>}}|10 - 30| + |30 - 20| = 30{{</katex>}}

**Sample Input 2 **

    2
    10 10



**Sample Output 2**

    0

---

## Question 2 - "String Palindrome Check"

### Problem Description

Given a string {{<katex>}}S{{</katex>}}, check if it is a palindrome using **recursion**.

### Input Format

The first line of input contains a single integer {{<katex>}}2T{{</katex>}} that denotes the number of test-cases. Then, {{<katex>}}2T{{</katex>}} lines follow.
The first line of each test-case contains a single integer {{<katex>}}N{{</katex>}} denoting the length of the string.
The second line of each test-case contains a string {{<katex>}}S{{</katex>}} of length {{<katex>}}N{{</katex>}}.

### Input constraints

- {{<katex>}}1 \le T \le 2 \times 10^5{{</katex>}}
- {{<katex>}}1 \le N \le 2 \times 10^5{{</katex>}}
- {{<katex>}}|S| = N{{</katex>}}
- {{<katex>}}S{{</katex>}} consists of only lowercase English alphabets
- The sum of {{<katex>}}N{{</katex>}} over all test-cases does not exceed {{<katex>}}2 \times 10^5{{</katex>}}

### Output Format 

For each test-case, on a single line, output `YES` if the string is a palindrome and `NO` if not

### Sample inputs and outputs

**Sample Input 1**

    2
    addd
    sss

**Sample Output 1**

    NO
    YES
    

**Sample Input 2**

    3
    addfdfdda
    a
    addfdffdda
    

**Sample Output 2**

    YES
    YES
    NO

---
