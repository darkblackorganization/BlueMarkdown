
### hello.c {.row-span-2}

```c
#include <stdio.h>

int main(void) {
  printf("Hello World!\n");

  return 0;
}
```

Compile `hello.c` file with `gcc`

```bash
$ gcc -Wall -g hello.c -o hello
```

Run the compiled binary `hello`

```bash
$ ./hello
```

Output => Hello World!

### Variables {.row-span-2}

```c
int myNum = 15;

int myNum2; // do not assign, then assign
myNum2 = 15;

int myNum3 = 15; // myNum3 is 15
myNum3 = 10;     // myNum3 is now 10

float myFloat = 5.99; // floating point number
char myLetter = 'D';  // character

int x = 5;
int y = 6;
int sum = x + y; // add variables to sum

// declare multiple variables
int a = 5, b = 6, c = 50;
```

### Constants

```c
const int minutesPerHour = 60;
const float PI = 3.14;
```

Best Practices

```c
const int BIRTHYEAR = 1980;
```

### Comment

```c
// this is a comment
printf("Hello World!\n"); // Can comment anywhere in file

/*Multi-line comment, print Hello World!
to the screen, it's awesome */
```

### Print text

```c
printf("I am learning C.\n");
int testInteger = 5;
printf("Number = %d\n", testInteger);

float f = 5.99; // floating point number
printf("Value = %f\n", f);

short a = 0b1010110; // binary number
int b = 02713; // octal number
long c = 0X1DAB83; // hexadecimal number

// output in octal form
printf("a=%ho, b=%o, c=%lo\n", a, b, c);
// output => a=126, b=2713, c=7325603

// Output in decimal form
printf("a=%hd, b=%d, c=%ld\n", a, b, c);
// output => a=86, b=1483, c=1944451

// output in hexadecimal form (letter lowercase)
printf("a=%hx, b=%x, c=%lx\n", a, b, c);
// output => a=56, b=5cb, c=1dab83

// Output in hexadecimal (capital letters)
printf("a=%hX, b=%X, c=%lX\n", a, b, c);
// output => a=56, b=5CB, c=1DAB83
```

### Control the number of spaces

```c
int a1 = 20, a2 = 345, a3 = 700;
int b1 = 56720, b2 = 9999, b3 = 20098;
int c1 = 233, c2 = 205, c3 = 1;
int d1 = 34, d2 = 0, d3 = 23;

printf("%-9d %-9d %-9d\n", a1, a2, a3);
printf("%-9d %-9d %-9d\n", b1, b2, b3);
printf("%-9d %-9d %-9d\n", c1, c2, c3);
printf("%-9d %-9d %-9d\n", d1, d2, d3);
```

output result

```bash
20        345       700
56720     9999      20098
233       205       1
34        0         23
```

In `%-9d`, `d` means to output in `10` base, `9` means to occupy at least `9` characters width, and the width is not
enough to fill with spaces, `-` means left alignment

### Strings

```c
char greetings[] = "Hello World!";
printf("%s", greetings);
```

Access string

```c
char greetings[] = "Hello World!";
printf("%c", greetings[0]);
```

Modify string

```c
char greetings[] = "Hello World!";
greetings[0] = 'J';

printf("%s", greetings);
// prints "Jello World!"
```

Another way to create a string

```c
char greetings[] = {'H','e','l','l','\0'};

printf("%s", greetings);
// print "Hell!"
```

Creating String using character pointer (String Literals)

```c
char *greetings = "Hello";
printf("%s", greetings);
// print "Hello!"
```

**NOTE**: String literals might be stored in read-only section of memory. Modifying a string literal invokes undefined
behavior. You can't modify it!

`C` **does not** have a String type, use `char` type and create an `array` of characters

### Condition {.row-span-2}

