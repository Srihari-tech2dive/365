C Memory Fundamentals + Linux Build Proces

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
