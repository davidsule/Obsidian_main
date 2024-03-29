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

## (a)

**Solution:** `0 397`
**Process overview**:
1. I used `objdump` to disassemble the binary (I also dumped the symbol table, the strings, and used the disassemble all option but these were not utilized for this phase)
2. I used `gdb` to inspect how the `phase_3` function works. First, I enabled logging and used `disas` to disassemble `phase_3` to get and save the disassembled function with the memory addresses matching the ones used in gdb, then disabled logging, to avoid saving anything further in the file.
3. I ran `gdb` with the text file containing the solutions for phase 1 & 2 (`gdb --args bomb solutions.txt`) so those don't need to be entered again.
4. I set breakpoints to `explode_bomb` and `phase_3`, to avoid detonation and to stop execution at the beginning of the function.
5. I initially entered arbitrary, simple, but distinctive values as guesses, so their values are easily recognized during debugging
6. I stepped through the instructions, inspecting registers and memory addresses as necessary.

**Solution logic:** (Line identifiers refer to the memory offset of the instruction from the first instruction of `phase_3`, found in 'gdb.txt'.)
1. <+0> to <+17> decrements the stack pointer to allocate the necessary space on the stack for the function then sets up the canary and saves its value on the stack, it has no bearing on the solution logic.
2. <+22> zeros out %eax.
3. <+24> to <+32> loads values into registers used as arguments for called functions (and indeed one is called at <+39>), so I inspected the register values and the memory addresses from which they were loaded. It was not immediately clear what the values were but I suspected that <+39> will load the inputs somehow, as there are comparisons happening after.
4. Indeed, after the function execution (%rsp) and 4(%rsp) contain the first two input values (when delimited by space) but subsequent input values do not appear. I inspected these addresses for two reasons: These were used in <+24> to <+32> and because the stack contains local variables. With strings this point wasn't obvious at first but since I tried both I could come to this conclusion. Later, line <+49> (`cmpl   $0x7,(%rsp)`) and <+53> (`ja     0x55555555678e <phase_3+213>`) made it obvious that the input must be numeric, as values from strings will always satisfy `ja` and the destination address is a call to `explode_bomb`.
5. We also know from <+49> that the first input must be between 0 and 7 (inclusive)
6. In case there was only one input given <+47> will take the jump to a call to `explode_bomb` because of `<+44>:	cmp    $0x1,%eax`, so we know that 2 arguments must be given (as any third argument will never be used).
7. <+59> to <+76> uses the first input to compute an address to jump to instructions in the range from <+164> to <+218>, where %eax is zerod out and a jump is performed to instructions in the range from <+86> to <+121>, which are a series of add and subtract operations (different immediate values added to / subtracted from $eax).
8. We then know that our first input will determine which operation we jump to, therefore determine the value in $eax at the end of the add/subtract sequence.
9. Lines <+126> and <+130> make it clear that the first input must actually be between 0 and 5 (inclusive).
10. From <+132> and <+136> we can see that the end result of $eax must match our second input. From this we can calculate evaluate what values $eax takes with different first inputs from 0 to 5 (or write up an equation and solve it).
11. From <+143> there is only a canary check left and if that's ok, then the function returns and the phase is solved. (It's important to note that there is no alternative way to end up at the ret instruction than the one described above.)
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

![[osc_exam_ass.png]]

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


# i/o

## (a)

When a program reads from a file on disk in Linux, which of the following events occurs as a result? Pick all that apply..

b. The program executes the INT (aka. SYSCALL) instruction.
c. The kernel performs a context switch.
e. The disk interrupts the CPU when the transfer is complete.

## (b)

Otherwise data may still reside in buffers which haven’t been flushed.

# concurrency

## (a)

3, 9, 12, 15
## (b)

k & s

# misc

## (a)

Not all functions are referrentially transparent

## (b)

**P2 reads in the value 0x00000020 had before P1 overwrote it with 1s (P2 does not have access to P1’s address space).**
**P2 reads in the contents of the physical page that 0x00000020 maps to in its own address space.**
**P2 experiences a segmentation fault.**

## (c)

An interrupt forces the processor to context-switch to the kernel at regular intervals.

## (d)

**By utilizing a special instruction modifier that locks the memory bus.**

## (e)

**A unified API for doing I/O on all kinds of resources.**


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