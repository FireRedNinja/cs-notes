---
layout: post
title:  "Algorithmics 1"
date:   2017-12-26 18:50:00
categories: Level3 Semester1
author: dasha
---

##### Useful Textbooks

* M.T. Goodrich & R. Tamassia, Algorithm Design: Foundations, Analysis, and Internet Examples, Wiley, 2002
* D. Harel & Y. Feldman, Algorithmics: the Spirit of Computing, Addison Wesley, 2004 (also earlier 1992 edition by D. Harel)
* M. Sipser, Introduction to the Theory of Computation, Course Technology, 2006
<!--excerpt-->

### Contents

[Introduction](#section_0)  
   [Fundamental Algorithms and Data Structures](#section_1)  
   [Sorting Algorithms](#section_2)  
   [Strings and text algorithms](#section_3)  
   [Graphs and graph algorithms](#section_4)  
   [NP Completeness](#section_5)  
   [Computability](#section_6)  


<a name="section_0"></a>

#### Introduction


##### Revision - Algorithm Analysis

* Time and space complexity is written as a function of input size
* Worst case - gives a guarantee of algorithm's performance
* Asymptotic behaviour indicates what will happen as input size grows
* Expressed using Big O notation

###### Big O notation

* `f(n) = O(g(n))`
* `f` grows no faster than `g`
* there exists a real constant `c` and integer constant `N` such that `|f(n)| <= |c*g(n)|` for all `n => N`
* `f` is usually a complex function, which is not known precisely
* `g` is a known function eg O(1), O(n) etc
* use the "tightest" `g` we can find for an algorithm

###### Log function

* x = log<sub>a</sub>n if n = a<sup>x</sup>
* log<sub>a</sub> m * n = log<sub>a</sub>m + log<sub>a</sub>n
* log<sub>a</sub> m / n = log<sub>a</sub>m - log<sub>a</sub>n
* log<sub>a</sub>n<sup>c</sup> = c * log<sub>a</sub>n

###### Time complexities

**For some constant `c`:**

* Polynomial-time = O(n<sup>c</sup>)
* Exponential-time = no better than O(c<sup>n</sup>) where `c > 1`


<a name="section_1"></a>

#### Fundamental Algorithms and Data Structures

* [Stacks](#stack_topic), [queues](#queue_topic) and [priority queues](#priority_queue_topic)
* [Complete binary trees](#cbt_topic)
* [Heaps and heap operations](#heap_topic)
* [Java class](#java_heap) for (integer) heaps
* [Heap sort](#heap_sort_topic)

<a name="stack_topic"></a>

##### Stack abstract data type (LIFO)

**Basic operations:**

* *create*
* *isEmpty*
* *push* (to top of stack)
* *pop* (delete and return from top of stack)

**Represent it as:**

* an array - all operations are O(1)
* a linked list - all operations are O(1)

<a name="queue_topic"></a>

##### Queue abstract data type (FIFO)

**Basic operations:**

* *create*
* *isEmpty*
* *insert* (to the back of queue)
* *delete* (delete and return item at front of queue)

**Represent it as:**

* an array - all operations are O(1) and it must be "wrapped around", treated as circular
* a linked list - all operations are O(1)

<a name="priority_queue_topic"></a>

##### Priority queue abstract data type

**Basic operations:**

* *create*
* *isEmpty*
* *insert* (new item with given priority)
* *delete* (delete and return item with highest priority)

**Represent it as:**

* unordered list - *insert* O(1), *delete* O(n)
* ordered list - *insert* O(n), *delete* O(1)
* heap - *insert* and *delete* are O(logn)
* in all cases *create* and *isEmpty* are O(1)

<a name="cbt_topic"></a>

##### Complete Binary Trees

**Height of a node:**

* length of the longest path from the node to a leaf
* height of a heap is the height of its root node
* a binary tree of height `h` can contain maximum 2<sup>h+1</sup> - 1 nodes
* therefore the height of a CBT with `n` nodes is é log<sub>2</sub>( n + 1 ) - 1 ù

**A complete binary tree with `n` nodes has:**

* the minimum possible height
* the maximum possible number of nodes at each level *except the last* (ie for `i = 0, ... , h - 2`, level `i` has 2<sup>i</sup> nodes
* the nodes on the *last* level are as far to the left as possible

**Properties of a CBT:**

* with a height `h`, it has at *most* 2<sup>h+1</sup> - 1 nodes
* with `n` nodes, its height is é log<sub>2</sub>( n + 1 ) - 1 ù
* then it has é n / 2 ù leaf nodes
* and it has ⌊ n / 2 ⌋ branch nodes

<a name="heap_topic"></a>

##### Heaps


   **Def:** A CBT where each node stores an item, and has a priority value  
   **Heap property:** Every node's priority is greater than or equal to the priorities of all its descendent nodes  
   **Min-heap:** Inverted so that the minimum priority is at the root
<br>
<br>
**For a node `i`:**

* its children are nodes `2i + 1` and `2i + 2`
* its parent is the node `⌊ (i - 1) / 2 ⌋`

**Basic operations:**

* *insert* an item
* *build* a heap containing a given set of items
* *delete* the item with highest priority
* *impose* the heap property on a given node

**Complexity:**

* *build* is O(n log n) and there is an O(n) alternative
* all other operations are O(log n) for algorithms which take O(1) steps at each level of the heap

**Insertion:**  
   `while (new_value NOT in root && new_value > parent_value)  
   swap new_value with parent_value`  
   **Imposing:**  
   Pre-condition - a specified node may violate the heap property, but all its descendents satisfy the property  
   Post-condition - the specified node and all of its descendents satisfy the property  
   `while (bad_value NOT in leaf && bad_value < larger_child)  
   swap bad_value with larger_child`  
   **Deletion:**  
   `swap root with node in last (bottom-right) leaf  
delete last leaf  
impose heap property on bad value now in root`  
   **Building:**  
   Pre-condition - values are in arbitrary order  
   Post-condition - values form a heap  
   `for each non-leaf node in bottom-to-top right-to-left order  
   impose heap propery`

<a name="java_heap"></a>

##### An integer heap class

Represent using an array, where:

* children of a node `i` are in the array at `2i + 1` and `2i + 2` 
* parent of a node `i` are in the array at `(i - 1) / 2` (floored automatically in Java)

Heap class [implementation in Java](#heap_class)

<a name="heap_sort_topic"></a>

##### Heap Sort

* more efficient than selection sort
* O(n log n) in the worst case
* [pseudocode](#heap_sort)


<a name="section_2"></a>

#### Sorting Algorithms

* [Comparison-based sorting](#comparison_topic)
* [Radix](#radix_topic) sort
* [Tries](#trie_topic) (re**trie**val)

**Common sorts:**  
   O(n<sup>2</sup>) - selection, insertion, bubble  
   O(n log n) - merge, heap  
   Quicksort is O(n log n) on average (but no better than O(n<sup>2</sup>) in the worst case

<a name="comparison_topic"></a>
   
##### Comparison-based sorting

   **Claim:** No sorting algorithm that is based on pairwise comparison can be better than O(n log n) in the worst case  
   **Justification:** Draw out the algorithm using a binary decision tree, where each node represents a comparison between two elements

* leaf nodes represent the possible outcomes of the algorithm
* so the number of leaf nodes = the possible ordering of `n` items
* so there are at least `n!` and maximum 2<sup>h+1</sup> leaf nodes
* its worst case complexity is O(h) where `h` = its height
* it follows that n! <= 2<sup>h+1</sup>

<img src="/cs-notes/assets/images/algs/decision_tree.png" nopin="nopin" />

   Reversing inequality and taking log<sub>2</sub> of both sides:
   
<img src="/cs-notes/assets/images/algs/comparison_based_complexity.png" nopin="nopin" />

   Giving a complexity of O(n log n) as required

<a name="radix_topic"></a>

##### Radix sorting

* O(n) complexity
* exploits the structure of items to be sorted to achieve this
* faster than O(n log n) only for very large `n`

**How it works:**

* each iteration the items are distributed into buckets (lists)
* during an `i`<sup>th</sup> iteration an item is placed in the bucket corresponding to the integer represented by its bits
* at the end of an iteration the buckets are concatenated to give a new sequence which will be used as the starting point of the next iteration
* there are `m / b` iterations, where `m` is the length of bit-sequences representing an item, and `b` is a chosen factor of `m`

To sort the following sequence: `15 43 5 27 60 18 26 2`  
   Where binary encodings are given by:  
   `15 = 001111  43 = 101011  5 = 000101  27 = 011011`  
   `60 = 111100  18 = 010010  26 = 011010  2 = 000010`
   
   Items have bit positions 0, ..., 5 so `m` = 6  
   `b` must be a factor of `m`, so choose `b` = 2  
   So we have 2<sup>b</sup> = 2<sup>2</sup> = 4 buckets labelled 0, 1, 2, 3 (or 00, 01, 10, 11)
   And `m / b = 3` iterations are required
   
See radix sorting pseudocode [here](#radix_sort)

**Correctness:** For two items `x` and `y` where `x < y`, we need to show that `x` precedes `y` in the final sequence

**During the last iteration** where some bits of `x` and `y` differ:

* the bits of `x` must be smaller than `y`
* so `x` goes into a bucket before `y` does
* so `x` precedes `y` in the sequence after this iteration
* in later iterations, `x` and `y` go in the same bucket as they don't have any more differing bits

**Complexity:**

* during each of the `m / b` iterations, the sequence is scanned --> O(n) time, and buckets are concatenated --> O(2<sup>b</sup>) time
* overall, O(m / b (n + 2<sup>b</sup>)) --> O(n)

**Time-space trade-off:**

* the larger the value of b, the smaller the multiplicative constant (m / b) in the complexity function and so the faster the algorithm will become
* an array of size 2<sup>b</sup> is required, so increasing `b` will increase space requirements

<a name="trie_topic"></a>

##### Tries

* stored items have a key that is interpreted as a sequence of bits/characters
* there is a multiway branch at each node where each branch has an associated symbol
* no two siblings have the same symbol
* the branch to be taken at level `i` is determined by the `i`<sup>th</sup> element of the key
* tracing a path from root to a node spells out the key of the item
* eg, used to store strings

<img src="/cs-notes/assets/images/algs/trie.png" nopin="nopin" />

*Search* and *insert* algorithms for the trie found [here](#trie_alg)

**Represent it as:**

* an array of pointers, which represent children
* linked lists, containing children of each node

<img src="/cs-notes/assets/images/algs/trie_list.png" nopin="nopin" />

[Example](#trie_class) trie class to represent a dictionary


<a name="section_3"></a>
   
#### Strings and text algorithms

* [Text compression](#compression_topic)
  * [Huffman](#huffman_topic) and [LZW](#lzw_topic)
* [String comparison](#string_comparison_topic)
  * [String distance](#string_distance_topic)
* [String/pattern search](#pattern_topic)
  * [Brute force](#brute_topic)
  * [KMP](#kmp_topic)
  * [BM](#bm_topic)

<a name="compression_topic"></a>
  
##### Text compression

* lossless
* compression ratio is `x / y` where `x` = compressed and `y` = original
* space saved = `1 - (x / y) * 100%`

<a name="huffman_topic"></a>

##### Huffman encoding

* statistical method
* unique, variable-length codeword for each character
* no codeword is the prefix of another
* each character is a leaf node
* codeword is the path from root to appropriate leaf
* when going down the path, left route = 0, right route = 1

**Huffman tree construction:**

* add leaf nodes containing the character represented and its frequency
* while there are > 1 parentless nodes
  * add new parent to the two nodes of smallest weight (frequency)
  * weight of the parent node = sum of child weights
  
The tree for a file with char frequencies:  
   `Space = 15  E = 11  A = 9  T = 8  I = 7  S = 7`  
   `R = 7  O = 6  N = 4  U = 3  H = 2  C = 1  D = 1`
   
<img src="/cs-notes/assets/images/algs/huffman_1.png" nopin="nopin" />

Tree construction [pseudocode](#huff_contruct)

**Generating the codewords:**

* following left and right paths down the constructed tree
  * Space `10`
  * E `010`
  * A `111`
  * T `110`
  * I `0000`
  * S `0001`
  * R `0011`
  * O `0110`
  * N `0111`
  * U `00101`
  * H `001001`
  * C `0010000`
  * D `0010001`
  
**Weighted path length of tree T:**

* `SUM( weight * distance from root )`
* sum is over all leaf nodes
* this gives the number of bits in the compressed file

**Complexity:**

* building tree - O(n)
* compression - O(n)
* decompression - O(n)
* use **adaptive** Huffman coding
  * same tree built and adapted by compressor and decompressor

<a name="lzw_topic"></a>
  
##### LZW compression

* dictionary method
* collection of strings, each with a bit pattern that represents it
* dictionary built dynamically during compression and decompression
* if string `s` is represented, so is every prefix of `s`
* a **trie** is an ideal representation

At any given time during comp./decomp. there is a **current codeword length `k`**:

* 2<sup>k</sup> distinct codewords available
* limits size of dictionary, but can be incremented as necessary (so doubling the codeword availability)
* initial `k` should be large enough to encode all strings of length `l`

LZW compression [pseudocode](#lzw)

<img src="/cs-notes/assets/images/algs/lzw_1.png" nopin="nopin" />

**LZW variants:**

* constant - fixed capacity dictionary
* dynamic - add 1 to current length whenever dictionary becomes full
* LRU - when full, current string replaces the least recently used string in the dictionary

**LZW decompression:**

* builds same dictionary as compression but **1 step out of phase**
* may encounter codeword that is not in dictionary
  * if (lookup fails) newS = oldS + oldS.charAt(0);
  
LZW decompression [pseudocode](#lzw_decomp)

<img src="/cs-notes/assets/images/algs/lzw_2.png" nopin="nopin" />

**Complexity:** O(n) for comp. and decomp. each

<a name="string_comparison_topic"></a>

##### String comparison

* given strings `s` and `t` of lengths `m` and `n`, what is the smallest number of basic operations needed to transform `s` into `t`?
* use
  * insertion
  * deletion
  * subsitution
  
**String distance:**

<img src="/cs-notes/assets/images/algs/distance_1.png" nopin="nopin" />

**Prefixes:**

* `i`<sup>th</sup> prefix of string `s` is first `i` chars of `s`
* let `d( i,j )` = distance between prefix `i` of `s` and prefix `j` of `t`
* then distance between `s` and `t` = `d( m,n )` for `len(s) = m` and `len(t) = n`

**Optimal alignment:**

The last position of the alignment must either be of the form  
   <img src="/cs-notes/assets/images/algs/optimal_alignment.png" nopin="nopin" />
   
In other words,  
   <img src="/cs-notes/assets/images/algs/optimal_alignment_alt.png" nopin="nopin" />

<a name="string_distance_topic"></a>
   
##### Distance with dynamic programming

* fill in entries of an `m * n` table row by row, and column by column
* time and space complexity = O(mn)
* keep most recent entry in each column of the table
  * space complexity = O(m + n)
  
**Distances table:**

<img src="/cs-notes/assets/images/algs/distance_table.png" nopin="nopin" />

* entries calculated one by one by applying formula above
* final entry `d( 7,8 ) = 4` so string distance is **4**
* trace back to entry `( 0,0 )` to find optimal alignment
  * vertical = deletion
  * horizontal = insertion
  * diagonal = match/substitution

<a name="pattern_topic"></a>
  
##### String/pattern search

Given a text `t` of length `n`, and a string/pattern `s` of length `m`, find the position of the last occurence of `s` in `t`

<a name="brute_topic"></a>

##### Brute force algorithm

* current starting position in text = 0
* compare chars from `s` and `t` left to right until the entire string is matched
* if mismatch, advance starting position by 1 and repeat

Brute force [pseudocode](#brute_force)

**Effectiveness:**

* expressed using char arrays rather than strings in Java
* `m` char comparisons needed at each `n - (m + 1)` positions in text before the pattern is found
* worse case O(mn)
* average case O(n)

<a name="kmp_topic"></a>

##### KMP algorithm

* online - removes need to back-up in text
* worst case O(n)
* need to pre-process the string into a border table (an array `b` with an entry `b[j]` for each position `j`)
* if mismatch at `j`, remain at current text char
* the border table says what to compare next

**Border of a string `s`:**

* a substring that
  * is a prefix
  * is a suffix
  * cannot be the string itself
* eg for string `s = a c a c g a t a c a c`
  * borders are `ac` and `acac`
  * `acac` is the longest border
  
**Border table:**
  
<img src="/cs-notes/assets/images/algs/border_table.png" nopin="nopin" />

* `b[j]` is
  * the length of the longest border of `s[0...j-1]`
  * `max { k | s[0...k-1] = s[j-k...j-1] }`
  
**KMP seach :**

* [implementation](#kmp)
* this is O(n) worst case
* naive method requires O(j<sup>2</sup>) steps to find `b[j]`, so O(m<sup>2</sup>) overall
* can be implemented in O(m + n) time (to set up border table and to conduct search)

<a name="bm_topic"></a>

##### Boyer-Moore algorithm

* string scanned left-to-right
* mismatched char used to decide next comparison
* need to pre-process string to record position of last occurence of each char in the alphabet
* alphabet must be fixed in advance of search

**Position of last occurence of char `c` in string `s`:**

* `max { k | s[k] = c }` if such a `k` exists, `-1` otherwise
* store last occurence position of `c` in array element `p[c]`

**Jump steps on a mismatch:**

* if mismatch between `s[j]` and `t[i]`, move `s` along so `p[t[i]]` of `s` aligns with `t[i]`
* if this moves `s` in the "wrong direction", instead move `s` one position to the right
* if `t[i]` doesn't appear in the string, slide the string past `t[i]`

**Jump step cases:**

1. `p[t[i]] < j and => 0`
   * new `i = i + m - 1 - p[t[i]]`
   * new `j = m - 1`
   * new `sp = sp + j - p[t[i]]` (starting position)
2. `p[t[i]] > j`
   * new `i = i + m - j`
   * new `j = m - 1`
   * new `sp = sp + 1`
3. `p[t[i]] = -1`
   * new `i = i + m`
   * new `j = m - 1`
   * new `sp = sp + j + 1`
   
BM [implementation](#bm)
   
**BM complexity:**

* worst case O(mn)
* search for `s = ab...aa` of length `m` in `t = aa...aaaa..aa` of length `n`
* `m - 1` char comparisons needed at each `n - (m + 1)` positions in text


<a name="section_4"></a>

#### Graphs and graph algorithms

* [Graph basics](#graph_basics_topic)
* [Graph representations](#graph_representations_topic)
* [Searching and traversal](#graph_search_topic)
* [Weighted graphs](#graph_weight_topic)
* [Topological ordering](#topological_topic)

<a name="graph_basics_topic"></a>

##### Graph basics

**Undirected graphs:**

* `G = (V,E)`
* each vertex is a point
* each edge is a line joining a pair of vertices

**Connected:** every vertex pair is joined by a path  
   **Non-connected:** graph has 2+ connected components  
   **Tree:** connected and acyclic (no cycles)  
   **Forest:** acyclic and components are trees  
   **Complete (clique):** every vertex pair is joined by an edge  
   **Bipartite:** vertices are in two dijoint sets `U` and `W` and **every** edge joins a vertex in `U` to one in `W`
   
<img src="/cs-notes/assets/images/algs/undirected_1.png" nopin="nopin" />

For the graphs above:

* adjacent - `{ a,z } Î E`
* non-adjacent - `{ a,b } ∉ E`
* `a` is **incident to** edge `{ a,z }`
* `a, x, b, y, c` is a path of length 4
* `a, x, b, y, a` is a cycle of length 4
* all vertices have **degree** 3

**Directed graphs (digraphs):**

* `D = (V,E)` where `V` and `E` are **finite** sets
* edges are ordered pairs
* drawn as arrows
* vertices have **in-degrees** and **out-degrees**
* paths and cycles must follow edge directions

<img src="/cs-notes/assets/images/algs/directed_1.png" nopin="nopin" />

In the graph above:

* `u` is adjacent **to** `v`
* `v` is ajdacent **from** `u`
* `y` has in-degree 2 and out-degree 1


<a name="graph_representations_topic"></a>

##### Graph representations

**Representing the undirected graph G:**

<img src="/cs-notes/assets/images/algs/undirected_2.png" nopin="nopin" />
   
**Representing the directed graph D:**

<img src="/cs-notes/assets/images/algs/directed_2.png" nopin="nopin" />

**Implementing adjaceny lists:**  
   Define classes representing  

* an entry of adjacency lists
* a vertex (with a linked list representing its adjacency list)
* a graph (with a size and an array of vertices)

Java [implementation](#adjacency_list) of an adjacency list


<a name="graph_search_topic"></a>

##### Graph searching and traversal algorithms

Graph traversal is efficient if it visits all vertices of the graph in `O( |V| + |E| )` time (by travelling along edges)


**Depth-first search:**

* follow a path of unvisited vertices until path can be extended no further
* backtrack until an unvisited vertex is reached
* repeat until there are no unvisited vertices (in all components of graph)
* edges used form a **depth-first spanning tree**

**Represent it as:**

* explicit stack 
* containing vertices on the path to the current vertex
* popping corresponds to backtracking

**DFS example:**

<img src="/cs-notes/assets/images/algs/dfs_1.png" nopin="nopin" />

DFS [implementation](#dfs)

**DFS complexity:**

* each vertex is visited ( `n` )
* each element in adj. list is processed ( `m` )
* O(n + m)
* can adapt to adj. matrix representation, but this increases complexity to O(n<sup>2</sup>)

**Applications of DFS:**

* determine if graph is connected and/or identify its connected components
* determine if a graph is bipartite
* determine if a graph contains a cycle

**Breadth-first search:**

* visit all adjacent vertices of current vertex (processing)
* vertices processed in the order in which they are visited (queue)
* continue until all vertices in current component have been processed
* edges used form a **breadth-first spanning tree**

**Represent it as:**

* queue
* visited vertices are added

**BFS example:**

<img src="/cs-notes/assets/images/algs/bfs_1.png" nopin="nopin" />

BFS [implementation](#bfs)

**BFS complexity:**

* each vertex visited and queued exactly once
* each adj. list traversed once
* O(n + m)
* can adapt to adj. matrix as with DFS, but also O(n<sup>2</sup>)

**Applications of BFS:**

* finding distance between two vertices

**Distance between two vertices:**

* assign distance `v = 0`
* carry out BFS from `v`
* when visiting a new vertex
  * assign its distance to be `1 + distance to its predecessor`
  
<img src="/cs-notes/assets/images/algs/bfs_2.png" nopin="nopin" />


<a name="graph_weight_topic"></a>

##### Weighted graphs

Each edge `e` has an integer weight given by `wt( e ) > 0` (undirected or directed)  
   Can represent weighted graphs using adj. lists and matrices as before
   
<img src="/cs-notes/assets/images/algs/weighted_1.png" nopin="nopin" />

<img src="/cs-notes/assets/images/algs/weighted_2.png" nopin="nopin" />

**Dijkstra's algorithm:**

* finds shortest path from one vertex `u` to all other vertices
* maintains a set containing all vertices for which shortest path from `u` is currently known
* each vertex `v` not in the set has a label `d(v)` = length of a shortest path from `u -> v` passing **only** through vertices in the set
* after adding `v` to the set, carry out **edge relaxation** (updating distance `d(w)` for all vertices `w` still not in the set)

**Edge relaxation:**

* suppose `v` and `w` are not in `S`, then we know
  * the shortest path from `u -> v` passing only through `S` is `d(v)`
  * the shortest path from `u -> w` passing only through `S` is `d(w)`
* suppose `v` is added to `S` and the edge `e = { v,w }` has weight `wt( e )`
* calculate the shortest path `u -> w` passing only through `S ∪ { v }`

<img src="/cs-notes/assets/images/algs/dijkstra_1.png" nopin="nopin" />

It is either:

* the original path through `S` of length `d(w)`
* the path combining edge `e` and shortest path `v -> u` with length `wt( e ) + d(v)`

Therefore, the distance is:   
   `d(w) = min{ d(w), d(v) + wt( e ) }`
   
Dijkstra's algorithm [implementation](#dijkstra)

**Dijkstra complexity:**

* with `n` vertices and `m` edges, using an **unordered array**
  * O(n) to initialise distances
  * O(n<sup>2</sup>) to find minimum
  * O(m) for relaxation
* hence, O(n<sup>2</sup>) overall

* with `n` vertices and `m` edges, using a **heap**
  * O(n) to initialise distances and create heap
  * O(n log n) to find minimum
  * O(m log n) for relaxation
* hence, O(m log n) overall (more edges than vertices)

**Dijkstra example:**

<img src="/cs-notes/assets/images/algs/dijkstra_2.png" nopin="nopin" />

**Spanning tree:**

* subgraph which is both a tree and spans every vertex
* obtained from a connected graph by **deleting edges**
* its weight = sum of weights of its edges

For a weighted connected undirected graph, find a **minimum weight spanning tree** (represents the cheapest way of interconnecting the vertices)

<img src="/cs-notes/assets/images/algs/spanning_tree.png" nopin="nopin" />

**Minimum weight spanning tree problem:**

This is an example of a **greedy** algorithm

* makes a sequence of decisions based on **local optimality**
* ends up with the **globally optimal** solution

**Prim-Jarnik algorithm:**

* minimum spanning tree contructed by choosing a sequence of edges
* initialisation is O(n) (where `n` is number of vertices)
* outer loop executed `n - 1` times
* inner loop checks all edges from a tree-vertex to a non-tree vertex, of which there can be O(n<sup>2</sup>)
* overall, alg. is O(n<sup>3</sup>)

Prim-Jarnik algorithm [pseudocode](#prim_jarnik)

Prim-Jarnik example

<img src="/cs-notes/assets/images/algs/prim_jarnik.png" nopin="nopin" />

The Prim-Jarnik proof of correctness will **not** be part of the exam, so it is omitted here.

**Dijkstra's refinement:**

Introduce attribute `bestTV` for each non-tree vertex `q`  
   This is the best tree vertex `p` for which `wt( {p, q} )` is minimised  
   [Pseudocode](#dijkstra_refinement) for this concept
   
* initialisation is O(n)
* while loop executed `n - 1` time
* O(n) to find minimal ntv
* O(1) to adjoin and update
* overall alg. is O(n<sup>2</sup>)


<a name="topological_topic"></a>

##### Topological ordering

**Directed Acyclic Graphs:**

A **topological order** on a DAG is a labelling of the vertices `1, ..., n` such that `(u, v) Î E` implies `label(u) < label(v)`  
   A directed graph D has a topological order if and only if D is a DAG  
   A **source** is a vertex of in-degree 0 and a **sink** has out-degree 0  
   **A DAG has at least one souce and at least one sink**, which forms the basis of a topological ordering alg.
   
Topological ordering of DAG `D`:

<img src="/cs-notes/assets/images/algs/dag.png" nopin="nopin" />

Topological ordering alg. [implementation](#topological_ordering)

**TOA correctness:**

A vertex is given a label only when the number of incoming edges from unlabelled vertices is 0  
   For `n` vertices, `m` edges:
   
Adj. matrix representation involves

* finding in-degree of each vertex, by scanning each column - O(n<sup>2</sup>)
* main loop executed `n` times for each row - O(n)
* overall alg. is O(n<sup>2</sup>)

Adj. list representation involves

* finding in-degree of each vertex, by scanning the list - O(n + m)
* main loop executed `n` times for each list
* overall alg. is O(n + m)

**Deadlock detection:**

Methods to detect whether a digraph contains a cycle

1. adaptation of topological ordering alg.
   * if source list becomes empty before all vertices are labelled, there must be a cycle
   * if all vertices can be labelled, the digraph is acyclic
2. adaptation of DFS
   * when a vertex is visited, check where there is an edge from it to another vertex which is on the current path from the current starting vertex
   * the existence of such a vertex indicates a cycle


<a name="section_5"></a>

#### NP Completeness

* [Introduction](#np_intro_topic)
* [NP-complete problems](#np_complete_topic)
* [The classes P and NP](#classes_topic)
* [Polynomial-time reductions](#poly_time_topic)
* [Formal def. of NP-completeness](#np_def_topic)
* [How to prove a problem is NP-complete](#prove_np_topic)

<a name="np_intro_topic"></a>

##### Introduction

We have seen algorithms for a wide range of problems, all of which are polynomial-time: their worst cast complexity is O(n<sup>c</sup>) for some constant `c`


Recall the Eulerian cycle problem: whether a graph has a cycle that traverses each **edge** exactly once  
   Theorem: A connected undirected graph has an Eulerian cycle if and only if each vertex has even degree  
   Therefore we can test and find such a cycle in a graph `G` in
   
* O(n<sup>2</sup>) time if `G` is represented with an adj. matrix
* O(m + n) if it is represented with an adj. list (`m = |E|` and `n = |V|`)

Recall the Hamiltonian cycle problem: whether a graph has a cycle that traverses each **vertex** exactly once  
   It is similar to the Eulerian cycle problem, but a polynomial-time algorithm has **not** been found to solve it  
   Its complexity is O(n<sup>2</sup> * n!) in the worst case  
   No polynomial-time algorithm has been found to solve this  
   Therefore this problem is **NP-complete**
   
* this is exponential (no better than O(b<sup>n</sup>) for some `b`)
* and cannot be expressed as O(n<sup>c</sup>)

**Polynomial vs exponential:**

<img src="/cs-notes/assets/images/algs/poly_vs_exp.png" nopin="nopin" />

Similar behaviour emerges in terms of computing power  
   Basically, a thousand-fold increase in computing power would only add `6` to the size of the largest problem instance solvable in `1` hour, for an algorithm of 3<sup>n</sup> complexity


A problem is **polynomial-time solvable** if it admits a polynomial-time algorithm

<a name="np_complete_topic"></a>

##### NP-completeness

No polynomial-time algorithm is known for an NP-complete problem  
   **However**, if one of them is solvable, then they all are

No proof of intractability is known for an NP-complete problem  
   **However**, if one of them is intractable, then they all are
   
**Causes of intractability:**

1. polynomial time is not sufficient in order to discover a solution
   * there are intractability proofs for this
   * some problems are **undecidable** (no alg. could solve them)
   * some decidable problems have been shown to be intractable
2. solution itself is so large that exp. time is needed to output it
   * eg problems of generating all cycles for a given graph
   
**Roadblock:**

* two players A and B
* network of roads, with intersections
* each road is coloured black, blue or green
* some intersections are marked "A wins" or "B wins"
* a player has a fleet of cars located at intersections (one car per intersection)

Player A begins, and then they take turns to

* move a car of theirs on one or more roads of the same colour
* a car may not overlap an intersection which already has a car

The problem is deciding, for a given starting configuration, whether A can win, regardless of what moves B takes

<img src="/cs-notes/assets/images/algs/roadblock.png" nopin="nopin" />

So, `NP-complete problems` must be **equal** to one of: `Polynomial-time solvable problems` or `Intractable problems`, and **not equal** to the other
   
**Problems:**

A problem is characterised by unspecified parameters  
   A problem instance is created by giving these parameters values  
   An example of a decision problem is the Hamiltonian cycle:  
   
* the answer is a "yes" or "no"
* its instance if a graph `G`
* every instance is either a "yes"-instance or a "no"-instance

**Other NP-complete problems:**

Travelling Salesman Decision Problem  
   Instance: a set of `n` cities and integer distance `d(i, j)` between each pair of cities `i, j` and a target integer `K`  
   Question: is there a permutation `P1P2...Pn-1Pn` of `1, 2,..., n` such that `d(P1, P2) + d(P2, P3) + ... + d(Pn-1, Pn) + d(Pn, P1) <= K`?
   
Clique Problem  
   Instance: a graph `G` and target integer `K`  
   Question: does `G` contain a clique of size `K`? (a set of `K` verices for which there is an edge between all pairs
   
Graph Colouring Problem  
   Instance: a graph `G` and target integer `K`  
   Question: can one of `K` colours be attached to each vertex of `G` so that adjacent vertices always have different colours?
   
<img src="/cs-notes/assets/images/algs/graph_colouring.png" nopin="nopin" />

Satisfiability  
   Instance: boolean expression `B` in **conjunctive normal form**  
   CNF: `C1 ∧ C2 ∧ ... ∧ Cn` where each `Ci` is a **clause**  
   Clause `C`: `L1 ∨ L2 ∨ ... ∨ Lm` where each `Lj` is a **literal**  
   Literal `L`: a variable `x` or its negation `¬x`  
   Question: is `B` satisfiable? (can values be assigned to the variables that make `B` true?)

<img src="/cs-notes/assets/images/algs/satisfiability.png" nopin="nopin" />

NP-completeness deals primarily with decision problems

* corresponding to each instance of an optimisation or search problem
* there is a family of instances of a decision problem obtainable by setting "target" values
* an optimisation or search problem can be solved in poly. time if and only if the corresponding decision problem can

<a name="classes_topic"></a>

##### The classes P and NP

**P:**

* the class of all decision problems that can be solved in poly. time
* often extended to include search and optimisation problems

**NP:**

* the class of decision problems solvable in **non-deterministic** polynomial time (a non-deterministic alg. can make non-deterministic choices, and hence is more powerful than a deterministic alg.)
* P is contained within NP
* there is no problem known to be in NP and known not to be in P

**P vs NP:**

A decision problem is NP if every "yes"-instance has a **short certificate**  
   i.e. a structure that can be used to verify, in polynomial time, that it is a "yes"-instance  
   No corresponding claim is made for "no"-instances
   

It is immediate that `P ⊆ NP`, but whether `P = NP` or `P ⊂ NP` is unknown  
   Most believe that `P ≠ NP`  
   But if so, there are problems that must lie in NP and not in P, and these are the NP-complete problems (the hardest, eg HC, TSDP, Graph Colouring etc)  
   A poly. time alg. for any of these would imply that they are **all** in P
   
   
**Non-deterministic algorithms:**

* has an extra operation: non-deterministic choice
* has many possible executions depending on values returned from the choice
* it solves a decision problem `Π` if
  * for a "yes"-instance `I` of `Π` there is **some** execution that returns "yes"
  * for a "no"-instance `I` of `Π` there is **no** execution that returns "yes"
* and solves a decision problem `Π` in poly. time if
  * for every "yes"-instance `I` of `Π` there is **some** execution `E` that returns "yes", which uses a number of steps bounded by a polynomial in the input
  
A non-deterministic alg. can be viewed as

* a guessing stage (non-deterministic)
* a checking stage (deterministic and poly. time)

Start ---> guess a "certificate" ---> verify the certificate ---> Stop  

[Example](#non_deterministic) of a non-deterministic alg.


<a name="poly_time_topic"></a>

##### Polynomial-time reductions

A mapping `f` from a decision problem `Π1` to a decision problem `Π2` such that

* for every instance `I1` of `Π1` we have
  * the instance `f(I1)` of `Π2` can be contructed in poly. time
  * `f(I1)` is a "yes"-instance of `Π2` if and only if `I1` is a "yes"-instance of `Π1`
* we write `Π1 ∝ Π2` as an abbreviation for: there is a polynomial-time reduction from `Π1` to `Π2`

**Properties of polynomial-time reductions:**

Transitivity: `Π1 ∝ Π2` and `Π2 ∝ Π3` implies that `Π1 ∝ Π3`

Since `Π1 ∝ Π2` and `Π2 ∝ Π3` we have

* a PTR `f` from `Π1` to `Π2`
* a PTR `g` from `Π2` to `Π3`

For any instance `I1` of `Π1`, since `f` is a PTR, we have

* `I2 = f( I1 )` is an instance of `Π2` that can be constructed in poly. time
* `I2` has the same answer as `I1`

Since `g` is a PTR, we have

* `I3 = g( I2 )` is an instance of `Π3` that can be constructed in poly. time
* `I3` has the same answer as `I2`

Putting the results together, for any instance `I1` of `Π1`

* `I3 = g( f( I1 ) )` is an instance of `Π3` constructed in poly. time
* `I3` has the same answer as `I1`
* ie the composition of `f` and `g` is a PTR from `Π1` to `Π3`

`Π1 ∝ Π2` and `Π2 Î P` implies that `Π1 Î P`

* to solve an instance of `Π1`, reduce it to an instance of `Π2`
* `Π1 ∝ Π2` means that `Π1` is no harder than `Π2`
* i.e. if we can solve `Π2`, then we can solve `Π1` without much more effort

For example, reducing the Hamiltonian cycle problem to the travelling salesman problem:  
   HC instance: a graph G  
   HC question: does G contain a cycle that visits each vertex exactly once?  
     
   TSDP instance: a set of `n` cities and integer distance `d(i, j)` between each pair of cities `i, j` and a target integer `K`  
   TSDP question: is there a permutation `p` of `{1, 2,..., n}` such that `d(P1, P2) + d(P2, P3) + ... + d(Pn-1, Pn) + d(Pn, P1) <= K`?
   
* `G = (V, E)` is an instance of HC
* construct TSP `f(G)` where
  * cities = `V`
  * `d(u, v) = 1` if `{u, v} Î E` and `0` otherwise
  * `K = |V|`
* `f(G)` can be constructed in poly. time
* `f(G)` has a tour of length `<= |V|` if and only if `G` has a Hamiltonian cycle (cannot take any of the edges with weight 2)
* therefore `TSDP Î P` implies that `HC Î P`
* equivalently `HC Ï P`implies that `TSDP Ï P`

<img src="/cs-notes/assets/images/algs/hc_to_tsdp.png" nopin="nopin" />


<a name="np_def_topic"></a>

##### Definition

A decision problem `Π` is NP-complete if

* `Π Î NP`
* `Π’` is polynomial-time reducable to `Π` (`Π’∝Π` for every problem `Π’` in NP)

So if `Π` is NP-complete and `Π Î P` then P = NP  
   Every problem in NP can be solved in polynomial time by reduction to `Π`  
   Supposing P ≠ NP, if `Π` is NP-complete, then `Π Ï P`

<img src="/cs-notes/assets/images/algs/np_structure.png" nopin="nopin" />

<a name="prove_np_topic"></a>

##### Proving NP-completeness

It is not feasible to describe a reduction from **every** problem in NP  
   However, suppose we knew just one NP-complete problem `Π1`
   
To prove `Π2` is NP-complete, it is enough to show

* `Π2` is in NP
* there exists a polynomial-time reduction from `Π1` to `Π2` (`Π1 ∝ Π2`)

Correctness of the approach:

* for any `Π' Î NP`, since `Π1` is NP-complete we have `Π' ∝ Π1`
* since `Π' ∝ Π`, `Π1 ∝ Π2` and in is transitive, it follows that `Π' ∝ Π2`
* since `Π' Î NP` was arbitrary, `Π' ∝ Π2` for all `Π' Î NP`
* hence `Π2` is NP-complete

Cook's Theorem, where the Satisfiability (SAT) problem is NP-complete

* proof consists of generic poly-time reduction to SAT from an abstract definition of a general problem in NP
* generic reduction could be instantiated to give an actual reduction for each individual NP problem
* given this theorem, to prove that problem P is NP-complete it is sufficient to show that
  * `Π` is in NP
  * there exists a poly-time reduction from SAT to `Π`
  
**Clique Problem:**

Instance: graph G and target integer K  
   Question: does G contain a clique of size K?  
   Proving: show clique is in NP, and that there exists a poly-time reduction from SAT to `Π`
   
We need to show SAT ∝ Clique:  
   Given an instance B of SAT we construct a `(G, K)` instance of Clique  
   
* K number of clauses of B
* vertices of G are pairs `(l, C)` where `l` is a literal clause of `C`
* `{(l, C), (m, D)}` is an edge of G if and only if `l ≠ ¬m` and `C ≠ D`
  * edge if distinct literals from different clauses can be satisfied simultaneously
* poly-time construction O(n<sup>2</sup>) (with `n` literals)
* this is a poly-time reduction since B has a satisfying argument if and only if G has a clique of size K

Proving it is a poly-time reduction:

* if B has a satisfying assignment then
  * if we choose a **true** literal in each clause the corresponding vertices form a clique of size K in G
* if G has a clique of size K then
  * assigning each literal associated with a vertex in the clique to be true yields a satisfying assignment for B
  
The following graph G has a clique of size 4 if and only if B has a satisfying assignment (which is a clique of size 4 here)

<img src="/cs-notes/assets/images/algs/clique.png" nopin="nopin" />

`B = (x1 ∨ x2 ∨ ¬x3) ∧ (¬x1 ∨ x3 ∨ ¬x4) ∧ (¬x2 ∨ x4) ∧ (x2 ∨ ¬x3 ∨ x4)`  
   There are K = 4 clauses (bracket pairs)
   
**Problem restrictions:**

A restriction consists of a subset of the instances of the original problem  
  If a restriction of a given decision problem `Π` is NP-complete, then so is `Π`  
  Given NP-complete `Π`, a restriction of `Π` **might** be NP-complete
  
eg a clique restricted to cubic graphs is in P, so a largest clique has size at most 4, so exhaustive search is O(n<sup>4</sup>)

K-colouring:  
   Restriction of Graph Colouring for a fixed K number of colours  
   2-colouring is in P, while 3-colouring is NP-complete
   
K-SAT:  
   Restriction of SAT in which every clause contains exactly K literals  
   2-SAT is in P, while 3-SAT in NP-complete  
   Showing 3-SAT Î NP is easy
   
**SAT ∝ 3-SAT:**

Given instance B of SAT we will construct an instance B' of 3-SAT  
   For each clause Ci of B we construct a number of clauses of B'
   
* if `C = l1`
  * introduce 2 additional variables x1 and x2, and add the clauses `(l1 ∨ x1 ∨ x2), (l1 ∨ x1 ∨ ¬x2), (l1 ∨ ¬x1 ∨ x2), (l1 ∨ ¬x1 ∨ ¬x2)` to B'
* if `C = (l1 ∨ l2)`
  * introduce 1 additional variable y and the clauses `(l1 ∨ l2 ∨ y) and (l1 ∨ l2 ∨ ¬y)` to B'
* if `C = (l1 ∨ l2 ∨ l3)`
  * add the clause C to B'
* if `C = (l1 ∨ ... ∨ lk)` and `k > 3`
  * introduce k - 3 additional variables z<sub>1</sub>, ..., z<sub>k-3</sub>
  * add the clauses `(l1 ∨ l2 ∨ z1), (¬z1 ∨ l3 ∨ z2), (¬z2 ∨ l4 ∨ z3), ..., (¬zk-4 ∨ lk-2 ∨ zk-3), (¬zk-3 ∨ lk-1 ∨ lk)` to B'
  
**Coping with NP-completeness:**

Maybe only a restricted version is of interest (which may be in P)  
   Seek an exponential-time alg. which improves on exhaustive search  
   For an optimisation problem:
   
* settle for an approximation alg. that runs in poly-time
* esp. if it gives a probably good result
* use a heuristic

For a decision problem:

* settle for a probabilistic alg. (correct answer with high probability)


<a name="section_6"></a>

#### Computability

* [Introduction](#computability_intro)
* [The halting problem](#halting_topic)
* [Models of computation](#computation_models_topic)


<a name="computability_intro"></a>

##### Introduction


<a name="halting_topic"></a>

##### The halting problem


<a name="computation_models_topic"></a>

##### Models of computation


<a name="heap_class"></a>

###### Heap class implementation in Java

```javascript
public class Heap {

  int size;
  int[] items;
  
  // create empty heap of max capacity n
  public Heap(int n) {
  
    size = 0;
    items = new int[n];
    
  }
  
  // create heap of capacity n containing items from array a
  public Heap(int n, int[] a) {
    
    size = a.length;
    items = new int[n];
    for (int i = 0; i < a.length; i++)
      items[i] = a[i];
    build(); // impose heap property
    
  }
  
}

// build a heap on current items
private void build() {

  // for each non-leaf node in bottom-to-top right-to-left order
  for (int i = (size-1)/2; i >= 0; i--) // start at parent of final leaf
    impose(i);
    
}

// insert item k
public void insert(int k) {
  
  size++;
  int i = size-1; // current position(starting at new leaf node)
  
  while (i > 0 && items[(i-1)/2] < k) {
    items[i] = items[(i-1)/2]; //swap with parent
    i = (i-1)/2; // new position is position of parent
  }
  
  items[i] = k; // finalise location of item

}

// delete and return the max
public int deleteMax() {
  
  int k = items[0]; // root
  items[0] = items[size-1] // swap root with last leaf
  size--;
  impose(0); // on bad value in root
  return k;
  
}

// impose property on node i
private void impose(int i) {
  
  int temp = items[i];
  int current = i;
  boolean finished = false;
  
  while (2*current+1 < size && !finished) {
  
    // find larger child
    int next = 2*current+1; // assume left child first
    if (next+1 < size && items[next+1] > items[next])
      next++; // change if right exists and is larger
    if (temp < items[next]) { // bad node
      items[current] = items[next]; // swap
      current = next; // new position
    }
    else finished = true; // not bad node
  }
  
  items[current] = temp; // finalise location

}
```
<a name="heap_sort"></a>

###### Heapsort pseudocode

* **Build** sequence into a heap; // O(n)  
   * for (int k = 0; k < n-1; k++)
   * // invariant: items 0,...,n-k-1 form a heap  
   * // invariant: items n-k,...,n-1 are sorted  
   * **Find** the largest unsorted item; // is in position 0, so O(1)  
   * **Swap** it into position n-1-k; // its correct place O(1)  
   * **Reduce** the size of the heap by 1; // O(1)  
   * **Impose** the heap property on position 0; // this is O(log n)   
* **Restore** size to original value; 

Loop is iterated `n - 1` times  
   Each iteration takes O(log n) time

<a name="radix_sort"></a>

###### Radix sort pseudocode

```javascript
private int bits(Item x, int b, int p) // helper method which would return the value represented by the b bits of x when starting at position p

// a is the sequence to be sorted
// m is the number of bits in each item of a
// b is the block length of radix sort

int numIterations = m/b;
int numBuckets = (int) Math.pow(2, b);

ArrayList<Item> a = new ArraList<>(); // sequence a

// representing the buckets
ArrayList<Item>[] bucket = new ArrayList[numBuckets];
for (int i = 0; i < numBuckets; i++) bucket[i] = new ArrayList<Item>();

for (int i = 1; i <= numIterations; i++) {

  // clear buckets
  for (int j = 0; j < numBuckets; j++) bucket[j].clear();
  
  // distribute items in order
  for (Item x : a) {
    int k = bits(x, b, (i-1)*b); // find correct bucket
	bucket[k].add(x);
  }
  
  a.clear(); // clear sequence
  
  // concatenate buckets in order
  for (j = 0; j < numBuckets; j++) a.addAll(bucket[j]);
  
}
```

<a name="trie_alg"></a>

###### Tries

**Search:**

```javascript
// search for a word w in a trie t
Node n = root of t;
int i = 0; // current position in w

while (true) {
  if (n has a child c labelled w.charAt(i)) {
    // if can match the char of word in the current position
    if (i == w.length()-1) { // end of word
	  if (c is an "intermediate" node) return "absent";
	  else return "present";
	}
	else { // not at end of word
	  n = c; // move to child
	  i++; // move to next char
	}
  }
  else return "absent"; // can't match current char
}
```

**Insert:**

```javascript
// insert word w into trie t
Node n = root of t;

for (int i = 0; i < w.length(); i++) { // go through chars of word
  if (n has no child c labelled w.charAt(i)) {
    create such a child c;
	mark c as intermediate;
  }
  n = c; // move to child node
}
mark n as representing a word;
```

<a name="trie_class"></a>

###### Trie class

```javascript
public class Node {

  private char letter; // label of incoming branch
  private boolean isWord; // true when node represents a word
  private Node sibling; // next sibling
  private Node child; // first child
  
  public Node(char c) {
  
    letter = c;
	isWord = false;
	sibling = null;
	child = null;
	
  }
  // include accessors and mutators for the various components of a class
}

public class Trie {

  private Node root;
  
  public Trie() {
    root = new Node(Character.MIN_VALUE);
  }
  
}
```

<a name="huff_contruct"></a>

###### Huffman tree construction

```javascript
// set up leaf nodes
for (each distinct char c occuring in the file) {

  make a new parentless node n;
  int f = frequency count for c;
  n.setWeight(f);
  n.setCharacter(c);
  n.setLeftChild(null);
  n.setRightChild(null);
  
}

// construct branch nodes and links
while (num of parentless nodes > 1) {

  make a new parentless node z;
  x, y = the 2 parentless nodes of minimum weight;
  z.setLeftChild(x);
  z.setRightChild(y);
  int w = x.getWeight() + y.getWeight();
  z.setWeight(w);
  
}
// the final z is root
```

<a name="lzw"></a>

###### LZW compression

```javascript
set current text position i to 0;
initialise codeword length k;
initialise dictionary d;

while (text t is not exhausted) {
  
  identify longest string s, starting at position i of the text that is represented in d;
  output codeword for s; // using k bits
  
  // move to next position in t
  i += s.length(); // move forward by the length of the string just encoded
  c = char at position i in t; // char in next position
  
  add string s+c to d, paired with next available codeword; // involves adding a new leaf node if d is represented by a trie
  
}
```

<a name="lzw_decomp"></a>

###### LZW decompression

```javascript
initialise codeword length k;
initialise dictionary d;

read first codeword x from the compressed file f; // read k bits
String s = d.lookUp(x); // look up codeword in d
output s; // output decompressed string

while (f is not exhausted) {

  String oldS = s.clone(); // copy last string decompressed
  
  if (d is full) k++;
  
  get next codeword x from f;
  s = d.loopUp(x); // look up codeword in d
  output s; // output decompressed string
  
  String newS = oldS + s.charAt(0); // string to add to d
  add newS to d paired with next available codeword;

}
```

<a name="brute_force"></a>

###### Brute force algorithm

```javascript
// return smallest k such that s occurs in t starting at position k, or -1 if no k exists
public int bruteForce(char[] t, char[] s) {
  int m = s.length; // length of string/pattern
  int n = t.length; // length of text
  int sp = 0; // starting position in t
  int i = 0; // curr position in t
  int j = 0; // curr position in s
  
  while (sp <= n-m && j < m) { // not reached end
    if (t[i] == s[j]) { // chars match
	  i++; // move on in t
	  j++ // move on in s
	} else {
	  j = 0; // start again in s
	  sp++; // advance starting position
	  i = sp; // back up in text to new starting position
	}
  }
  
  if (j == m) return sp;
  else return -1;
  
}
```

<a name="kmp"></a>

###### KMP search implementation

```javascript
// return smallest k such that s occurs from position k in t, or -1 if no k exists
public int kmp(char[] t, char[] s) {
  
  int m = s.length;
  int n = t.length;
  int i = 0;
  int j = 0;
  int [] b = new int[m]; // create border table
  
  setUp(b); // set up border table
  
  while (i < n) { // not reached end of text
  
    if ([i] == s[j]) { // positions match
	  i++; // move on in text
	  j++; // move on in string
	  if (j = m) return i - j; // reached end of string so a match
	} else { // mismatch so adjust curr position in string using border table
	  if (b[j] > 0) j = b[j]; // if there is a common prefix/suffix then change position in string
	  else { // no common prefix/suffix
	    if (j = 0) i++; // then move forward 1 position in text if not advanced
		else j = 0; // else start from beginning of string
	  }
	}
  
  }
  
  return -1; // no occurence
  
}
```

<a name="bm"></a>

###### Boyer-Moore implementation

```javascript
// return smallest k such that s occurs at k in t, or -1 if no k exists
public int bm(char[] t, char[] s) {

  int m = s.length;
  int n = t.length;
  int sp = 0;
  int i = m-1; // pos in text
  int j = m-1; // pos in string
  // declare a suitable array p
  setUp(s, p); // set up last occurence array
  
  while (sp <= n-m && j >= 0) {
  
    if (t[i] == s[j]) { // match
	  i--; // move back in text
	  j--; // move back in string
	} else {
	  sp += max(1, j - p[t[i]]);
	  i += m - min(j, 1 + p[t[i]]);
	  j = m - 1; // return to end of string
	}
  
  }

  if (j < 0) return sp;
  else return -1;

}
```

<a name="adjacency_list"></a>

###### Adjacency list implementation

```javascript
// an entry in the adjacency list
public class AdjListNode {

  private int vertexIndex;
  // possibly other fields eg weight, capacity...
  
  public AjdListNode(int i) {
    vertexIndex = i;
  }
  
  public int getVertexIndex() {
    return vertexIndex;
  }
  public void setVertexIndex(int i) {
    vertexIndex = i;
  }

}

// a vertex
import java.util.LinkedList;
public class Vertex {

  private int index; // the index of this vertex
  private LinkedList<AjdListNode> adjList; // and its adjacency list
  // possibly other fields eg storing data
  
  public Vertex(int i) {
    adjList = new LinkedList<AjdListNode>();
	index = i;
  }
  
  public int getIndex() {
    return index;
  }
  public void setIndex(int n) {
    index = n;
  }
  // add vertex with index m to the adj list
  public void addToAdjList(int m) {
    adjList.addLast(new AjdListNode(m));
  }
  public int vertexDegree() {
    return adjList.size();
  }

}

// a graph
import java.util.LinkedList;
public class Graph {

  private Vertex[] vertices;
  private int numVertices = 0;
  // possibly other fields for graph properties
  
  // create graph with vertices indexed 0,..., n-1
  public Graph(int n) {
    numVertices = n;
	vertices = new Vertex[n];
	for (int i = 0; i < n; i++) vertices[i] = new Vertex(i);
  }
  
  public int size() {
    return numVertices;
  }

}
```

<a name="dfs"></a>

###### Depth-first search implementation

Add this to the previously defined **vertex** class:  
   ```javascript
   private boolean visited;
   private int pred; // index of predecessor vertex
   
   public boolean getVisited() {
     return visited;
   }
   public void setVisited(boolean b) {
     visited = b;
   }
   public int getPred() {
     return pred;
   }
   public void setPred(int i) {
     pred = i;
   }
   ```

And add this to the previously defined **graph** class:  
   ```javascript
   // visit vertex v with predecessor p
   private void visit(Vertex v, int p) {
   
     v.setVisited(true); // update
	 v.setPred(p); // set predecessor (-1 if none)
	 LinkedList<AdjListNode> L = v.getAjdList(); // get adj. list
	 
	 for (AdjListNode node : L) { // go through all adjacent vertices
	   int i = node.getIndex();
	   if (!vertices[i].getVisited()) visit(vertices[i], v.getIndex()); // if current vertex hasn't been visited, continue the search from there
	 }
	 
   }
   
   // carry out a df traversal
   public void dfs() {
   
     for (Vertex v : vertices) v.setVisited(false); // initialise
	 for (Vertex v : vertices) if (!v.getVisited()) visit(v, -1); // if vertex not visited, start search there
   
   }
   ```
   
<a name="bfs"></a>

###### Breadth-first search implementation

```javascript
for (Vertex v : vertices) v.setVisited(false); // initialise
LinkedList<Vertex> queue = new LinkedList<>();
for (Vertex v : vertices) {

  if (!v.getVisited()) { // start search
  
    v.setVisited(true); // now visited
	v.setPredecessor(-1); // v initial vertex
	queue.add(v); // ready to be processed
	
	while (!queue.isEmpty()) {
	
	  Vertex u = queue.remove(); // get next vertex to process
	  LinkedList<AdjListNode> list = u.getAdjList(); // get its adj. list
	  
	  for (AdjListNode node : list) { // go through its adj. list
	  
	    Vertex w = vertices[node.getVertexIndex()]; // next vertex in list
		if (!w.getVisited()) {
		  
		  w.setVisited(true); // now visited
		  w.setPredecessor(u.getIndex()); // set predecessor of w to be u
		  queue.add(w); // add to queue
		  
		}
	  
	  }
	
	}
  
  }

}
```

<a name="dijkstra"></a>

###### Dijkstra's algorithm implementation

```javascript
// S is set of vertices for which shortest path from u is known
// d(w) is length of a shortest path from u to w passing only through vertices of S
S = {u}; // initialise S
for (each vertex w) d(w) = wt(u, w); // initialise distances

while (S != V) { // still vertices to add in S

  find v not in S with d(v) minimum;
  add v to S;
  for (each w not in S and adjacent to v) d(w) = min{ d(w), d(v) + wt(v, w) }; // perfom relaxation

}
```

<a name="non_deterministic"></a>

###### Graph colouring - example of a non-deterministic alg.

```javascript
// return true if graph g is k-colourable
boolean nDGC(Graph g, int k) {

  for (each vertex v : g) v.setColour(nonDeterministicChoice(k)); // guess a colour for each vertex
  
  for (each edge {u,v} : g)
    if (u.getColour() == v.getColour()) return false; // verify the colouring
  return true;

}
```

<a name="prim_jarnik"></a>

###### Prim-Jarnik algorithm pseudocode

```javascript
set an arbitrary vertex r to be a tree-vertex (tv)
set all other vertices to be non-tree-vertices (ntv)

while (size of ntv > 0) {

  find edge e = {p, q} of graph such that
    p is a tv;
	q is an ntv;
	wt(e) is minimised;
  adjoin edge e to the spanning tree;
  make q a tv;

}
```

<a name="dijkstra_refinement"></a>

###### Dijkstra's refinement to the Prim-Jarnik algorithm

```javascript
set an arbitrary vertex r to be a tree-vertex (tv)
set all other vertices to be non-tree-vertices (ntv)

for (each ntv s) set s.bestTV = r; // r is the only tv

while (size of ntv > 0) {

  find ntv q for which wt( {q, q.bestTV} ) is minimal;
  adjoin {q, q.bestTV} to the tree;
  make q a tv;
  for (each ntv s) update s.bestTV; // update as tv set changed

}
```

<a name="topological_ordering"></a>

###### Topological ordering algorithm

```javascript
// assume each vertex has 2 integer attributes, label and count
// count is the number of incoming edges from unlabelled vertices

for (each vertex v) v.setCount(v.getInDegree());
set up empty sourceQueue

for (each vertex v) if (v.getCount() == 0) add v to sourceQueue; // add vertices with no incoming edges

int nextLabel = 1; // to give the topological order
while (sourceQueue !empty) {

  take v from sourceQueue;
  v.setLabel(nextLabel++); // label the vertex
  for (each w with (v, w) in E) {
  
    w.setCount(w.getCount() - 1); // update attribute count
	if (w.getCount() == 0) add w to sourceQueue; // add vertex if no incoming vertices
  
  }

}
```