```c
int time = 20;
if (time < 18) {
  printf("Goodbye!\n");
} else {
  printf("Good evening!\n");
}
// Output -> "Good evening!"
int time = 22;
if (time < 10) {
  printf("Good morning!\n");
} else if (time < 20) {
  printf("Goodbye!\n");
} else {
  printf("Good evening!\n");
}
// Output -> "Good evening!"
```

### Ternary operator {.col-span-2}

```c
int age = 20;
(age > 19) ? printf("Adult\n") : printf("Teenager\n");
```

### Switch

```c
int day = 4;

switch (day) {
  case 3: printf("Wednesday\n"); break;
  case 4: printf("Thursday\n"); break;
  default:
    printf("Weekend!\n");
}
// output -> "Thursday" (day 4)
```

### While Loop

```c
int i = 0;

while (i < 5) {
  printf("%d\n", i);
  i++;
}
```

**NOTE**: Don't forget to increment the variable used in the condition, otherwise the loop will never end and become an
"infinite loop"!

### Do/While Loop

```c
int i = 0;

do {
  printf("%d\n", i);
  i++;
} while (i < 5);
```

### For Loop

```c
for (int i = 0; i < 5; i++) {
  printf("%d\n", i);
}
```

### Break out of the loop Break/Continue {.row-span-2}

```c
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    break;
  }
  printf("%d\n", i);
}
```

Break out of the loop when `i` is equal to `4`

```c
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    continue;
  }
  printf("%d\n", i);
}
```

Example to skip the value of `4`

### While Break Example

```c
int i = 0;

while (i < 10) {
  if (i == 4) {
    break;
  }
  printf("%d\n", i);

  i++;
}
```

### While continue example

```c
int i = 0;

while (i < 10) {
  i++;

  if (i == 4) {
    continue;
  }
  printf("%d\n", i);
}
```

### Arrays {.row-span-2}

```c
int myNumbers[] = {25, 50, 75, 100};

printf("%d", myNumbers[0]);
// output 25
```

Change array elements

```c
int myNumbers[] = {25, 50, 75, 100};
myNumbers[0] = 33;

printf("%d", myNumbers[0]);
```

Loop through the array

```c
int myNumbers[] = {25, 50, 75, 100};
int i;

for (i = 0; i < 4; i++) {
  printf("%d\n", myNumbers[i]);
}
```

Set array size

```c
// Declare an array of four integers:
int myNumbers[4];

// add element
myNumbers[0] = 25;
myNumbers[1] = 50;
myNumbers[2] = 75;
myNumbers[3] = 100;
```

### Enumeration Enum {.col-span-2}

```c
enum week { Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun };
```

Define enum variable

```c
enum week a, b, c;
enum week { Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun } a, b, c;
```

With an enumeration variable, you can assign the value in the list to it

```c
enum week { Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun };
enum week a = Mon, b = Wed, c = Sat;
// or
enum week{ Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun } a = Mon, b = Wed, c = Sat;
```

### Enumerate sample applications

```c
enum week {Mon = 1, Tues, Wed, Thurs} day;

scanf("%d", &day);

switch(day) {
  case Mon: puts("Monday"); break;
  case Tues: puts("Tuesday"); break;
  case Wed: puts("Wednesday"); break;
  case Thurs: puts("Thursday"); break;
  default: puts("Error!");
}
```

### User input

```c
// Create an integer variable to store the number we got from the user
int myNum;

// Ask the user to enter a number
printf("Enter a number: ");

// Get and save the number entered by the user
scanf("%d", &myNum);

// Output the number entered by the user
printf("The number you entered: %d\n", myNum);
```

### User input string

```c
// create a string
char firstName[30];
// Ask the user to enter some text
printf("Enter your name: ");
// get and save the text
scanf("%s", &firstName);
// output text
printf("Hello %s.\n", firstName);
```

### memory address

When a variable is created, it is assigned a memory address

```c
int myAge = 43;

printf("%p", &myAge);
// Output: 0x7ffe5367e044
```

To access it, use the reference operator (`&`)

### create pointer

