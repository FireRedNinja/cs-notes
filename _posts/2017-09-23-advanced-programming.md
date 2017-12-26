---
layout: post
title:  "Advanced Programming"
date:   2017-09-23 18:50:00
categories: Level3 Semester1
---

#### Lecture 1
#### Introduction

##### Application Level
* Java - Strong Types
* Python - Auto Memory Mgt
* Haskel - Abstract Resources
* ... - IDE
<!--excerpt-->

##### Systems Level
* Languages: C, Rust, OCaml
* Used for:
	* OS
	* Communications
	* Numerical
	* Drivers
	* Embedded Systems

* C/C++ most heavily used programming language
* Used in OS and embeded systems


## Edit - Compile - Link - Execute Cycle
* Source Files > Compiler > Bin > Linker > Executable
```bash
gcc -o test test.o
```

## Memory Layout
* Higher Mem address
	* stack
	* heap
	* bss segment
		* stores uninitialized variables
	* data segment
		* initialized data is stord
	* test segment
		*  read-only, holds instructions that the processor understands
* Lower mem adress

* stack & heap shared memory

## Makefiles
* makes compiling bigger programs easier
```bash
gcc -c mod_a.c
gcc -c mod_b.c
gcc -c mod_a.o mod_b.o -o app_x
```
- becomes

```Makefile
app_x: mod_a.o mod_b.o
	gcc mod_a.o mod_b.o -o app_x

mod_a.o: mod_a.c global.h
	gcc -c mod_a.c

mod_b.o: mod_b.c global.g
	gcc -c mod_a.c
```

```
CFLAGS = -W -Wall
%.o : %.c
	gcc -c $(CFLAGS) $< -o $@
OBJECTS = mod_a.o mod_b.o

app_x: $(OBJECTS)
	gcc $(OBJECTS) –o app_x

mod_a.o: mod_a.c global.h
mod_b.o: mod_b.c global.h
```

# Lecture 2
# Overview of C

* Must contain main()
```C
int main(){
	// something
	return 0;
}
```

```C
#include <stdio.h>
printf()
```


* char - 8 bits
* short - 16 bits
* long - 32 bits
* float - 32 bit
* long long - 64 bits
* double - 64-bit<br>

#### printf formatting
* %d - print as a decimal integer
* %6d - print as a decimal integer at least 6 characters wide with leading blanks
* %06d - print as a decimal integer at least 6 characters wide with leading zeros
* %f - print as a floating point number
* %6f - print as a floating point number at least 6 characters wide
* %.2f - print as a floating point number with 2 digits after the decimal point
* %6.2f - print as a floating point number at least 6 characters wide with 2 digits after the decimal point
* %c - print as a character
* %s - print as a string
* %x - print as a hexadecimal integer


```C
while(condition) {
	statement;
}

for (int = i; i < length; ++i) {
	statement;
}
```

```C
//Constant
#define LOWER 0
#define UPPER 300
#define STEP 20
```

```C
// Character input
#include <stdio.h>
...
for (c = getchar(); c!=EOF;c=getchar()){
	statement;
}
// or
while ((c = getchar()) != EOF) {
	statement;
}
```

#### Arrays
```C
int numbers[10];
numbers[4];
```

#### Functions
```C
// Must use prototype before
return-type function-name (parameter declarations, if any);
....
return-type function-name (parameter declarations, if any) {
	statements;
}
```

* call by value
	* manipulate actual values
* call by reference
	* cannot manipulate actual values
* arrays passewd by reference

```C
/// External Variables
extern type varName;
```

* signed
	* can be negative or positive ($2^-(n-1)$ to $2^(n-1)$)
* unsigned
	* always positive or 0

#### escape sequences
```
\a - alert (bell) character
\b - backspace
\f - formfeed
\n - newline
\r - carriage return
\t - horizontal tab
\v - vertical tab
\\ - backslash
\?
\'
\"
\ooo - octal number
\xhh - hexadecimal number
\0 - null character (EOS)
```

* 'x' - integer representing value of letter x
* "x" - array of 2 chars, 'x' and '\0'

```C
// enum
enum months {JAN = 1; FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC};
```

### Variables default initialized
* external
	- 0
* automatic
	- undefined


* "const" can be used with array arguments to functions, to tell the function not to change the array
```C
int strlen(const char[])
```

* Conversion takes place across assignments; the value of the right hand side is converted to the type of the left hand side, which is the type of the result
* Longer integers are converted to shorter ones by dropping the excess high order bits
* float to int conversions cause truncation of any fractional part

#### cast
```c
(type) expression
```

```C
++n // increments before value us used
n++ // increments after value is used
```

#### Bitwise operations
* & - AND
* | - OR
* ^ - EXOR
* << - left shift
* >> - right shift
* ~ - one's complement

