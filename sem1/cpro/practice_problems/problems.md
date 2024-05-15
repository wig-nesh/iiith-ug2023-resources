---
title: "Problems"
bookHidden: false
---
# Practice Problems


## 1. Cycles in a permutation

Let $\pi:\\{1,\cdots, n\\} \rightarrow \\{1,\cdots, n\\}$ be permutation (that is a one-one onto function). 
The cycle containing 1 is the sequence of numbers
$$1\qquad \pi(1)\qquad \pi(\pi(1))\qquad \pi(\pi(\pi(1)))\qquad \cdots$$
Notice that the sequence is periodic (Why?)  and the period is called the size of the cycle containing 1. Similarly one can define the cycle containing 2, 3 etc. 
Write a program to take $n$ and a permutation of $\\{1,\cdots,n\\}$ as inputs and print all the cycles (you can stop at the period).    

For example:   
For input 4 and permutation 2 3 4 1 (ie $\pi(1) = 2, \pi(2) = 3, \pi(3) = 4, \pi(4) = 1$), it should output 1->2->3->4->1.  
For input 4 and permutation 1 2 3 4, (ie the identity permutation) it should output 1->1, 2->2, 3->3, 4->4.  
For input 4 and permutation 2 1 4 3 (ie $\pi(1) = 2, \pi(2) = 1, \pi(3) = 4, \pi(4) = 3$), it should output 1->2->1, 3->4->3.  



## 2. Cycles in a LinkedList

In a linked list, its possible to have a cycle in the nodes. That is, while iterating through the nodes, a node could be there whose next pointer is pointing to a previous node. 

Write a C program which takes linked list as input and checks if it has a cycle.   

Hint: You can add extra fields into the Node struct, for aiding this program.  

For example:  
On input linked list 1->2->3->4->5->6->3, the program should print true.  
On input linked list 1->2->3->4->5->6->NULL, the program should print false.    

## 3. Bank
Problems in the comments
```c
/* Build a program for managing a bank.
   There should be a database of bank
   accounts and transactions. We should
   be able to add new accounts, 
   new transactions (credit/debit) and 
   compute the balance of a account     */
#include <stdio.h>
#include <string.h>

typedef enum AccountType {
  Savings,
  Current
} AccountType;

typedef enum TransactionType {
  Credit,
  Debit
} TransactionType;

typedef struct Transaction {
  TransactionType type;
  struct BankAccount* account;
  int amount;
} Transaction;

typedef struct BankAccount {
  char name[100];
  int pin;
  AccountType type;
  // passbook is an array of transactions
  // pointers to avoid taking too much memory
  struct Transaction* passbook[1000]; 
  int transactions_count;
} BankAccount;

typedef struct BankDatabase {
  BankAccount accounts[1000];
  Transaction transactions[10000];
  int accounts_count;
  int transactions_count;
} BankDatabase;

// compute the total amount of money 
// with the bank amoung all the accounts
int compute_money_with_bank(
                      BankDatabase* db) {
  int sum = 0;  
  for(int i = 0; 
        i < db->transactions_count; i++) {
    switch(db->transactions[i].type) {
      case Credit:
        sum += db->transactions[i].amount;
        break;
      case Debit:
        sum -= db->transactions[i].amount;
        break;
    }  
  }
  return sum;
}

int compute_balance(BankAccount* acc) {
  // Problem 2 a.) fill in the code to 
  // find the balance of the account 
  // 'acc'.(3 marks)
}

BankAccount* add_bank_account(char* name, 
                    int pin, AccountType type,
                    BankDatabase* db) {
  // Problem 2 b.) fill in the code to add 
  // a new account 'acc' to the bank 
  // database 'db'. The function should 
  // also return a pointer to the bank 
  // account created in 'db'. (3 marks)
}

Transaction* add_transaction(
            TransactionType type, 
            BankAccount *account, 
            int amount, BankDatabase* db) {
  // Problem 2 c.) Fill in the code for 
  // adding a transaction to the system. 
  // The logic should be written such 
  // that the all the other functions in
  //  this program continue to work 
  // correctly. (4 marks)
}

int main() {

  BankDatabase db;
  db.accounts_count = db.transactions_count = 0;
  BankAccount acc = { .pin = 1234, 
                      .transactions_count = 0};
  strcpy(acc.name, "Ivan");
  BankAccount* acc_ptr = add_bank_account(
                 acc.name,acc.pin,acc.type, &db);
  add_transaction(Credit, acc_ptr, 10000, &db);
  add_transaction(Debit, acc_ptr, 2000, &db);
  add_transaction(Credit, acc_ptr, 5000, &db);

  // should print 13000
  printf("Account balance is %d\n", 
         compute_balance(acc_ptr));

  BankAccount acc2 = { .pin = 6897, 
                      .transactions_count = 0};
  strcpy(acc2.name, "Jake");
  BankAccount* acc_ptr2 = add_bank_account(
             acc2.name, acc2.pin,acc2.type, &db);
  add_transaction(Credit, acc_ptr2, 100000, &db);
  add_transaction(Debit, acc_ptr2, 20000, &db);
  add_transaction(Credit, acc_ptr2, 50000, &db);

    // should print 130000
  printf("Account balance is %d\n", 
         compute_balance(acc_ptr2));

  // should print 143000
  printf("Total Money with bank is %d\n", 
         compute_money_with_bank(&db)); 
}
```