```c
int myAge = 43; // an int variable
printf("%d\n", myAge); // output the value of myAge(43)

// Output the memory address of myAge (0x7ffe5367e044)
printf("%p\n", &myAge);
```

### pointer variable {.col-span-2}

```c
int myAge = 43; // an int variable
int*ptr = &myAge; // pointer variable named ptr, used to store the address of myAge

printf("%d\n", myAge); // print the value of myAge (43)

printf("%p\n", &myAge); // output the memory address of myAge (0x7ffe5367e044)
printf("%p\n", ptr); // use the pointer (0x7ffe5367e044) to output the memory address of myAge
```

### Dereference

```c
int myAge = 43; // variable declaration
int*ptr = &myAge; // pointer declaration

// Reference: output myAge with a pointer
// memory address (0x7ffe5367e044)
printf("%p\n", ptr);
// dereference: output the value of myAge with a pointer (43)
printf("%d\n", *ptr);
```

## Operators

### Arithmetic Operators

```c
int myNum = 100 + 50;
int sum1 = 100 + 50; // 150 (100 + 50)
int sum2 = sum1 + 250; // 400 (150 + 250)
int sum3 = sum2 + sum2; // 800 (400 + 400)
```

---

| Operator | Name      | Example |
| -------- | --------- | ------- |
| `+`      | Add       | `x + y` |
| `-`      | Subtract  | `x - y` |
| `*`      | Multiply  | `x * y` |
| `/`      | Divide    | `x / y` |
| `%`      | Modulo    | `x % y` |
| `++`     | Increment | `++x`   |
| `--`     | Decrement | `--x`   |

### Assignment operator

| Example              | As                        |
| -------------------- | ------------------------- |
| x `=` 5              | x `=` 5                   |
| x `+=` 3             | x `=` x `+` 3             |
| x `-=` 3             | x `=` x `-` 3             |
| x `*=` 3             | x `=` x `*` 3             |
| x `/=` 3             | x `=` x `/` 3             |
| x `%=` 3             | x `=` x `%` 3             |
| x `&=` 3             | x `=` x `&` 3             |
| x <code>\|=</code> 3 | x `=` x <code>\|</code> 3 |
| x `^=` 3             | x `=` x `^` 3             |
| x `>>=` 3            | x `=` x `>>` 3            |
| x `<<=` 3            | x `=` x `<<` 3            |

### Comparison Operators

```c
int x = 5;
int y = 3;

printf("%d", x > y);
// returns 1 (true) because 5 is greater than 3
```

---

| Symbol | Name                     | Example  |
| ------ | ------------------------ | -------- |
| `==`   | equals                   | x `==` y |
| `!=`   | not equal to             | x `!=` y |
| `>`    | greater than             | x `>` y  |
| `<`    | less than                | x `<` y  |
| `>=`   | greater than or equal to | x `>=` y |
| `<=`   | less than or equal to    | x `<=` y |

Comparison operators are used to compare two values

### Logical Operators {.col-span-2}

| Symbol            | Name          | Description                                   | Example                       |
| ----------------- | ------------- | --------------------------------------------- | ----------------------------- |
| `&&`              | `and` logical | returns true if both statements are true      | `x < 5 && x < 10`             |
| <code>\|\|</code> | `or` logical  | returns true if one of the statements is true | <code>x < 5 \|\| x < 4</code> |
| `!`               | `not` logical | Invert result, return false if true           | `!(x < 5 && x < 10)`          |

{.show-header}

### Operator Examples {.row-span-2}

```c
unsigned int a = 60; /*60 = 0011 1100 */
unsigned int b = 13; /*13 = 0000 1101 */
int c = 0;

c = a & b; /*12 = 0000 1100 */
printf("Line 1 -the value of c is %d\n", c);

c = a | b; /*61 = 0011 1101 */
printf("Line 2 -the value of c is %d\n", c);
c = a ^ b; /*49 = 0011 0001 */
printf("Line 3 -the value of c is %d\n", c);
c = ~a; /*-61 = 1100 0011 */
printf("Line 4 -The value of c is %d\n", c);
c = a << 2; /*240 = 1111 0000 */
printf("Line 5 -the value of c is %d\n", c);
c = a >> 2; /*15 = 0000 1111 */
printf("Line 6 -The value of c is %d\n", c);
```