```C
n = n & 0xff;
/*sets all bits of n to 0 except the low order 8 bits */
n = n & ~0xff;
/* zeroes the low order 8 bits */
n = n | 0x11;
/* sets bits 0 and 4 to 1, leaving all others alone */
n = n ^ 0x11;
/* if n’s bit 0 has a value of 0, set it to 1; if it is 1, set it to
0; same for bit 4 */
n = n << 2;
/* shift n’s value 2 bits left, filling with 0’s; equivalent to
multiplying by 4 */
n = n >> 3;
/* shift n’s value 3 bits right; if n is signed, fill vacated
bits with the sign bit; if unsigned, fill with 0; equivalent
to division by 8 */
```

```C
x = expr1 ? expr2 : expr3;
// is the same as
if (expr1) {
	x = expr2;
} else {
	x = expr3;
}
```

| Operations | Associativity |
| :------------- | :------------- |
| () [] -> .  | left to right |
| ! ~ ++ -- + - * & (type) sizeof  | right to left |
| * / %  | left to right |
| + -   | left to right |
| << >>  | left to right |
| < <= > >=  | left to right |
| == !=  | left to right |
| & | left to right |
| ^ | left to right |
| \|  | left to right |
| &&  | left to right |
| \|\| | left to right |
| ?; | right to left |
| = += -= *= /= %= &= ^= \|= <<= >>= | right to left |
| ,  | left to right |

# Chapter 3
## Control statements

```C
if (/* condition */) {
	/* code */
} else if (/* condition */) {
	/* code */
} else {
	/* code */
}

while (/* condition */) {
	/* code */
}

for (size_t i = 0; i < count; i++) {
	/* code */
}

do {
	/* code */
} while(/* condition */);

switch (/* expression */) {
	case /* value */:
		/* statement */;
		break;
	default /* value */ :
		/* statement */;
		break;
}

for (. . .)
	for (. . .) {
		. . .
		if (disaster)
			goto error;
		. . .
	}

error:
/* cleanup the mess */
```


# Chapter 4
## Functions

```C
// always use prototypes
return-type name(/* arguments */);

return-type name(/* arguments */) {
	/* code */
	return 0;
}
```

* if funciton doesn't have a type, it is set to int as default

#### Static Variables
```C
static int sp;
// can only use this variable inside the file it's declared in
```
* internal static variables are local to a particular function, just as automatic variables are, but unlike automatics, they remain in existence rather than coming and going each time that the function is activated

#### Register Variables
* The keyword register hints to compiler that a given variable can be put in a register. It’s compiler’s choice to put it in a register or not
* Registers are faster than memory to access, so the variables which are most frequently used in a C program can be put in registers using register keyword

```C
register int x;
int f(register unsigned m, register long n) {…}
```

#### Preprocessor

```C
// file inclusion
#include "filename"
#include <filename>

// macro substitution
#define name replacement-text
// use "\" to continue for multiple lines
#define name replacement-textreplacement-textreplacement-textreplacement-text\
replacement-textreplacement-textreplacement-text\
replacement-textreplacement-textreplacement-text
// ## can concatenate arguments
#define paste(front, back) front ## back
paste(name, 1);
// will give
name1;

// Conditional evaluation
#if
	#endif
	#else
	#elif
// eg
#if SYSTEM == SYSV
	#define HDR “sysv.h”
#elif SYSTEM == BSD
	#define HDR “bsd.h”
#elif SYSTEM == MSDOS
	#define HDR “msdos.h”
#else
	#define HDR “default.h”
#endif /* SYSTEM */
#include HDR


#ifdef
#ifndef
// ifdef/ifndef is the same as checks if contents of a header file is only included once
#if !defined(_HDR_H_)
#define _HDR_H_
/* contents of hdr.h go here */
#endif /*_HDR_H_ */
```

- Automatic variable
	- lives inside function
	- allocated upon function call
	- deallocated upon function return

- External variable
	- lives outside functions
	- allocated upon program start
	- never deallocated

#### Visibility of variables
- As default all top-level names are visible everywhere
- use static to restrict visibility

## Chapter 5
### pointers

```C
// points to a value of type int
int*;
// points to a value of type int*
int**;
```

#### purpose?
- call-by-reference
- linked data structures
- array indexing
- higher order functions - functions that call some of their own arguments


```C
// stores address of int X in P
int *P = &X;

// writes 42 to the address pointed to by P
*P = 42;
```

- & cannot be used for register variables or complex expressions

```C
int x = 1, y = 2;
int z[10];
int *p, *q; /* p and q are pointers to int */

p = &x; /* p now points to x */
y = *p; /* y is now 1 */
*p = 0; /* x is now 0 */
q = &z[3]; /* q now points to z[3] */
p = q; /* p now points to z[3] */
while (p == q) /* loop exits on 1st iter */
	break;
if (p != NULL) /* address of z[3] != 0 */
	p = &z[0]; /* p now points to z[0] */
if (q)
	q = &z[0]; /* q now equals p; */
```

- Use pointers to call by reference
```C
swap(&a[i], &a[j])
// instead of
swap(intx , int y)
```

