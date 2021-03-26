

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
    
    #### Answer : 
    >**input:**
	>* **Places** is array of structure, were first part is ***income*** (r1, r2, ... , rn) and second is ***position*** (x1, x2, ... , xn)
	>* **d** our constrain  
	>
	>**output:**
	> + Pair of
	>    *  first - **profit** is maximum possible income
	>    *  second - **positions** is array of places that satisfy the profit
	>``` c++
	>Func (Places) -> pair(profit, positions)
	>{
	>	if Places.isEmpty() :
	>		return 0
	>	t1 = Func( Places.withoutFirst() )
	>	t2 = Func( Places.withoutClosest(d) )
	>	t2.profit += Places.top().income
	>	t2.positions += Places.top().position
	>	if t1.profit > t2.profit:
	> 		return t1
	>	else:
	>		return t2
	>}
	>```
	>**explanation:**   
We divide the task into two subtasks: if we choose the first position to build a shop `t2` and if we don't `t1`. If we take it, we run the same algorithm recursively, with no positions current and closer to d positionsthan our `Places.withoutClosest(d)` . If we don't take it, we remove the first element from the array  `Places.withoutFirst()`.
	>
	
2. Provide asymptotic worst-case time complexity of the recursive algo-
    rithm.  
    #### Answer : 
    > #### The ful time complexity:
    > 
	>    1. **T(n)** = T(n-1) + T(n - d') +  c , d' >= 1, c - some constant
	>    2. **T(0)** = Θ(1)
	> #### In the worst- case `d' = 1`:
    >
	>    **T(n)** = 2*T(n-1) + c =  
	>    = 2*(2*T(n-2) + c )+ c = 4*T(n-2) + 3c =  
	>    = 4*(2*T(n-3) + c) + 3c = 8*T(n-3) + 7c =   
	>	  = 2^k^ * T(n-k) + 2^k^ c - c  
	>
	>  	**`(k = n)`** => T(n) = Θ( 2^n^ + 2^k^c) = Θ(2^n^)
			
3. Identify overlapping subproblems.

	#### Answer : 
	> #### overlapping:
	> In the process of performing recursion, it may happen that the function will be executed with the same input data that it  was previously calculated with. Since this function is pure, that is, it depends only on the input values, the program performs unnecessary work.  
	>
	> **simple example:**
	 `p={p1,p2,p3}, d = 0`
	  **1's step**  `Func({p1, p2, p3})`
  	  **2's step**  `Func({p2, p3})` and `Func({p2, p3})`
	  **3's step**  `Func({p3})`,`Func({p3})`,`Func({p3})`,`Func({p3})`
	>
    
4. Write down pseudocode for the optimized algorithm that solves the
    problem using dynamic programming (top-down or bottom-up). The
    algorithm should compute both the maximum estimated revenue **and**
    the specific locations where shopping centers should be placed.

	 #### Answer : 
    >**I\O: thee same as 2.1.1**
	>``` c++
	>Func (Places) -> pair(profit, positions)
	>{
	>	static Arr = NULL // storage of of overlapping
	>	if Places.isEmpty() :
	>		return 0
	>	if Arr[Places.size()] == NULL :
	>		t1 = Func( Places.withoutFirst() )
	>		t2 = Func( Places.withoutClosest(d) )
	>		t2.profit += Places.top().income
	>		t2.positions += Places.top().position
	>		Arr[Places.size()]  = t1 if t1.profit > t2.profit else t2
	>	return Arr[Places.size()] 
	>}
	>```
	>**explanation:**   
It works because array of places `Places` is systematically reduced from full to zero capacity. So running the function with arrays of the same size will give the same result. We store it's calculated value under the size index in `Arr`.
	>

5. Provide asymptotic worst-case time complexity of the dynamic pro-
    gramming algorithm.
    
	 #### Answer : 
    > The **worst-case** occurs when recursion reduces the size of the array by only one with each step (as shown in the picture).
    >![image](https://user-images.githubusercontent.com/47717531/112659291-470ff000-8e65-11eb-9acb-7bb0021ee771.png)
    > The time complexity can be computed by a tree. I have illustrated the schematic approach. At each step, two subproblems are run, of which only one is actually calculated. hence, the **worst-case** time complexity is Θ(n)
    

### 2.2 Sorting


1. Briefly explain how insertion sort works.  
	#### Answer : 
	>## Insert sorting is one of the sorting algorithms.
	>- An empty additional array is created, where new elements will be added.
	>- When adding a new element, the program sequentially iterates through the existing sorted sequence until it finds a place that satisfies the condition.
	>- And so all the elements from the original array are inserted into this array, thereby sorting it.
	> ## Insertion sort properties
	> -   adaptive (performance adapts to the initial order of elements);
	> -   stable (insertion sort retains relative order of the same elements);
	> -   in-place (requires constant amount of additional space);
	> -   online (new elements can be added during the sort).
2. Prove that the worst and the best case running times of insertion sort
    are Θ( _n_^2^ ) and Θ( _n_ ), respectively.  
    
   	#### Answer : 
	> **Adding a one element** takes **Θ (n)** at *worst* and **Θ (1)** at *best* *case*.   
	> **Prove**: If the array is sorted in ascending order and we add the largest element to the beginning, we need to make `n`checks to push it to the end. When adding the smallest element to the beginning, we compare it only with the first element and immediately insert it, respectively, only one check occurred.  
	> **Adding a `n` elements** takes **Θ (n^2^)** at *worst* and **Θ (n)** at *best* *case*.   
	> ___
	> Provided that the insertion in any place is free, as in the list.
	
3. What is a _k_ -sorted array? Is insertion sort fast or slow, relative to its
    worst-case, when applied to a _k_ -sorted array? Justify your answer by
    computing the running time of insertion sort for a _k_ -sorted array.

 	#### Answer : 
	> • A k-sorted array is an array whose elements are no further than k positions from their target position in the sorted array.   
	> • Insertion sort in the worst-case for a k-sorted array will take less time, because finding a place for each new element will not be more than k, otherwise the element will be further than k from the original position, so inserting n elements will take  time.   

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

#### Answer :    
>	**input:**  
>* **array** is array of data that will be sorted  
>* **compFunc** is a comparison function  
>**output:**  
>* sorted array  
>  
>``` c++  
>insertSort (array, compFunc) {
>	tmpArr = { array.at(0) }
>	for i = 1 to array.size() : 
> 		tmpArr.push_pack( array.at(i) )
>		for j = tmpArr.Size()-1 downto i :
>			if compFunc(tmpArr.at(j-1) , tmpArr.at(j)) :
>				break
>			else:
>				swap(tmpArr.at(j-1) , tmpArr.at(j))
> 	return tmpArr 
>}
>```
>
>**input:**
>* **left** and **right** is the user's elements from table above
>**output:**
>* logical answer of operator less than 
>
>```c++
>myCompFunc (left , right) {
>	if left.code != left.code:
>		return left.code < left.code
>	if left.date_start != left.date_start:
>		return left.date_start < left.date_start
>	if left.date_end != left.date_end:
>		return left.date_end < left.date_end
>	if left.sponsor != left.sponsor:
>		return left.sponsor < left.sponsor
>	... // by description and etc.
>}
>```
>

5. Write two versions, one recursive, the other iterative, of a boolean
    function named **belongs** which takes as arguments an array **A** of ordered
    integers, a start index **from**, an end index **to** and an integer **x** to search
    for and which returns **true** if **x** is in the array **A** between index **from**
    and index **to**, and **false** otherwise.
    
    #### Answer : 
    
	>## Iterative:  
	>
	>``` c++
	>belongs(array, from, to, x){
	>	while True : // waiting for an interruption.
	>		middle = (from + to)/2
	>		if array[middle] == x:
	>			return True
	>		if from == to :
	>			return False
	>		if array[middle] < x:
	>			from = middle
	>		if array[middle] > x:
	>			to = middle
	>}
	>```
	>
	>## Recursive:  
	>
	>``` c++
	>belongs(array, from, to, x){
	>		middle = (from + to)/2
	>		if array[middle] == x :
	>			return True
	>		if from == to :
	>			return False
	>		if array[middle] < x:
	>			return = belongs(array, middle, to, x)
	>		if array[middle] > x:
	>			return = belongs(array, from, middle, x)
	>}
	>```
	>

6. Write a variant of the previous function called search which takes the
    same arguments as belongs, and which returns the indexi of the cell
    containing x if x appears in the array A between the index from and
    the index to and null otherwise.  
      
     #### Answer : 
    
	>## Recursive:  
	>
	>``` c++
	>search(array, from, to, x){
	>		middle = (from + to)/2
	>		if array[middle] == x :
	>			return middle
	>		if from == to :
	>			return NULL
	>		if array[middle] < x:
	>			return = belongs(array, middle, to, x)
	>		if array[middle] > x:
	>			return = belongs(array, from, middle, x)
	>}
	>```
	>
	
7. Establish the recurrence relation for the running time ofsearchand
    determine the time complexity by applying Master Theorem.
     #### Answer : 
    
	>## Time complexity:  
	>`T(n) = T(n/2) + c` , were n - amount of elements between from and to; c - some constant
	>### Master Theorem:  
	> ```
	>1. a = 1, b = 2, f(n) = Θ (1) = Θ(n^0^log^0^n) 
	>2. C = 0, k = 0, Ccrit = log(a)/log(b) = 0
	>```
	>##### Case *II*: `C == Ccrit`
	>`T(n) = Θ(log(n))` 
	>
	
8. Explain the benefit of using search in the context of insertion sorting.
    Give a version of insertion sorting usingsearch. How does it affect the
    time complexity of insertion sort?
    
	#### Answer : 
    
	>## Benefits:    
	>Because you can use a binary search to find the place where the element will insert.  
	>The main advantage is that you can split the sorting into two independent modules: search and paste. Modularity is always excellent.  
	>## Implementation:    
	>``` c++
	>upper_bound(array, from, to, x){ // asymptotic time O(log(n))
	>		middle = (from + to)/2
	>		if array[middle] == x :
	>			return middle
	>		if from == to :
	>			return to + 1 if x > array[to] else to
	>		if array[middle] < x:
	>			return = belongs(array, middle, to, x)
	>		if array[middle] > x:
	>			return = belongs(array, from, middle, x)
	>}
	>```
	>
	>``` c++
	>insert(array, place, element){ // asymptotic time O(n)
	>		array.push_back(element)
	>		for i = array.size() - 1 downto place :
	>			swap(array.at(i -1), array.at(i))
	>}
	>```
	>
	>``` c++
	>insertionSort(array){ // asymptotic time O(n^2^)
	>		for i = 0 to array.size() :				// n times
	>			element = array.at(i)
	>			pos = upper_bound(array, 0,  i-1, element) // O(log(n))
	>			insert (array, pos, element)							// O(n)
	>}
	>```
	>## How does it affect?
	>The asymptotic complexity will not decrease, because the shift of the elements will be n times in O (n)
	>
	
9. Is Bubble Sort difficult to parallelize? Why? Provide pseudocode (and
    explain) a parallel version of bubble sort.
#### Answer : 
>
>### Standart Bubble sort:
>``` c++
>bubbleSort (array) {
>	for i=array.size()-1 downto 0:
>		for j=0 to i :
>			if array[j] > array[j+1] :
>				swap(array[j], array[j+1])
>}
>```
> In this case it is almost impossible to parallelize the program, because it is straightforward and depends on previous actions.
> ### To parallelize, use odd-even bubble sorting
> ``` c++
> OddEvenBubble(array){
>	for i=1 to n :
>		for (j=1-i%2; j<n-1; j+=2)
>			if array[j] > array[j+1]:
>				swap(array[j],array[j+1]) 
>	}
> ```
> ![image](https://user-images.githubusercontent.com/47717531/112681790-3f117980-8e80-11eb-8753-fa5ef02667e3.png)
> The picture above perfectly illustrates how this program works.
> The sequential complexity of this program is preserved because each phase of the algorithm (odd or even) requires comparison.
> Now this code can be parallelized.
> 
> ###  Parallel  odd-even bubble sort:
> ``` c++
> ParallelOddEvenBubble (array, num_proc){
>	id = GetProcId();// process number
>	for(i=0; i< num_proc;i++){
>		if( i%2 == id%2)
>			compare_exchange_min(id+1)
>		else 
>			compare_exchange_max(id-1)
>	}
>```

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
	> ``` c++
	>		List : 1, 2, 3, 5, 8, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70
	> ```
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
