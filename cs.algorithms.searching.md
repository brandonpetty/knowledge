# Searching Algorithms

Searching Algorithms are designed to check for an element or retrieve an element from any data structure where it is stored.

## Linear Search

`Use when the list is unsorted and/or small.`

A linear search or sequential search is a method for finding an element within a list. It sequentially checks each element of the list until a match is found or the whole list has been searched.

Search for the target element in the list in sequential order one by one from the first element of the list to last.

__Best Case:__ Target Value is at the first position of the list  
__Worst Case:__ Target Value is the last position of the list

## Binary Search

`Use when the list is sorted and/or big.`

A binary search, also known as half-interval search, logarithmic search, or binary chop, is a search algorithm that finds the position of a target value within a sorted array. Binary search compares the target value to the middle element of the array. If they are not equal, the half in which the target cannot lie is eliminated and the search continues on the remaining half, again taking the middle element to compare to the target value.

In Binary Search, the list must be in some sorted order. Searching the target value by picking the value from the middle of the list and comparing it. If not matched, then if the target value is less than the middle element then the initial half will be drop otherwise the terminating half will be drop. The process will continue until we find the target value.

__Best Case:__ Target Value is at the middle position of the list  
__Worst Case:__ Target Value is at either first or last position of the list

## Depth First Search (DFS)

`Use when the tree is very wide and/or when the target value is located at the deep of the tree.`

Depth-first search (DFS) is an algorithm for traversing or searching tree or graph data structures. The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) and explores as far as possible along each branch before backtracking.

In DFS, you choose the root of the graph, tree, or data structure and explore every branch in order. When a branch is selected then it explores its all sub-branches before changing to a different branch.

__Best Case:__ Target Value is at the root position of the tree  
__Worst Case:__ Target Value is at the tip of a sub-branch of the last ordered branch

## Breadth First Search (BFS)

`Use when the tree is very deep (or target value is rare) and/or when the target value is located near the root of the tree.`

Breadth-first search (BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the tree root (or some arbitrary node of a graph, sometimes referred to as a 'search key'), and explores all of the neighbor nodes at the present depth prior to moving on to the nodes at the next depth level.

In BSF, same as in DFS, you choose the root node of graph, tree, or data structure.

__Best Case:__ Target Value is at the root position of the tree  
__Worst Case:__ Target Value is at the tip of the longest branch of the tree