### Bitwise operators {.col-span-2}

| Operator        | Description                                                     | Instance                                              |
| :-------------- | :-------------------------------------------------------------- | :---------------------------------------------------- |
| `&`             | Bitwise AND operation, "AND" operation by binary digits         | `(A & B)` will get `12` which is 0000 1100            |
| <code>\|</code> | Bitwise OR operator, "or" operation by binary digit             | <code>(A \| B)</code> will get`61` which is 0011 1101 |
| `^`             | XOR operator, perform "XOR" operation by binary digits          | `(A ^ B)` will get `49` which is 0011 0001            |
| `~`             | Inversion operator, perform "inversion" operation by binary bit | `(~A)` will get `-61` which is 1100 0011              |
| `<<`            | binary left shift operator                                      | `A << 2` will get `240` which is 1111 0000            |
| `>>`            | binary right shift operator                                     | `A >> 2` will get `15` which is 0000 1111             |

{.show-header}

## Data Types

### Basic data types {.col-span-2}

| Data Type            | Size             | Range                              | Description                         |
| -------------------- | ---------------- | ---------------------------------- | :---------------------------------- |
| `char`               | 1 byte           | `−128` ~ `127`                     | single character/alphanumeric/ASCII |
| `signed char`        | 1 byte           | `−128` ~ `127`                     |                                     |
| `unsigned char`      | 1 byte           | `0` ~ `255`                        |                                     |
| `int`                | `2` to `4` bytes | `−32,768` ~ `32,767`               | store integers                      |
| `signed int`         | 2 bytes          | `−32,768` ~ `32,767`               |                                     |
| `unsigned int`       | 2 bytes          | `0` ~ `65,535`                     |                                     |
| `short int`          | 2 bytes          | `−32,768` ~ `32,767`               |                                     |
| `signed short int`   | 2 bytes          | `−32,768` ~ `32,767`               |                                     |
| `unsigned short int` | 2 bytes          | `0` ~ `65,535`                     |                                     |
| `long int`           | 4 bytes          | `-2,147,483,648` ~ `2,147,483,647` |                                     |
| `signed long int`    | 4 bytes          | `-2,147,483,648` ~ `2,147,483,647` |                                     |
| `unsigned long int`  | 4 bytes          | `0` ~ `4,294,967,295`              |                                     |
| `float`              | 4 bytes          | `3.4E-38` ~ `3.4E+38`              |                                     |
| `double`             | 8 bytes          | `1.7E-308` ~ `1.7E+308`            |                                     |
| `long double`        | 10 bytes         | `3.4E-4932` ~ `1.1E+4932`          |                                     |

{.show-header}

### Data types

```c
// create variables
int myNum = 5; // integer
float myFloatNum = 5.99; // floating point number
char myLetter = 'D'; // string
// High precision floating point data or numbers
double myDouble = 3.2325467;
// print output variables
printf("%d\n", myNum);
printf("%f\n", myFloatNum);
printf("%c\n", myLetter);
printf("%lf\n", myDouble);
```

---

| Data Type | Description                          |
| :-------- | :----------------------------------- |
| `char`    | character type                       |
| `short`   | short integer                        |
| `int`     | integer type                         |
| `long`    | long integer                         |
| `float`   | single-precision floating-point type |
| `double`  | double-precision floating-point type |
| `void`    | no type                              |

### Basic format specifiers

| Format Specifier | Data Type                                             |
| ---------------- | :---------------------------------------------------- |
| `%d` or `%i`     | `int` integer                                         |
| `%f`             | `float` single-precision decimal type                 |
| `%lf`            | `double` high precision floating point data or number |
| `%c`             | `char` character                                      |
| `%s`             | for `strings` strings                                 |

