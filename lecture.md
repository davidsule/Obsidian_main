# Algorithmic Problem Solving, Spring 2024, Lecture 1

## Welcome!

---

## Who are we?

- Martin Aumüller (maau@itu.dk) 
- Riko Jacob (rikj@itu.dk)
- Alexander Theodor Bilde Pedersen (altp@itu.dk)
- Simon Martin Breum (smbr@itu.dk)

## Who are you?


---

## Main Resources
 * Material: https://github.itu.dk/algorithms/aps-24
 * Assignments/Project submission: https://learnit.itu.dk/course/view.php?id=3022875

## Material
* [AL] Antti Laaksonen, Competitive Programmer's Handbook, https://cses.fi/book/book.pdf
* [AFLV] Bjarki Gudmundsson, T-414-AFLV: A competitive programming course, https://github.com/SuprDewd/T-414-AFLV
* [CJ] Christoph Dürr, Jill-Jenn Vie, Competitive Programming in Python, Chapters made available

---

## Intended Learning Outcomes
After completing this course, the student is able to

- **Explain, choose and make use** of a wide range of algorithmic problem solving techniques
- **Implement** an algorithmic solution to a computational problem
- **Design** a computational problem, including a problem description, implemented accepted and wrong solutions, and design of test cases
- **Test** the correctness and empirical running time of an implementation by generating appropriate test cases


---

# Weekly activities
- First 10 weeks, lectures 14:15-15:45 (Aud 3), exercises 16:00-17:45 (2A52), 2A20 also available in exercise hours, if you want some quiet. 

