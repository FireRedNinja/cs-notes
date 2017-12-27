---
layout: post
title:  "Algorithmics 1"
date:   2017-12-26 18:50:00
categories: Level3 Semester1
author: dasha
---


#### Introduction


##### Useful Textbooks

* M.T. Goodrich & R. Tamassia, Algorithm Design: Foundations, Analysis, and Internet Examples, Wiley, 2002
* D. Harel & Y. Feldman, Algorithmics: the Spirit of Computing, Addison Wesley, 2004 (also earlier 1992 edition by D. Harel)
* M. Sipser, Introduction to the Theory of Computation, Course Technology, 2006
<!--excerpt-->

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


#### Fundamental Algorithms and Data Structures

* Stacks, queues and priority queues
* Complete binary trees
* Heaps and heap operations
* Java class for (integer) heaps
* Heap sort

##### Stack abstract data type (LIFO)

**Basic operations:**

* *create*
* *isEmpty*
* *push* (to top of stack)
* *pop* (delete and return from top of stack)

**Represent it as:**

* an array - all operations are O(1)
* a linked list - all operations are O(1)

##### Queue abstract data type (FIFO)

**Basic operations:**

* *create*
* *isEmpty*
* *insert* (to the back of queue)
* *delete* (delete and return item at front of queue)

**Represent it as:**

* an array - all operations are O(1) and it must be "wrapped around", treated as circular
* a linked list - all operations are O(1)

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

##### An integer heap class

Represent using an array, where:

* children of a node `i` are in the array at `2i + 1` and `2i + 2` 
* parent of a node `i` are in the array at `(i - 1) / 2` (floored automatically in Java)

Heap class [implementation in Java](#heap_class)

##### Heap Sort

* more efficient than selection sort
* O(n log n) in the worst case
* [pseudocode](#heap_sort)


#### Sorting Algorithms

   O(n<sup>2</sup>) - selection, insertion, bubble  
   O(n log n) - merge, heap  
   Quicksort is O(n log n) on average (but no better than O(n<sup>2</sup>) in the worst case
   
##### Comparison-based sorting

   **Claim:** No sorting algorithm that is based on pairwise comparison can be better than O(n log n) in the worst case  
   **Justification:** Draw out the algorithm using a binary decision tree, where each node represents a comparison between two elements

* leaf nodes represent the possible outcomes of the algorithm
* so the number of leaf nodes = the possible ordering of `n` items
* so there are at least `n!` and maximum 2<sup>h+1</sup> leaf nodes
* its worst case complexity is O(h) where `h` = its height
* it follows that n! <= 2<sup>h+1</sup>

<img src="/cs-notes/assets/images/decision_tree.png" nopin="nopin" />

   Reversing inequality and taking log<sub>2</sub> of both sides:
   
<img src="/cs-notes/assets/images/comparison_based_complexity.png" nopin="nopin" />

   Giving a complexity of O(n log n) as required

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

##### Tries

* stored items have a key that is interpreted as a sequence of bits/characters
* there is a multiway branch at each node where each branch has an associated symbol
* no two siblings have the same symbol
* the branch to be taken at level `i` is determined by the `i`<sup>th</sup> element of the key
* tracing a path from root to a node spells out the key of the item
* eg, used to store strings

<img src="/cs-notes/assets/images/trie.png" nopin="nopin" />

*Search* and *insert* algorithms for the trie found [here](#trie_alg)

**Represent it as:**

* an array of pointers, which represent children
* linked lists, containing children of each node

<img src="/cs-notes/assets/images/trie_list.png" nopin="nopin" />

[Example](#trie_class) trie class to represent a dictionary
   
#### Strings and text algorithms

* Text compression
  * Huffman and LZW
* String comparison
  * String difference
* String/pattern search
  * Brute force
  * KMP
  * BM
  
##### Text compression

* lossless
* compression ratio is `x / y` where `x` = compressed and `y` = original
* space saved = `1 - (x / y) * 100%`

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
   
<img src="/cs-notes/assets/images/huffman_1.png" nopin="nopin" />

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

<img src="/cs-notes/assets/images/lzw_1.png" nopin="nopin" />

**LZW variants:**

* constant - fixed capacity dictionary
* dynamic - add 1 to current length whenever dictionary becomes full
* LRU - when full, current string replaces the least recently used string in the dictionary

**LZW decompression:**

* builds same dictionary as compression but **1 step out of phase**
* may encounter codeword that is not in dictionary
  * if (lookup fails) newS = oldS + oldS.charAt(0);
  
LZW decompression [pseudocode](#lzw_decomp)

<img src="/cs-notes/assets/images/lzw_2.png" nopin="nopin" />

**Complexity:** O(n) for comp. and decomp. each

##### String comparison

* given strings `s` and `t` of lengths `m` and `n`, what is the smallest number of basic operations needed to transform `s` into `t`?
* use
  * insertion
  * deletion
  * subsitution
  
**String distance:**

<img src="/cs-notes/assets/images/distance_1.png" nopin="nopin" />

**Prefixes:**

* `i`<sup>th</sup> prefix of string `s` is first `i` chars of `s`
* let `d( i,j )` = distance between prefix `i` of `s` and prefix `j` of `t`
* then distance between `s` and `t` = `d( m,n )` for `len(s) = m` and `len(t) = n`

**Optimal alignment:**

The last position of the alignment must either be of the form  
   <img src="/cs-notes/assets/images/optimal_alignment.png" nopin="nopin" />
   
In other words,  
   <img src="/cs-notes/assets/images/optimal_alignment_alt.png" nopin="nopin" />
   
##### Distance with dynamic programming

* fill in entries of an `m * n` table row by row, and column by column
* time and space complexity = O(mn)
* keep most recent entry in each column of the table
  * space complexity = O(m + n)
  
**Distances table:**

<img src="/cs-notes/assets/images/distance_table.png" nopin="nopin" />

* entries calculated one by one by applying formula above
* final entry `d( 7,8 ) = 4` so string distance is **4**
* trace back to entry `( 0,0 )` to find optimal alignment
  * vertical = deletion
  * horizontal = insertion
  * diagonal = match/substitution
  
##### String/pattern search

Given a text `t` of length `n`, and a string/pattern `s` of length `m`, find the position of the last occurence of `s` in `t`

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
  
<img src="/cs-notes/assets/images/border_table.png" nopin="nopin" />

* `b[j]` is
  * the length of the longest border of `s[0...j-1]`
  * `max { k | s[0...k-1] = s[j-k...j-1] }`
  
**KMP seach :**

* [implementation](#kmp)
* this is O(n) worst case
* naive method requires O(j<sup>2</sup>) steps to find `b[j]`, so O(m<sup>2</sup>) overall
* can be implemented in O(m + n) time (to set up border table and to conduct search)

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

#### Graphs and graph algorithms

#### NP Completeness

#### Computability



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