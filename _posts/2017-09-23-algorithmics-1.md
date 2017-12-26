---
layout: post
title:  "Algorithmics 1"
date:   2017-09-23 18:50:00
categories: Level3 Semester1
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
* [pseudocode](#heapsort)


#### Sorting Algorithms

   O(n<sup>2</sup>) - selection, insertion, bubble  
   O(n log n) - merge, heap  
   Quicksort is O(n log n) on average (but no better than O(n<sup>2</sup>) in the worst case
   
   
#### Strings and text algorithms

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
<a name="heapsort"></a>

###### Heapsort pseudocode

**Build** sequence into a heap; // O(n)  

for (int k = 0; k < n-1; k++){  
    
   // invariant: items 0,...,n-k-1 form a heap  
      
   // invariant: items n-k,...,n-1 are sorted  
      
   **Find** the largest unsorted item; // is in position 0, so O(1)  
      
   **Swap** it into position n-1-k; // its correct place O(1)  
      
   **Reduce** the size of the heap by 1; // O(1)  
      
   **Impose** the heap property on position 0; // this is O(log n)  
      
   }  
    
**Restore** size to original value; 

* loop is iterated `n - 1` times
* each iteration takes O(log n) time



You'll find this post in your `_posts` directory - edit this post and re-build (or run with the `-w` switch) to see your changes!
To add new posts, simply add a file in the `_posts` directory that follows the convention: YYYY-MM-DD-name-of-post.ext.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com
