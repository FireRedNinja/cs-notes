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
becomes
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
```



[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com
