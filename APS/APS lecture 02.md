# Algorithmic Problem Solving, Spring 2024, Lecture 2: Problem Solving Paradigms

![DALL·E 2023-02-02 10 09 19 - an abstract painting of a greedy cat on her laptop ](https://github.itu.dk/storage/user/716/files/446aba9c-7390-4be0-9467-594c9b73eef2)


### Outline

####  Complete Search / Exhaustive Search
  - Enumerating all possible answers
  - Backtracking

#### Greedy Algorithms
  - General idea
  - Examples with proof of correctness

<!--
# Exercises from last week

<https://itu.kattis.com/courses/BAPS/APS23/assignments/qsdm6c/statistics> (only visible to teachers)

-->

# Complete Search

**Setting:**

- Finite set of possible answers, want to find true/optimal answers
- Simple approach: Just try all possible answers one by one, keep track of true/optimal answers

**Running time**: Usually exponential in the number of objects.

(But if `n <= 25`, this might be a valid approach.)

**Example**: <https://itu.kattis.com/problems/geppetto>

---

## Enumerating all subsets

Let's say we want to enumerate all subsets of `{0, ..., n-1}`. 

### Using recursion

```python
def search1(subset, k, n):
  if k == n:
    # process subset
    print(subset)
  else:
    search1(subset, k + 1, n) # do not take element k in the subset
    subset.append(k)
    search1(subset, k + 1, n) # take element k in the subset
    subset.pop()

search1([], 0, n)
```

---

### Using bit representations

```python
def search2(n):
    for i in range(1 << n):
        subset = [j for j in range(n) if i & (1 << j) != 0]
        print(subset)
  
search2(n)
```

---

## Bruteforce for small input sizes

- <https://itu.kattis.com/problems/closestsums>
- <https://itu.kattis.com/problems/walls>

---

# Backtracking

n-by-n queens problem: Place `n` queens on a `n`-by-`n` chessboard such that no two queens can attack each other.
![[queens.png]]


---

## Example Problem
<https://itu.kattis.com/problems/holeynqueensbatman>  

---

# Greedy algorithms

A greedy algorithm constructs a solution by always making a local "good" choice and never backtracks. 

### Solution template
- S is the empty solution
- Order the input elements in a certain way, e.g., by "contribution to a solution" 
- Go through input elements one by one:
  - If adding current element to S is a valid solution, add it
  - Otherwise skip it
- Return S

**Running time**: Usually "O(sorting time)", i.e., `O(n log n)`. 

**Main obstacle**: Show correctness.

---

# Which greedy algorithms do you know?

---


## Proof idea

Usually want to show that the _first choice_ of the greedy algorithm is _correct_, i.e., there exists an optimal solution that would pick the same element. Then apply induction on the remaining input.

---

## Intro: Coin exchange and task scheduling

<http://www.cs.princeton.edu/~wayne/kleinberg-tardos/pdf/04GreedyAlgorithmsI.pdf>

---

## Examples

- <https://itu.kattis.com/problems/standings>
- <https://itu.kattis.com/problems/bank>

<!--
- <https://chalmerschallenge21.kattis.com/problems/chalmerschallenge21.chactl>

> Thore: I’m still not quite sure why this works; luckily I advocate proving correctness of greedy solutions only in the Fall, never in Spring. -->

---

## When greedy is not a good choice

**Input**: We are given a set of `n` objects with weights `w_i` and value `v_i` and have a max weight `W`. 

**Task**: Select a subset `I` of the objects such that the total weight is at most `W`, and the sum of `v_i` is maximized.

**Greedy**: Sort elements by `v_i/w_i` and pick them in this order as long as there is space for them.


### Bad news
This can be arbitrarily bad, for example for the `(v, w)` pairs `(1,1), (999, 1000)` and `W = 1000`.

### Good news
We get a 2-approximation if we also take into account just returning the element of largest value. 