```C
int a[10];
int *pa;

pa = a; // points to a[0]
pa++; // points to a[1]

// given pointers q, p that points to the same array
q-p; // is the number of array elements between pointers p ad q

//-------------

char amsg[] = "this is a string"; // array of 17 characters including '\0'
char *pmsg = "this is a string" // pointer to an array of the same 17 chars
```

- pmsg can be resized but amsg can't;


#### Memory management

```C
malloc(); // requests given no. of bytes adn returns a void * to the first byte
sizeof(t); // no. of bytes required to store a value of type t

free(); // deallocates memory that was malloced;
```

- given
```bash
./program hello world
```

```C
// in int main(int argc *argv[]);
argc == 3
argv[0] == "./program";
argv[1] == "hello";
argv[2] == "world";
```

#### Function pointers
```C
void sort(char *lineptr[], int left, int right, int (*comp)(void *, void *));
```

## Chapter 7
#### Standard Input and output
```C
#include <stdio.h>

int getchar(void); // read one character at a time
int getchat(); // return next input char, returns EOF on end
int putchar(int ch); // prints ch to stdout
printf(); // prints to stdout
```

#### Formated I/O
```C
// Format string determines type of remaining arguments
int printf(const char *format, ...);
printf("%d\n", 8);

int scanf(char *format, ...); // same as printf formatting
int day, year;
char monthname[20];
scanf(“%d %s %d”, &day, monthname, &year);
```

| Character | Input Data |
| :------------- | :------------- |
| d | decimal int |
| i  | integer. integer may be octal(leading 0) or hexadecimal(leading 0x/0X)  |
| o   | octal int(with/without leading 0)  |
| u  | unsigned int  |
| x  | hexadecimal int  |
| c  | char  |
| s  | string  |
| e,f,g  | floating point with optional sight/decimal point/exponential  |
| %   | literal %, no assignment is made |

#### File I/O
```C
FILE *fopen(char *name, char *mode);
int getc(FILE *fp);
int putc(int c, FILE *fp);
int fclose(FILE *fp);

// printf and scanf variants
int fscanf(FILE *fp, char *format, ...);
int fprintf(FILE *fp, char *format, ...);

// line buffered input/output
char *fgets(char *line, int maxline, FILE *fp);
int fputs(char *line, FILE *fp);
```

## Chapter 6
#### Structs
```C
struct [tag] {
	member declarations
};

struct point {
	int x;
	int y;
};

struct point p = {320, 200};
struct point q;
struct point *r;

q = p; // struct assignment
r = &q; // address of struct variable q

q.y; // access struct member y
r->x; // dereference
```

- Legal Operations
	- copying
	- passing to a function
	- returning from a function
	- taking the address with &
	- accessing members
	- assigning to members
- Illegal Operations
	- arithmetic
	- comparisons

#### Self-referential structs
```C
struct tnode {
	int value; // payload
	struct tnode *left; // ptr to left child
	struct tnode *right; // ptr to right child
};

struct tnode *;
```
#### Typedefs
- create new data type synonyms
```C
typedef type synonym;
```
```C
typedef int Length; // Length is synonym for int
typedef char *String; // String is synonym for char *

Length len, maxlen; // Length variables
Length *lengths; // ptr to (array of) Length
String lineptr[MAXLINES]; // array of String
Length strlen(String s); // prototype
```

#### Unions
- Variable that may hold objects of different types and sizes
```C
union const_value { // type declaration
	int ival;
	double dval;
	char *sval;
};
union const_value val; // variable definition
```
- assignment to any union member turns all other members into garbage
- compiler doesn't track this

#### Differences between Java and C
- Interface support
	- Java compiler checks that a class implements its interface
	- C compiler doesn't check that .c file defines what .h declares
- Memory management
	- Java garbage collector
	- In C unused memory mused be freed explicitly
- Memory protection
	- Java - private attributes cannot be tampered with
	- Pointers to opaque structs can still be dereferenced
		- never leak pointers to internal data structures, for security reasons.

## Threads and Concurrency
*Concurency* means multiple computations are happening at the same time.

#### Process
A *process* is an instance of a running program that is isolated from other processes on the same machine. In particular, it has its own private section of the machine’s memory.


- Processes has:
	- An address space
	- A collection of OS state
	- A CPU context - a thread of control

#### Threads
A *thread* is a locus of control inside a running program. Think of it as a place in the program that is being run, plus the stack of method calls that led to that place (so the thread can go back up the stack when it reaches return statements).

- Why use threads?
	- Split program into routines to execute in parallel

- Shares a process address space with >= 0 threads

#### Thread Models
- Manager/Worker
	- Manager handles I/O and assignes work to worker threads
- Peer
	- similar to manager/worker, but after the main thread creates other threads it participates in the work
- Pipeline
	- Each thread handles a different stage of an assemply line
	- Threads hand word to each other in producer-consumer relationship



## Generic Threading Concepts

## Java support for multi-threading

## PThreads

## Thread Safe ADTs

## Memory Management

## OpenMP

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com