## 4. Enumerating Sets

Write a C program which takes $n$, $k$, and some $n$ numbers $a_1,a_2,\cdots,a_n$ as inputs and 
prints all subsets of them of size $k$.   

Example:  
On input $n=4, k =2$ and $2,4,6,8$ it should output  
```
{2, 4}, {2, 6}, {2, 8}, {4, 6}, {4, 8}, {6, 8}
```

## 5. Recursively Enumerating Permutations


Consider all arrangements of $k$ items
   from $n$ objects. For $n=3, k=2$, they
   are $12, 21,13,31,23,32$. The number
   of such arrangements is 
   $$^nP_k = n(n-1)\cdots(n-k+2)(n-k+1).$$ 
   Bellow is a program which when given $n,k$
   as input, prints all arragements of $k$
   items from $n$ objects.         

Problems in the comments:

```c
/* Consider all arrangements of $k$ items
   from $n$ objects. For $n=3, k=2$, they
   are $12, 21,13,31,23,32$. The number
   of such arrangements is 
   $^nP_k = n(n-1)\cdots(n-k+2)(n-k+1).$ 
   Bellow is a program which when given $n,k$
   as input, prints all arragements of $k$
   items from $n$ objects.               */
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
typedef int** PermList;

int count_arrangements(int n, int k) {
  // Problem 1 a.) write a recursive 
  // function logic here in one line to 
  // compute the number of all arragements 
  // of $k$ items from $n$ objects. (2 marks)
}

PermList create_perm_list(int n, 
                                 int k) {
  int fn = count_arrangements(n, k);
  PermList pl=malloc(fn*sizeof(int *));
  for(int i =0; i < fn ;i++) {
    pl[i] = malloc(n*sizeof(int)); 
  }
  return pl;
}
void destroy_perm_list(PermList pl, 
                       int n, int k) {
  int fn = count_arrangements(n, k);
  for (int i =0; i < fn ;i++) {
    free(pl[i]); 
  }
  free(pl);
}

// given a `small_row` of size `size`
// copies it to `big_row` which has size 
// `size+1`. Also sets the last position 
// in `big_row` to `e`
void insert_and_copy(int* small_row, int size, 
                     int e, int* big_row) {
  for (int i = 0; i < size; i++) {
    big_row[i] = small_row[i];
  }
  big_row[size] = e;
}

// checks if `e` is in the `row` of size `size`
bool find(int e, int* row, int size) {
  for(int i = 0; i < size; i++) {
    if (row[i] == e) {
      return true;
    }
  }
  return false;
}
// find the numbers from $\{1,\ldots, n\}$
// that are not in `row` which is of size `k`
// and puts them in `elements`
void find_elements_not_in_row(int* row, int n, 
                              int k, 
                              int* elements) {
  int c = 0;
  for (int i = 0; i < n; i++) {
    if (find(i+1, row, k) == false) {
      elements[c++] = i+1;
    }
  }
}

PermList enumerate_arrangements(
                        int n, int k) {
  PermList B = create_perm_list(n,k);
  if (k == 1) {
    // Problem 1 b.) write code here for base 
    // case of recursively building list `B` 
    // of all arrangements of $k=1$ items 
    // from $\{1,..,n\}.$ (3 marks)
  } else { 
    // Problem 1 c.) write code here for 
    // recursively building list `B` of all
    //  arrangements of $k$ items from 
    // $\{1,..,n\}.$ (5 marks)
  }
  return B;
}
void print_perm_list(PermList pl, 
                     int n, int k) {
  int fn = count_arrangements(n, k);
  for(int i = 0; i < fn;i++) {
    for (int j =0; j <k; j++) {
      printf("%d ", pl[i][j]);
    }
    printf("\n");
  }
}

int main() {
  int n = 10;
  int k = 5;
  print_perm_list(
        enumerate_arrangements(n, k),n,k);
  return 0;
}
```