{.show-header}

### Separate base format specifiers

| Format      | Short         | Int         | Long          |
| ----------- | ------------- | ----------- | :------------ |
| Octal       | `%ho`         | `%o`        | `%lo`         |
| Decimal     | `%hd`         | `%d`        | `%ld`         |
| Hexadecimal | `%hx` / `%hX` | `%x` / `%X` | `%lx` / `%lX` |

{.show-header}

### Data format example

```c
int myNum = 5;
float myFloatNum = 5.99; // floating point number
char myLetter = 'D';     // string
// print output variables
printf("%d\n", myNum);
printf("%f\n", myFloatNum);
printf("%c\n", myLetter);
```

## C Preprocessor

### Preprocessor Directives {.row-span-2}

| Directive  | Description                                                          |
| ---------- | :------------------------------------------------------------------- |
| `#define`  | define a macro                                                       |
| `#include` | include a source code file                                           |
| `#undef`   | undefined macro                                                      |
| `#ifdef`   | Returns true if the macro is defined                                 |
| `#ifndef`  | Returns true if the macro is not defined                             |
| `#if`      | Compile the following code if the given condition is true            |
| `#else`    | Alternative to `#if`                                                 |
| `#elif`    | If the `#if` condition is false, the current condition is `true`     |
| `#endif`   | End a `#if...#else` conditional compilation block                    |
| `#error`   | Print an error message when standard error is encountered            |
| `#pragma`  | Issue special commands to the compiler using the standardized method |

{.show-header}

```c
// replace all MAX_ARRAY_LENGTH with 20
#define MAX_ARRAY_LENGTH 20
// Get stdio.h from the system library
#include <stdio.h>
// Get myheader.h in the local directory
#include "myheader.h"
#undef FILE_SIZE
#define FILE_SIZE 42 // undefine and define to 42
```

### Predefined macros {.row-span-2}

| Macro      | Description                                                           |
| ---------- | :-------------------------------------------------------------------- |
| `__DATE__` | The current date, a character constant in the format "MMM DD YYYY"    |
| `__TIME__` | The current time, a character constant in the format "HH:MM:SS"       |
| `__FILE__` | This will contain the current filename, a string constant             |
| `__LINE__` | This will contain the current line number, a decimal constant         |
| `__STDC__` | Defined as `1` when the compiler compiles against the `ANSI` standard |

{.show-header}

`ANSI C` defines a number of macros that you can use, but you cannot directly modify these predefined macros

#### Predefined macro example

```c
#include <stdio.h>

int main(void) {
  printf("File: %s\n", __FILE__);
  printf("Date: %s\n", __DATE__);
  printf("Time: %s\n", __TIME__);
  printf("Line: %d\n", __LINE__);
  printf("ANSI: %d\n", __STDC__);
}
```

### Macro continuation operator (\\)

A macro is usually written on a single line.

```c
#define message_for(a, b) \
    printf(#a " and " #b ": We love you!\n")
```

If the macro is too long to fit on a single line, use the macro continuation operator `\`

### String Constantization Operator (#)

```c
#include <stdio.h>

#define message_for(a, b) \
  printf(#a " and " #b ": We love you!\n")

int main(void) {
  message_for(Carole, Debra);

  return 0;
}
```

When the above code is compiled and executed, it produces the following result:

```
Carole and Debra: We love you!
```

When you need to convert a macro parameter to a string constant, use the string constant operator `#`

### tag paste operator (##)

```c
#include <stdio.h>

#define tokenpaster(n) printf ("Token " #n " = %d\n", token##n)

int main(void) {
  int token34 = 40;
  tokenpaster(34);

  return 0;
}
```

### defined() operator

```c
#include <stdio.h>

#if !defined (MESSAGE)
   #define MESSAGE "You wish!"
#endif

int main(void) {
  printf("Here is the message: %s\n", MESSAGE);

  return 0;
}
```

### Parameterized macros

```c
int square(int
