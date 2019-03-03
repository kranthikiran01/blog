## Golang Array and slices

Findings/Learnings from golang, post#1

Unlike c/c++ where arrays are pointers and Java, where arrays are object references in heap/stack, in Go, arrays are values. That implies, array assignments involve copying of array value to the assignee, and arrays passed in functions are copy values and not references or pointers.

This has an important implication, the array operations are expensive and when the arrays are huge, the computation becomes challenging.

So, golang has come up with a concept called Slices, which is a slice of an array. But, slices are not values, they are reference types, they are cheap to assign, and function passing is not costlier without having to create a copy.