## 6. Grades
Problem given in comments. Format of input files is also given bellow the code.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef enum Grade {A,Am,B,Bm,C,Cm} Grade;

typedef struct Student {
  char email[100];
  int assigment1;
  int assigment2;
  int midsem;
  int endsem;
  Grade grade;
} Student;

typedef struct Database {
  Student students[300];
  int count_students;
} Database;

float compute_total_marks(Student s) {
/* Problem 2.1: write code here, for computing the 
total marks for a student and returning it. 
Assume that
assignment marks were out of 100, midsem marks 
were out of 50 and endsem marks were out of 80. 
The best 1 score amoung the 2 assignments will 
only be taken. The weightage for the total marks 
is 30% from assignment, 30% from midsem and 40% 
from endsem. (2 marks)
*/
}

void compute_grades(Database* db) {
/* Problem 2.2: Assume that grades are given as 
follows: >= 90: A, between 90 and 80: Am,
between 70 and 80: B, between 60 and 70: Bm,
between 50 and 60: C, between 40 and 50: Cm.
Write code here to assign grades to each 
student, and save it in the `grade` field of the
`Student`. (2 marks)
*/
}

int main(int argc, char* argv[]) {
  Database db;
  /* Problem 2.3: Suppose the a.out is run with the 
  first argument as the name of the `.csv` file. 
  For example `./a.out marks.csv`. Write code here, 
  that will read all the data from the `.csv` file 
  and populate the Database `db`.  (3 marks)
  */
    
  compute_grades(&db);
  
  /* Problem 2.4: Suppose the a.out is run with the 
  second argument as the name of the `.csv` file for 
  grades. 
  For example `./a.out marks.csv grades.csv`. 
  Write code here, open the file with name given by
  second argument, and write the grades.  (3 marks)
  */
  
}
```

### marks.csv (input file)
```
email,A1,A2,Mid,End
student1@students.iiit.ac.in ,68,72,34,56
student2@students.iiit.ac.in ,90,85,56,48
```


### grades.csv (output file)
```
email,total_marks,grade
student1@students.iiit.ac.in ,70.000000,B
student2@students.iiit.ac.in ,84.599998,A-
```

## 7. Inventory Grouping
Problem given in comments. Format of input files is also given bellow the code.
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef enum Group {
  Diary,
  Vegetables,
  Fruits
} Group;

char group_names[3][100] = {
    "diary",
    "vegetable",
    "fruit"
  };

typedef struct InventoryItem {
  char name[100];
  int quantity;
  int price;
  Group group;
} InventoryItem;

int main(int argc, char* argv[]) {

  InventoryItem inventory[100];

/* Problem 2.1: Suppose the first argument of a.out
contains the csv file of inventories, write code 
here, which reads that file and stores the data in 
the `inventory` array declared above.
*/

/* Problem 2.2: Suppose the second argument of a.out
contains the csv file which has the group name
corresponding to each inventory item, write code here,
which updates the `group` field
in each InventoryItem of the `inventory` array.
*/
 
int grouped_value[3];
/* Problem 2.3: Compute the total value of all
items in a group and store it in the correpsonding
entry of the array `grouped_value`. That is
grouped_value[0] has the total value of all
Diary items. Similarly Vegetables for 1 and Fruits for 2.
*/

/* Problem 2.4: Write down the grouped inventory values
into a file given by the third argument to a.out, in the format
specificed for `grouped_inventory.csv`.
*/

}
```
### inventory.csv (input file)

