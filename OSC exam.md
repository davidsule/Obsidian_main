# clab

## (a)

The members (variables) of the `queue_t` struct to which `malloc` returns a pointer (given the allocation was successful and after casting to `queue_t *`) need to be correctly initialized. `malloc` does not initialize the allocated memory, therefore no assumptions can be made about the values stored there and so dereferencing the `head` or `tail` members (type `list_ele *`) of the `queue_t` struct might trigger a segmentation fault or lead to unexpected behavior depending on the garbage values. Similarly, `size` is not guaranteed to be correct (0).

In the second hint, the insert to head completed successfully, as the initial `head` (garbage value) got assigned as the `next` of the new list element (“hello_world”) and the pointer to this list element will be assigned as the new `head`. The reverse operation triggers a segmentation fault when the function implementing it (`queue_reverse`) tries to access the memory address corresponding to the garbage value mentioned.

As a fix one can use the following implementation:

```C
/**
* @brief Allocates a new queue
* @return The new queue, or NULL if memory allocation failed
*/
queue_t *queue_new(void) {
	queue_t *q = malloc(sizeof(queue_t));
	if (!q) {
		printf("Memory allocation failed!\n");
		return NULL;
	}
	q->head = NULL;
	q->tail = NULL;
	q->size = 0;
	return q;
}
```

Here, the void pointer returned by `malloc` is explicitly cast to `queue_t *`, then `head` and `tail` are initialized as null pointers and `size` to 0. `NULL` is still returned if the allocation fails.

## (b)

The implementation:

```C
/**
* @brief Frees all memory used by a queue
* @param[in] q The queue to free
*/
void queue_free(queue_t *q) {
	if (!q) {
		printf("Queue is NULL!\n");
		return;
	}
	list_ele_t *current = q->head;
	list_ele_t *tmp = NULL;
	while (current) {
		tmp = current;
		current = current->next;
		free(tmp->value);
		free(tmp);
	}
	/* Free queue structure */
	free(q);
}
```

We need to free every memory segment that was dynamically allocated (in this implementation only `malloc` was used). These were:
- the strings the list elements have contain a pointer to,
- the list elements,
- the queue itself.

First, in the `if` block, I test if `q` is not a null pointer, in which case there is nothing to free and the rest of the function would fail. Then, I iterate through the queue, freeing the memory allocated to the string for each list element, then the element itself. This is done the following way:
- I declare a variable `current` that's a pointer to the list element whose `value` member needs to be freed in the current iteration (more accurately the string pointed to by `value`) and initialize it to the first element of the queue (`q->head`).
- I declare a temporary variable `tmp` of type `list_ele_t *` whose role will be described below and initialize it to `NULL`.
- I iterate through the queue using a while loop. In each iteration I free the current element and its string and make `current` point to the next element. Since the `next` pointer of the tail (last element) is NULL and I use `current` as the condition for the while loop, it terminates after the tail is freed. The body of the loop has the following logic:
	- Make `tmp` equal to `current`, so I can make `current` point to the next element while still being able to free the list element itself.
	- Free the value (string) of `tmp`.
	- Free `tmp` itself.
	- (After the tail, `current` will be a null pointer in which case the while loop terminates.)
- Lastly, I free `q` (the queue).

Notice that we always pass the pointer returned by `malloc` to `free` (but cast to the type of pointer it's used for).

# asmlab

# logic

## (a)

All except **A&B&C**

## (b)

All except **A=1, B=1, C=0, Q=0**

# assembly

```
	irmovq $D, %rdi # instruction nr. 0
	irmovq $S, %rsi # instruction nr. 1
	irmovq two, %rax # instruction nr. 2
	mrmovq 0(%rax), %rax # instruction nr. 3
main:
	addq %rdi, %rax # instruction nr. 4
	addq %rax, %rax # instruction nr. 5
	subq %rdi, %rsi # instruction nr. 6
	je done # instruction nr. 7
	jmp main # instruction nr. 8
done:
	irmovq $0, %rdi # instruction nr. 9
	halt # instruction nr. A
two:
	.quad 0x000000000002
```

## (a)

1. 30
2. 44
3. undefined

## (b)

# locality

## (a)

- **src**: spatial
- **dst**: neither
- **i**: temporal

## (b)

- `i=0`: neither
- `j++`: temporal
- **inner loop body**: both

# caching

## (a)

Capacity miss

## (b)

… a read from an address gives you its most up-to-date value.

# memory

## (a)

The process attempted to access a region of memory which it is not privileged to access.

## (b)

everything but backwards compatibility (although I'm only 100% sure about simplifies access)



# Notes

## Q19

5Q on PDF, 4Q on Quiz (excluded from grading)

## Q15

High miss penalty / High miss rate - doesn't matter

## Q4

In question 4, what exactly do you mean by "demonstrate the benefit"? Are you saying I should implement multithreading for the SIMD part of my prflab, it I believe that part to be a "How"? That seems a bit excessive, so if not, what is a valid demonstration?"Would vectorization benefit rotate_t ? How, or why not?  
Would multithreading benefit blend_v ? How, or why not?  
Hint: What is it about the problem that makes this (not) beneficial? For a "why not", give a solid argument. For a "how", demonstrate the benefit." (edited)

Answer
 for a "How?" answer to the `blend_v` part, implementing multithreading and running the driver would indeed be the ideal way to demonstrate the benefit. It is not excessive; you have already done multithreading (`rotate_t`); now you just need to divide the blend-task into subproblems.

## Q24
For question 24:  
The first question states P2 does not have access to P1s address space, does this apply to other possible answers or just that single answer?[

![[osc_exam.png]]

It applies only to that answer