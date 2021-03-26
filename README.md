

# Data Structures and Algorithms
> Spring 2021
> Assignment No **2**
> ### made by Voronov Artem


## Contents

**1 About this homework 2**  
1.1 Submission............................ 2  
  
**2 Theoretical part 3**  
2.1 Dynamic programming...................... 3  
2.2 Sorting............................... 4  
2.3 Balanced Binary Search Trees.................. 5  
2.4 Binary Heap............................ 6  


## 1 About this homework

This homework assignment only has theoretical exercises.

```
Solutions to theoretical exercises have to be elaborate and clear. Write
all solutions in a single document, then save or compile it as a PDF for
submitting.
```
#### Do not forget to include your name in the document!

### 1.1 Submission

You are required to submit your solutions to all parts via Moodle.

```
For this assignment you will need to submit:
```
- a PDF file with solutions for theoretical parts.


> Submit a single file with your name and group number. For example, if your
> name is _Ivanov Ivan_ and your group is _BS20-05_ then your file should be
> named **BS20-05_Ivanov_Ivan.pdf**.


## 2 Theoretical part

### 2.1 Dynamic programming

Two cities A and B are connected by a highway. Your task is to place shopping
centers along the highway in an efficient way, maximizing estimated revenue.
Possible locations of shopping centers along the highway are given by _N_
numbers _x_ 1 _, x_ 2 _,... , xN_. Each number specifies the number of kilometers from
city A to that location on a highway. For each position _xi_ we also know in
advance the estimated revenue _ri_ that we get if we place a shopping center
there. There is a restriction that no two shopping centers can be placed
within _d_ kilometers of each other. The highway length is _H_ kilometers and
we have 0 _< x_ 1 _< x_ 2 _<... < xn< H_.

```
For example, if we have 3 locations x 1 = 5 , x 2 = 10 , x 3 = 14 , x 4 = 15with
estimated revenue r 1 = 80 , r 2 = 150 , r 3 = 60 , r 4 = 75and d = 6then the
maximum revenue is 155 when we place two shopping center at locations
x 1 = 80 , x 4 = 15.
```
```
Describe a general algorithm for any number N of available locations, any
length of the highway H :
```
1. Write down pseudocode for a recursive algorithm that solves the prob-
    lem.
2. Provide asymptotic worst-case time complexity of the recursive algo-
    rithm.
3. Identify overlapping subproblems.
4. Write down pseudocode for the optimized algorithm that solves the
    problem using dynamic programming (top-down or bottom-up). The
    algorithm should compute both the maximum estimated revenue **and**
    the specific locations where shopping centers should be placed.
5. Provide asymptotic worst-case time complexity of the dynamic pro-
    gramming algorithm.


### 2.2 Sorting


1. Briefly explain how insertion sort works.
2. Prove that the worst and the best case running times of insertion sort
    are Θ( _n_^2 ) and Θ( _n_ ), respectively.
3. What is a _k_ -sorted array? Is insertion sort fast or slow, relative to its
    worst-case, when applied to a _k_ -sorted array? Justify your answer by
    computing the running time of insertion sort for a _k_ -sorted array.
4. Implement a comparison-based sorting algorithm to sort the following
    table of data, containing information on events (code, start_date,
    end_date,sponsor,description). Given thecodeas the key, provide
    a pseudocode for comparing two keys that will be used in your sorting
    algorithm.
   
| code | date_start |  date_end  | sponsor | description |
| ---- |:----------:| ----------:|--------:|------------:|
| A001 | 20-03-2021 | 27-03-2021 | IU      | ...         |
| A123 | 20-04-2021 | 20-05-2021 | DS      | ...         |
| B001 | 10-04-2021 | 17-04-2021 | MTS     | ...         |
| A009 | 12-04-2021 | 15-04-2021 | GTK     | ...         |


5. Write two versions, one recursive, the other iterative, of a boolean
    function namedbelongswhich takes as arguments an arrayAof ordered
    integers, a start indexfrom, an end indextoand an integerxto search
    for and which returnstrueifxis in the arrayAbetween indexfrom
    and indexto, andfalseotherwise.
6. Write a variant of the previous function calledsearchwhich takes the
    same arguments asbelongs, and which returns the indexiof the cell
    containingxifxappears in the arrayAbetween the indexfromand
    the indextoandnullotherwise.
7. Establish the recurrence relation for the running time ofsearchand
    determine the time complexity by applying Master Theorem.
8. Explain the benefit of usingsearchin the context of insertion sorting.
    Give a version of insertion sorting usingsearch. How does it affect the
    time complexity of insertion sort?
9. Is Bubble Sort difficult to parallelize? Why? Provide pseudocode (and
    explain) a parallel version of bubble sort.


### 2.3 Balanced Binary Search Trees

Consider the following sequence of numbers:

```
25 , 60 , 35 , 10 , 5 , 20 , 65 , 45 , 70 , 40 , 50 , 55 , 30 , 15
```
1. Explain in words the properties of AVL trees.
2. Explain in words or in pseudocodeinsertoperation for AVL trees.
3. Considering the following tree as the initial state of the tree, construct
    the AVL tree by adding values in the order of the sequence above.
    Particular attention should be paid to explaining the reasoning.
    
![image](https://user-images.githubusercontent.com/47717531/112558655-4b45fa00-8de0-11eb-825e-9b5b66242b50.png)



```
Figure 1: Initial AVL tree for insertion.
```
4. List values at the nodes of the tree by in-order traversal of the tree. 
	What property does resulting sequence have? Is this always the case?
	#### Answer : 
	>  ``` c++
	>		List : 1, 2, 3, 5, 8, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70
	>```
	>a. **property:** this list is sorted.  
	>b. Yes, it is the main idea of  AVL tree.  
6. Starting with the same initial tree, construct a 2-3 tree by inserting
    values in the order of the sequence above.
   	#### Answer : 
	>  ![image](https://user-images.githubusercontent.com/47717531/112561025-69622900-8de5-11eb-91dc-28593f0d39a4.png)

7. Explain in words or in pseudocode *delete* operation for AVL trees.
8. Give the trees obtained by deleting 45 and then 30 in the tree below.

![image](https://user-images.githubusercontent.com/47717531/112557565-ce198580-8ddd-11eb-8a00-6af5f5d0ed0c.png)

```
Figure 2: Initial AVL tree for deletion.
```

### 2.4 Binary Heap

```
Using two binary heaps describe a way to efficiently keep track of median^1
values. That is, describe a data structure that is based on two heaps and
provides the following methods:
```
1. insert(k)— insert value;
2. remove_median()— remove median value and return it;
3. size() — return the size of the data structure (number of stored
    values);
4. isEmpty()— check if the structure is empty (no values).

Write down pseudo code for these methods, using the interface of the binary
heap and provide worst-case time complexity for each method.
___
> ###### (^1) median values are those in the middle of the sorted sequence of values. For example,
> ###### 5 is median in 1, 2, 5, 100, 254. When number of elements is even, we have two median
> ###### values and the algorithm can return either one.