## Preliminary Plan
| Week | Description | Material | Lecturer | Exercises | 
|:------|-------------|:----------:|:----------:| :-----: |
| 1, Jan 31 | Introduction, Basic Algorithms and Data Structures | - | Martin | [Kattis](https://itu.kattis.com/courses/BAPS/APS24/assignments/zr5cjv)|
| 2, Feb 07 |  Problem Solving Paradigms | [AL 5-6], Optional: [AFLV 4] | Martin | -  |
| 3, Feb 14 | Dynamic Programming | [AL 7], Optional: [ AFLV 6] | Martin | -  | 
| 4, Feb 21 |  Problem Design in Kattis |  | Thore | - |
| 5, Feb 28 | Graph Algorithms | [AL 11, 12, 16], Optional: [AFLV 7-8] | Riko | -  |
| 6, Mar 06 | Network Flow | [AL 20] | Riko | - |
| 7, Mar 13 | Geometric Algorithms | [AL 29-30] | Riko | - |
| 8, Mar 20  | Algorithms on Arrays |  [AL 9], [AL 27 'Square Root Alg'], [AL 28, top-bottom], Python examples:  [[CJ, 4]](https://github.itu.dk/algorithms/aps-24/blob/master/book_chapters/cp_in_python_chapter_4.pdf) | Riko | - |
| 9, Apr 03 | String Algorithms | [AL 26 'tries', 'string hashing'] | Martin | - |
| 10, Apr 10 | Randomized Algorithms & Project kick-off | - | Martin | - | 

**Intended Workflow:** Prepare for the lecture &rarr; go to the lecture &rarr; start solving exercises in exercise session &rarr; solve more at home :-)

---

## Time expectations

- 7.5 ECTS -> 11.5 hours workload/week
- Lecture + Exercises = 4 hours
- Almost one day for preparing/recap of lecture, solving exercises

---

## Exercises
- One kattis session per week (first week: many easy, one/two non-trivial)
  - Straight-forward application tasks
  - Some other harder examples that require additional thinking
- Requirement: Solve two (out of 6-9) per week
  - One will always be part of the lecture
- Suggestion:
  - You solve the problems yourself (individually), group work encouraged
  - You should not expect to solve all exercises each week. 
  - Suggestion: Read the problem, figure out how to apply the technique, think about test cases
- Not a valuable learning experience: you see us solving the problem 

---

## What this course is about

- Deepen algorithmic repertoire 
- Learn how to approach more difficult computational problems than those accessible with algorithms & data structure knowledge
- See more connections between implementation and running time
- Being able to generate difficult inputs

---

## What this course is **not** about

- Learning C++ (but if you want to do it: Please do!)
- Training core elements of competitive programming
  - Programming under stress
  - Fast typing, knowing all details of the programming language
  - Working in a team with different roles

---

## Project

Two parts:

1. Create one or multiple well-defined programming exercises, including test cases for automatic solution checking. This includes 
  - (i) defining an algorithmic problem, 
  - (ii) writing a problem description, and 
  - (iii) generating intended solutions and test cases. 
  Supervisors helps with (i).
2. Solve one or multiple programming exercises from a pre-defined selection. These exercises will be selected in coordination with the supervisor. Document choice of algorithmic techniques in a report.

---

## Exam

Report followed up by an oral exam, 7-scale grade.

Report focuses on _solving problems_ and _designing problems_. 

Oral Exam: Short (group) discussion, followed up by an individual part about course content. 

---
# Short recap of Algorithms and Data Structures 

---

## Data Structures You Have Seen 

Data structures and types in Java and Python

- Arrays: _int[]_ - _List_
- Lists: _ArrayList, LinkedList_ - _List, Deque_
- Sets: _TreeSet, HashSet_ - _Set_
- Maps: _TreeMap, HashMap_ - _Dict_
- PQs: _PriorityQueue_ - _heapq_
- Graphs: _HashMap_ - _Dict_
- (Balanced) Binary Search Tree: _???_

---

## Algorithms you have seen 

- Stacks & Queues 
- Searching & Sorting
- Algorithms for Strings (Tries)
- Graph Traversal, Shortest Path, MST, Union-Find

---

## Running time complexity
- Important: You have an overall idea of running time complexity
- We won't see much analysis in the course, it's more about ideas
- We will discuss how to rule out approaches because they can obviously not be done in time

---

<!--
## An Example Problem

- **Problem Description**: 

- **Input Description**:

- **Output Description**:

--- 


## Quickly Identify Problems

### Overview of Problem Categories

Rate of appearance of different problem types in recent ICPC Asia Regional problem sets

| Category | Sub Category | Count |
|:-------:|:-----------|:----:|
| Ad Hoc | Straightforward | 1-2 |
| Ad Hoc | Simulation | 0-1 |
| Complete Search | Iterative | 0-1 |
| Complete Search | Backtracking | 0-1 |
| Divide and Conquer |- | 0-1 |
| Greedy | Classic | 0 |
| Greedy | Original | 1 |
| Dynamic Programming | Classic | 0 |
| Dynamic Programming | Original | 1-3 |
| Graph |  | 1-2 |
| Mathematics |  | 1-2 |
| String Processing |  | 1 |
| Computational Geometry |  | 1 |
| Harder Problems |  | 0-1 |

Source: Lecture 1, <https://github.com/SuprDewd/T-414-AFLV>

---
-->

## Quickly Estimate Running Time

- Rough estimate: 100 million - 1 billion operations per second (10<sup>8</sup> - 10<sup>9</sup>)

- We can rule out algorithms based on input size.

- e.g., problem boils down to sorting the input. How long could we use an $O(n^2)$ algorithm?

---

## Problems Solved in Class

**Approach:**

- Discuss the problems in groups
- Input generation
- Solving the problem 

**Problems:**
- https://itu.kattis.com/problems/grandpabernie (nice combination of basic primitives)
- https://itu.kattis.com/problems/froshweek (nice "extending the algorithm")


<!--
## Thoughts from the lecture

For both problem mentioned above, we shortly discussed the problem and designed a basic solution. 

For *grandpabernie*, an obvious solution is to store the *n* visits to countries in a single list and sort that list by year.
For a query, iterate through the list until the *k*th occurrence of a country is found.
For *q* queries, this leads to a running time of *O(q n)*. 
Since both variables are at most 100,000, the worst case running time is in the order of 10^10 and thus prohibitively large.

For *froshweek* we noticed that we could simulate bubblesort or insertionsort and count the number of swaps carried out.
This takes *O(n^2)* time for *n* elements, and is thus too slow for inputs of a size of up to 1,000,000 elements. 

At the end of the class, we coded a solution for grandpabernie which can be found under `code/grandpa.py`.

-->
