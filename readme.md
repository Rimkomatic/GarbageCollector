# Simple Garbage Collector in C

This project is an implementation of a simple garbage collector in C.

## Overview

Garbage collection is a form of automatic memory management that aims to reclaim memory occupied by objects that are no longer in use by the program. This project demonstrates a basic garbage collection system using the mark-and-sweep algorithm.

## Key Components

### 1. Memory Management
The garbage collector manages a pool of memory blocks. These blocks are dynamically allocated as needed and freed when they are no longer reachable.

### 2. Mark-and-Sweep Algorithm
The algorithm operates in two phases:
- **Mark Phase**: Traverse the graph of references starting from the root and mark all reachable objects.
- **Sweep Phase**: Scan through all objects and free those that are not marked.

### 3. Object Representation
Each object managed by the garbage collector contains metadata including:
- A mark bit indicating whether the object is reachable.
- A size field specifying the size of the object.
- A pointer to the next object in the list.

## Implementation Details

### Memory Pool
The memory pool is a contiguous block of memory from which objects are allocated. The pool is initialized once and objects are allocated from it until it is exhausted.

### Allocation
Objects are allocated from the memory pool using a simple bump-pointer allocator. If the pool is exhausted, the garbage collector is invoked to free up memory.

### Collection
The collection process involves:
1. **Marking**: Start from the roots (global variables, stack variables) and recursively mark all reachable objects.
2. **Sweeping**: Traverse the memory pool and free all unmarked objects, adding their memory back to the pool.

## Example Usage

```c
#include "gc.h"

int main() {
    gc_init(); // Initialize the garbage collector

    // Allocate some objects
    Object *obj1 = gc_alloc(sizeof(Object));
    Object *obj2 = gc_alloc(sizeof(Object));

    // Set up references
    obj1->ref = obj2;

    // Manually invoke garbage collection
    gc_collect();

    gc_shutdown(); // Clean up and free all allocated memory
    return 0;
}

```

## Building and Running

To build and run the project, use the following commands:
``` bash
gcc -o gc_example gc_example.c gc.c
./gc_example
```


## License
This project is licensed under the MIT License.

