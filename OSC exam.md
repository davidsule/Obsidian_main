# Clab

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