```
name,quantity,price
onion ,100,15
paneer ,50,100
tomato ,70,10
curd ,30,50
apple ,150,100
orange ,200,150
```
### group.csv (second input file)
```
item,group
curd ,diary
tomato ,vegetable
paneer ,diary
apple ,fruit
onion ,vegetable
orange ,fruit
```
### out.csv (output file)
```
group,value
diary,6500
vegetable,2200
fruit,45000
```

## 8. Checking Bipartiteness
Given an undirected graph $G=(V,E)$, it is said to be bipartite if the vertex set $V$ can be partitioned into two sets $V_1,V_2$ (such that $V_1 \cup V_2 = V$ and $V_1 \cap V_2 = \emptyset$), such that there is no edge in $E$ which has one endpoint in $V_1$ and another endpoint in $V_2$. 

Write a program, which takes a graph as input and checks if it is bipartite.


Note: Runtime of the algorithm doesnt matter, but it should output the correct answer.

## 9. Colorings of a Graph
Given an undirected graph $G=(V,E)$, a *coloring* of the graph using $\{R,G,B\}$ is an assignment of these colors for every vertex, such that there is no edge in $E$ which has the same color in both end points. See [https://en.wikipedia.org/wiki/Graph_coloring](https://en.wikipedia.org/wiki/Graph_coloring).

Write a program, which takes a graph as input and outputs a coloring of the graph with $\{R,G,B\}$ colors.


Note: Runtime of the algorithm doesnt matter, but it should output the correct answer.

## 10. Finding Satisfying Assignments for 2SAT

A Boolean formula consists of 
- Boolean variables denotes by $a,b,c, \cdots, z$ which can take values $0,1$
- not operations which flip the value  of the variable denoted by $\neg a$.
- or $||$, and $\\&$ operations.  

A *satisfying assignment* to a Boolean formula is an assignment of $0,1$ values to the variables,
such that the formula evaluates to $1$.    See [https://en.wikipedia.org/wiki/Boolean_algebra](https://en.wikipedia.org/wiki/Boolean_algebra)

For example:
$$ (\neg a||c)~\\&~(\neg a||\neg d)~\\&~(b||\neg d)~\\&~(b||\neg e)~\\&~(c||\neg e)~\\&~(\neg a||\neg f)~\\&~(b||\neg f)~\\&~(c||\neg f)~\\&~(d||g)~\\&~(e||g)~\\&~(f||g)$$
The assignment $a = 0, b = 1, c = 1, d = 1, e = 1, f = 1, g = 1$ is a satisfying assignment to the above formula, since if you make this substitution and evaluate the expression, 1 is obtained.  

Note that in the Boolean formula above, there are 11 terms in brackets, outside which there is and $\\&$ operation. Inside the bracket a variable or a negated variable is or ed $||$ with another one. Formula of this form are called 2SAT.   

Write a program which takes a 2SAT formula as input and outputs/prints a satisfying assignment to the formula.  

Note: The algorithm only needs to be correct.


## 11. Student Database

You are tasked with creating a program to manage a student database. The program should allow users to dynamically add, display, and delete student records. Each student record should include a student ID, name, and age. The program should use dynamic memory allocation for storing student records.  

**Requirements:**  

Implement a menu-based program with the following options:
- Add Student: Dynamically allocate memory for a new student record and prompt the user to enter the student's details (ID, name, and age).  
- Display Students: Display a list of all students in the database, including their details.
- Delete Student: Prompt the user to enter a Student ID and delete the corresponding student record from the database.
- Exit: Terminate the program.  

Use structures to represent a student's details. Implement dynamic memory allocation for storing student records. Use pointers to navigate and manipulate the dynamically allocated memory. Use functions to modularize the code (e.g., separate functions for adding, displaying, and deleting student records).  

Example:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure to represent a student
struct Student {
    int id;
    char name[50];
    int age;
};

// Function to add a new student
void addStudent(struct Student** database, int* numStudents) {
    // Your implementation goes here.
}

// Function to display all students
void displayStudents(struct Student* database, int numStudents) {
    // Your implementation goes here.
}

// Function to delete a student
void deleteStudent(struct Student** database, int* numStudents, int idToDelete) {
    // Your implementation goes here.
}

int main() {
    struct Student* studentDatabase = NULL;
    int numStudents = 0;
    int choice, studentIdToDelete;

    do {
        printf("\nStudent Database Management System\n");
        printf("1. Add Student\n");
        printf("2. Display Students\n");
        printf("3. Delete Student\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addStudent(&studentDatabase, &numStudents);
                break;
            case 2:
                displayStudents(studentDatabase, numStudents);
                break;
            case 3:
                printf("Enter the Student ID to delete: ");
                scanf("%d", &studentIdToDelete);
                deleteStudent(&studentDatabase, &numStudents, studentIdToDelete);
                break;
            case 4:
                printf("Exiting the program...\n");
                break;
            default:
                printf("Invalid choice. Please enter a valid option.\n");
        }

    } while (choice != 4);

    // Free dynamically allocated memory before exiting
    free(studentDatabase);

    return 0;
}
```
Feel free to modify the problem or add additional features to suit your needs.


## 12. Employee Database

You are tasked with developing a simple employee database system in C. The program should be capable of performing the following operations:  

- Add Employee:  
Prompt the user to enter the employee's details (Employee ID, Name, Position, and Salary).  
Add the employee to the database.  
 
- Display Employees:  
Display a list of all employees in the database, including their details.  
  
- Search Employee:  
Prompt the user to enter an Employee ID.  
Display the details of the employee with the given ID if found; otherwise, show a message indicating that the employee was not found.  
  
- Update Salary:  
Prompt the user to enter an Employee ID.  
If the employee is found, allow the user to update the salary for that employee.  
  
- Delete Employee:   
Prompt the user to enter an Employee ID.  
If the employee is found, remove the employee from the database.  
  
- Exit:  
Terminate the program.  
  
**Requirements:**  
- Use structures to represent an employee's details.  
- Implement dynamic memory allocation for storing employee records.  
- Use functions to modularize the code (e.g., separate functions for adding, displaying, searching, updating, and deleting employees).  
  
Example run of the program
```
Employee Database Management System

1. Add Employee
2. Display Employees
3. Search Employee
4. Update Salary
5. Delete Employee
6. Exit

Enter your choice: 1
Enter Employee ID: 101
Enter Name: John Doe
Enter Position: Software Engineer
Enter Salary: 60000

Employee added successfully!

Enter your choice: 2
Employee List:

ID    Name               Position               Salary
-----------------------------------------------------
101   John Doe           Software Engineer      60000

Enter your choice: 3
Enter Employee ID to search: 101

Employee Found!

ID    Name               Position               Salary
-----------------------------------------------------
101   John Doe           Software Engineer      60000

Enter your choice: 4
Enter Employee ID to update salary: 101
Enter new salary: 65000

Salary updated successfully!

Enter your choice: 5
Enter Employee ID to delete: 101

Employee deleted successfully!

Enter your choice: 2
Employee List: (empty)

Enter your choice: 6
Exiting the program...
```
Feel free to customize the problem as needed or add additional features for extra complexity.


## 13. Sudoku Solver

You are tasked with implementing a program that solves a Sudoku puzzle (see [https://en.wikipedia.org/wiki/Sudoku](https://en.wikipedia.org/wiki/Sudoku)). Sudoku is a number-placement puzzle where the objective is to fill a 9x9 grid with digits from 1 to 9, such that each column, each row, and each of the nine 3x3 subgrids that compose the grid (also called "boxes", "blocks", or "regions") contains all of the digits from 1 to 9.  

Your program should take a partially filled 9x9 Sudoku grid as input, where zeros represent empty cells. The goal is to fill in the empty cells such that the Sudoku puzzle is solved.  

**Requirements:**
- Implement a function solveSudoku that takes a 9x9 integer array representing the Sudoku grid and solves the puzzle in place.
- The input grid will be given as a function parameter.
- The solved Sudoku grid should be displayed as the output.  
  
Example:

```c
#include <stdio.h>

void printSudoku(int sudoku[9][9]) {
    for (int i = 0; i < 9; i++) {
        for (int j = 0; j < 9; j++) {
            printf("%d ", sudoku[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int sudoku[9][9] = {
        {5, 3, 0, 0, 7, 0, 0, 0, 0},
        {6, 0, 0, 1, 9, 5, 0, 0, 0},
        {0, 9, 8, 0, 0, 0, 0, 6, 0},
        {8, 0, 0, 0, 6, 0, 0, 0, 3},
        {4, 0, 0, 8, 0, 3, 0, 0, 1},
        {7, 0, 0, 0, 2, 0, 0, 0, 6},
        {0, 6, 0, 0, 0, 0, 2, 8, 0},
        {0, 0, 0, 4, 1, 9, 0, 0, 5},
        {0, 0, 0, 0, 8, 0, 0, 7, 9}
    };

    printf("Sudoku Puzzle:\n");
    printSudoku(sudoku);

    solveSudoku(sudoku);

    printf("\nSolved Sudoku:\n");
    printSudoku(sudoku);

    return 0;
}

```

```
Sudoku Puzzle:
5 3 0 0 7 0 0 0 0 
6 0 0 1 9 5 0 0 0 
0 9 8 0 0 0 0 6 0 
8 0 0 0 6 0 0 0 3 
4 0 0 8 0 3 0 0 1 
7 0 0 0 2 0 0 0 6 
0 6 0 0 0 0 2 8 0 
0 0 0 4 1 9 0 0 5 
0 0 0 0 8 0 0 7 9 

Solved Sudoku:
5 3 4 6 7 8 9 1 2 
6 7 2 1 9 5 3 4 8 
1 9 8 3 4 2 5 6 7 
8 5 9 7 6 1 4 2 3 
4 2 6 8 5 3 7 9 1 
7 1 3 9 2 4 8 5 6 
9 6 1 5 3 7 2 8 4 
2 8 7 4 1 9 6 3 5 
3 4 5 2 8 6 1 7 9
```


## Solutions

Problem 3 Solution: https://github.com/geevi/cpro_mon_2022/blob/main/lecs/quiz2/bank_soln.c  

Problem 5 Solution: https://github.com/geevi/cpro_mon_2022/blob/main/lecs/quiz2/arrangements_soln.c  

Problem 6 Solution: See grades.c in https://github.com/geevi/cpro_mon_2022/tree/main/lecs/end_sem  

Problem 7 Solution: see inventory_grouping_soln.c in https://github.com/geevi/cpro_mon_2022/tree/main/lecs/end_sem  
