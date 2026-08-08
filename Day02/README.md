C Memory Fundamentals + Linux Build Process

Pointer 

The stages to compiler :
Preprocessor
Compiler
Assembler
Linker
Object file (.o)
Executable

Memory Layout of C Programs:

High Address ---> Stack
                  Heap
                  Uninitialized Data (BSS)
                  Initialized Data 
Low Address --->  Text

Segments:
1. Text Segment
2. Data Segment
    A. Initialized Data Segment
    B. Uninitialized Data Segment (BSS)
3. Heap Segment
4. Stack Segment

Text    --> Program code
Data    --> Initialized globals
BSS     --> Uninitialized global variables 
Heap    --> malloc( ) memory
Stack   --> Local variable

Memory Layout:

+------------------+
| Stack            |
| Local variables  |
+------------------+

+------------------+
| Heap             |
+------------------+

+------------------+
| Static / Global  |
+------------------+

+------------------+
| Code             |
+------------------+

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Static:

Static local variable
Static global variable
Static function

Static local variable:

| Variable       | Lifetime       |
| -------------- | -------------- |
| Local variable | Function call  |
| Static local   | Entire program |


Static Global variable:

eg :  static int speed = 50; 

this is accessed / Visible only inside an source file which it is being written. 
This is internal linkage.

motor.c  has a var : speed
display.c aslo has a var : speed

If both expose as a global(var) rather than static global(var) : speed, the linker reports multiple definitions.

Making one static keeps it private to its source file.

Static Function :

static void helper(void)
{
}

This function can only be called from the same .c file.

Used for helper functions that are not part of the module's public API.

Example:

uart.c ,      uart_init()


CODE
 ↓
Instructions

STATIC / GLOBAL
 ↓
Lives for program lifetime

STACK
 ↓
Function calls + automatic local variables

HEAP
 ↓
Dynamic runtime memory


Pointer :

& — Address-of operator

* — Dereference operator

p   → address
*p  → value at that address


&  → WHERE?
*  → WHAT?
&x   Where is x?
*p   What is stored at the address p points to?


When used before a variable:

int x = 10;

&x

means:

"Give me the memory address of x."

Imagine:

Variable       Address       Value

   x           0x1000         10
   │
   └───────────────┐
                   │
              memory location

Suppose:

int x = 10;
int *p = &x;

Now:

x
│
├── value = 10
└── address = 0x1000

p
│
└── stores 0x1000

So p contains the address of x.

When we write:

*p

we're saying:

"Go to the address stored inside p and access the value there."

So:

printf("%d", *p);

prints:

10

the      int x = 10;    int *p = &x; 

        &x
         ↓
┌─────────────────┐
│       x         │
│                 │
│ value = 10      │
│ address = 1000  │
└─────────────────┘
         ↑
         │
         p
so;

*p

means:

Go to address 1000 → get 10.


~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Quick test

Given:

int speed = 80;
int *ptr = &speed;

What do these represent?

speed =
&speed =
ptr =
*ptr =

ans:
speed   = 80
&speed  = address of speed
ptr     = address stored in ptr (the address of speed)
*ptr    = value at that address = 80

