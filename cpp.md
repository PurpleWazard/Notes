# c++ notes
im following this [**free** corse](https://www.learncpp.com)
# chapter 0 (history)
# chapter 1 (basicly basic) 
> A computer program is a sequence of instructions that tell the computer what to do. A **statement** is a type of instruction that causes the program to perform some action.  

so a statement is a command for a computer to follow.

syntax is like grammer if you misspell a word or statement you get a syntax error.  
using a LSP (lanugae server protocol) will help you solve errors while you are coding not at compile time.  

---
### comments 
comments have nothing to do with the code its just text in the coding file its self. why you compile a file with comments they are ignored complealy.  
```cpp
//i am a regular comment 
/*im a j    uu
multi
line 
comment
*/
```
you can also use comments to "comment out" code for debuging and for fixing problems  
```cpp
int x{};  // you can also put them here too
//int y{};
```
---
### varible assignment 
computer what what is called ram (random access memory) its just abunch of computer chips that can hold **alot** ones and zeros we can store the value of varibles there

when we **declare** a varible the computer will make space for it in the ram the type of the varible will dictate how large the space is and how it is interptied.
there are many ways we can define and declare varibles  
define = saying somthing exsist and explicting saying what it is
declare = saying somthing exsist but not saying what it is
```cpp
int a; //(default initialization) this declares a ininterger called a and sets it with no value.
```
```cpp
int a = 5;//(copy initialization)
```

```cpp
int a(5);//(direct initialization)
```

```cpp
int a = 5, b = 6;          // copy initialization
int c( 7 ), d( 8 );        // direct initialization
int e { 9 }, f { 10 };     // direct brace initialization
int g = { 9 }, h = { 10 }; // copy brace initialization
int i {}, j {};            // value initialization
```
```cpp
//if you dont use a var the compiler might error
[[mabye_unused]] int x { 5 };
```

---
### iosteam
iosteam is a cpp standand libary with abunch of helpful functions however it can cause bloat naming concliioins and complexity.
include iostream and you get a few functions 
```cpp
#include <iostream>
std::cout << "words";//prints text or the value of var to the console 
// std::cout is also buffered
std::cin >> x;// reads a line from the dafasdfaskljfklsjdklonsole and saves it to a varible 
std::endl// the same as \n but it flushe the buffer
```
### undefined bahavior 
```cpp
int x; // un-init-ed int called x
printf("%i",x); // then we prnt x with could be any thing
```
### whilespace
whitespace is:  
    tabs  
     &  
s p a c e s   
you need whitespace in:
```cpp 
int x;
```
other that stuff like that it doesnt matter
```cpp
int        
x 
= 
5 


;// valid
```
### literals and opteraters
a literal is something explicit like the number 5 or the string "Hello"  
> In mathematics, an operation is a process involving zero or more input values (called operands) that produces a new value (called an output value). The specific operation to be performed is denoted by a symbol called an operator.
--- 
operators
> In mathematics, an operation is a process involving zero or more input values (called operands) that produces a new value (called an output value). The specific operation to be performed is denoted by a symbol called an operators
eg.. + - * / == <= >= != new delete throw
# chapter 2 
### functions 
functions are used so you dont have to repeat code over and over it eaier to write it once 
eg..
```cpp
// return-type name parmaters
void sayhello(){
    printf("hello");
}
// ...

sayhello();
```

the return type says what the function is going to return like int would return and int a string would return a string and void would return nothing.
eg ..
```cpp
int add(int x{}, int y{}){
    return x + y;
}
```
return is the keyword to end the function and return the givin value.

functions have to be **defined** before the main function so the program knows what it is.  
or you could **declare** it in the beggening of the program and define it later.
eg..
```cpp
int add(int x{}, int y{});
int main(){
    total = add(5, 5);
    return 0;
}
int add(int x{}, int y{}){
    return x + y;
}

```
---
### local scope
local scope talks about how depending where a varible or function in declared if it avabile
eg ..
```cpp
void yes(){
    int x{}; // x is created here
} // x dies here

x = 99; // wont work because x is only avabile in the function yes
```
---
### namespaces 

namespaces are used to avoid naming concliioins. they used the (::) operator.
iostream is an name space so the var and functions in it dont interfear with your program 
(name)::(the function) eg.. std::cout 

--- 
### multi-file 



to be revisied in future ^


# chapter 5 constant and strings 
## 5.1 constant varibles 
there are two types of constant  

- one is a name constant which means the value of the named constant will not and cannot change durring run time 
- another is a literal constant like pi (3.14) pi will never change 

types of named constants

- constant varibles
- object like macros like #define this "that"
- enumerated constants in lesssion 13.2

to make a constant varible is is your prefix varible defeination with const eg 
```cpp
const int {89};
```
the do nots:

- int const this{};
- void voo(const int){}
- use #define as const unless programing on arduiono / imbeded to save on binay space

the do's 

- prefer const over macros

const is a type qualifer as so is volatile which is rarely used.

## 5.2 Constant expressions, compile-time const, and runtime const

the as-if rule say the the compiler may change your program in order to product more optimized code.

there are 3 differnt stages of constsants

- constant expressions 
- compile time constants
- run time constants

consider the following
```cpp
#include <iostream>

int main()
{
	int x { 3 + 4 };
	std::cout << x << '\n';

	return 0;
}
```
x is equal to the constant expression 4 + 3. no matter what 4 + 3 is always equal to 7. so instead of spending cpu cycles on solving 4 + 3 every run time the compiler can just solve it then replace 4 + 3 with 7 eg
```cpp
#include <iostream>

int main()
{
	int x { 7 };
	std::cout << x << '\n';

	return 0;
}
```
there is still one more optimation that the compiler could make. since int x is only used once we could replace every accurance of x with its value to save on having to create space in ram and cpu cycles to read form ram eg
```cpp
#include <iostream>

int main()
{
	std::cout << 7 << '\n';

	return 0;
}
``` 
## 5.2 Constexpr variables

constexpr int x{};  
constexpr has to be defined when its declared.  
constexpr is flexable and can be runtime and compile time varible.
## 5.4 literals


|type |value | data type |
|--- | --- | ---|
|integer value|5, 0, -3|int|
|boolean value|true, false	|bool|
|floating point value|1.2, 0.0, 3.4|double (not float!)|	
|character|‘a’, ‘\n’|char|
|C-style string|“Hello, world!”|const char[14]|


Literal suffixes

|Data type|	Suffix|	Meaning|
| --- | --- | --- |
|integral|	u or U|	unsigned int|
|integral|	l or L|	long|
|integral|	ul, uL, Ul, UL, lu, lU, Lu, LU|	unsigned long|
|integral|	ll or LL|	long long|
|integral|	ull, uLL, Ull, ULL, llu, llU, LLu, LLU|	unsigned long long|
|integral|	z or Z|	The signed version of std::size_t (C++23)|
|integral|	uz, uZ, Uz, UZ, zu, zU, Zu, ZU|	std::size_t (C++23)|
|floating point|	f or F|	float|
|floating point|	l or L|	long double|
|string|	s|	std::string|
|string|	sv|	std::string_view|

**best practice**  
- prefer upper case suffixes
- dont use magic numbers use constexpr varibles instead
## 5.5 
we use the deciaml number system but there are others like:
- octal 1 2 3 4 5 6 7 (skip any 8 or 9) 10 11 12 13 14 15 16 17 (skip any 8 or 9) 20
- hexadecimal 1 2 3 4 5 6 7 8 9 10 A B C D E F 11 12 13 14 15 16 17 18 19 10 A B C D E F 

octals:
```cpp
int octal{012};// = 10 in decimal prefix any octal with 0
```
hexadecimal:
```cpp
int hexideciamal(0x28fb); // = something
```
there is also binary which you prefix with 0b

and you could use ' to sepreate large numbers or binary 

2'132'645'785

std::cout by default outputs decimal but you can chage that 
```cpp
    int x { 12 };
    std::cout << x << '\n'; // decimal (by default)
    std::cout << std::hex << x << '\n'; // hexadecimal
    std::cout << x << '\n'; // now hexadecimal
    std::cout << std::oct << x << '\n'; // octal
    std::cout << std::dec << x << '\n'; // return to decimal
    std::cout << x << '\n'; // decimal

```

Outputting values in binary is a little harder, as std::cout doesn’t come with this capability built-in. Fortunately, the C++ standard library includes a type called std::bitset that will do this for us (in the <bitset> header).

To use std::bitset, we can define a std::bitset variable and tell std::bitset how many bits we want to store. The number of bits must be a compile-time constant. std::bitset can be initialized with an integral value (in any format, including decimal, octal, hex, or binary).

```cpp
#include <bitset> // for std::bitset
#include <iostream>

int main()
{
	// std::bitset<8> means we want to store 8 bits
	std::bitset<8> bin1{ 0b1100'0101 }; // binary literal for binary 1100 0101
	std::bitset<8> bin2{ 0xC5 }; // hexadecimal literal for binary 1100 0101

	std::cout << bin1 << '\n' << bin2 << '\n';
	std::cout << std::bitset<4>{ 0b1010 } << '\n'; // create a temporary std::bitset and print it

	return 0;
}
```
## 5.6 conditional operator
so you can bacicly do if else statemnts in arithmetic 

```cpp
constexpr int x{4};
constexpr int y{6};
constexpr int b{ (x > y) ? x : y};
// b is = to x if x is larger or y if y is larger
```
these are good for conditions in varible inits. there is no if else replacement for this.

**note**  
cpp prioritizes the evaluation of most operators above the evaluation of the conditional operator, it’s quite easy to write expressions using the conditional operator that don’t evaluate as expected.

best practice:
 - dont use conditional operator in complex conditions.

## 5.7 inline functions

when ever a function is called there is a prefomacne overhaed

```cpp
int min(int x, int y){
    return (x > y) ? x : y;
}
```
since min is a simple function the overhead is not optimal 

stultion  
inline expansion happens at compile time and if the compiler decides to do so  
inline expansion is when the content of the function defination replaces the functions calles along with their varibles.

the only down side is that is the function being expanded takes more instructions thatn the function call beding replaced thatn each inline expannsion will cause the exectable to grow larger.

the inline keyword prefixes functions and tell the compiler that this function would prob benfit from inline expansion but now compilers dont need that now becuase they are better than they used to be and they can totaly just ignore the inline keyword

the inline keyword can also cause problems so its best not to use it.

## 5.8 constexpr and consteval functions

constexpr can also prefix varibles 
```cpp
constexpr int x {10}; // the value of x is known at init.
```
remeber constexpr cant be declared they have to be defined. 

constexpr functions must have a constexpr return and constexpr praamters and no call any non-constexpr functions for it to optimised. 

constexpr functions and varibles have the benifit of being runtime and compile-time.

```cpp
constexpr int min(int x, int y){
    return (x>y?y:x);
}
int main(){
    constexpr int x{6};
    constexpr int y{10}; // if i were to remove constexpr the function would run at run time not comile time 
    constexpr int g{min(x,y)};
    std::cout << g << "is greater";
    return 0;
}
```

if you want min() to be run at compile time set it equal to a constexpr varible eg ^  
if min() is set to a non constexpr varible it will run at runtime.  
pass min() to somthing like std::cout << min(5,6); it could run at compile time or runtime. 

in #include type_traits> std::is_constant_evaluated() returns a bool if a the current function is ran in a const context 

consteval mean that a function **must** be evaluated at compile time and will error if not.
```cpp
consteval min(int x, int x){
    return (x > y ? y : x );
}
```
```cpp
consteval auto comileTime(auto value){
    return value;
}
```

constexpr and consteval can be defined in many file but that fails the one-def rule, but if all the funcitons are defined the same it will run.

**best practice**
use constexpr functions when possible

## 5.9 strings and std::string

so any string like this "hello" is a c type string they have a fixed size

std::stirng and std::string_view are safer but more complex string types.  
std::string can very in legnth and can be set to differnt size string after its been defined.  
each charter in a strings 1 a byte.  
you can sufix a string 'hello's like this so its type is a std::string 

std::cin is used to get input form the user. its in iostream std::cin will only get input up to the first while space.

std::getline is like but its std::getline(std::cin,var); var is the varible to save the input to 

when using std::getline use std::gitline(std::cin >> std::ws, varible); this filters any whitespace at the start of the line.

you can get the length of a std::string name.length() is unsigned int int length { static_cast<int>(name.length()) };

c++20 gives std::ssize() to get the length of a string as a signed int

appearntly std::strings are expensive to init and copy so copy std::strings by refference
also returning a std::string from a function is also expensive.

** need to proper format ^**

## 5.10 intro to std::string_view
this topic is complex will revisit.

## 6.1 — Operator precedence and associativity


# Bits

std::bitset in in <bitset>

it lets us make varibles 

```cpp
#include <bitset>
#include <iostream>
int main(){
    // <8> is the numb of bits to be useable in the var foo
    //the bits order is..7654 3210
    // you can use ' to seperate the bits every 4 bits to make it more readable
    std::bitset<8> foo{0b0000'1111};
    std::cout << foo.test(7) << "\n";
    foo.set(7) // sets the bit on if off and if on nothing
    std::cout << foo.test(7) << "\n";
    foo.reset(6) // sets the bit off
    foo.flip(5) //if on sets off. if off sets on.
    return 0;
}
```
    size() returns the number of bits in the bitset.
    count() returns the number of bits in the bitset that are set to true. This can be used to determine if all bits are 0 or any bits are 1.
    all() returns a Boolean indicating whether all bits are set to true.
    any() returns a Boolean indicating whether any bits are set to true.
    none() returns a Boolean indicating whether no bits are set to true.
| operator | sysmbol | form | operation |
| --- | --- | --- | --- |
|left shift|	<<	|x << y	|all bits in x shifted left y bits|
|right shift|	>>	|x >> y	|all bits in x shifted right y bits|
|bitwise NOT|	~	|~x	|all bits in x flipped|
|bitwise AND|	&	|x & y	|each bit in x AND each bit in y|
|bitwise OR	|	x | y	|each bit in x OR each bit in y|
|bitwise XOR|	^	|x ^ y	|each bit in x XOR each bit in y|

the bits section is hard and long will come back to it 

# chapter 7

you can used {} for block statements such as for functions.
if statements by default execute only one statement but if we want more we can use block statements for any many statements as we want

## namespaces 

to make a namespace to avoid naming confilicts
```cpp
namespace my_space
{
    // namespace content
}
```

the scope resolution operator ( :: ) is used to go into a namespace and get a var or func

```cpp
#include <iostream>
namespace goo
{
  int x{69};
  void y(int x)
  {
    std::cout << x << "\n";
  }
}
namespace foo
{
  int x{54};
  void y(int x)
  {
    std::cout << x << "\n";
  }
}

int main(){
  foo::y(goo::x);
}
```

if we define x in the global namespace and you wnat to use the global namespace instead of the current one just use ::x

global varibles can be defined outside of the main function

```cpp
const g_x{67};
int main()
{
    return 0;
}
```

## shadow varibles

```cpp
#include <iostream>
int value{0};

int main(){
{
    std::cout << value; // prints global value
    int value{5} // shadows var value
    std::cout << value; // prints local value
    std::cout << ::value; // prints global value
    ++(::value)
    std::cout << ::value; // prints global value
}
    return 0;
}
```

## internal linkage

Global variables with internal linkage are sometimes called internal variables.

To make a non-constant global variable internal, we use the static keyword.

```cpp
// Internal global variables definitions:
static int g_x;          // defines non-initialized internal global variable (zero initialized by default)
static int g_x{ 1 };     // defines initialized internal global variable

const int g_y { 2 };     // defines initialized internal global const variable
constexpr int g_y { 3 }; // defines initialized internal global constexpr variable

// Internal function definitions:
static int foo() {};     // defines internal function
```
its best to use an unnamed namedspace for statics 

## external 

add external keyword to amke global virailbes external

```cpp
// External global variable definitions:
int g_x;                       // defines non-initialized external global variable (zero initialized by default)
extern const int g_x{ 1 };     // defines initialized const external global variable
extern constexpr int g_x{ 2 }; // defines initialized constexpr external global variable

// Forward declarations
extern int g_y;                // forward declaration for non-constant global variable
extern const int g_y;          // forward declaration for const global variable
extern constexpr int g_y;      // not allowed: constexpr variables can't be forward declared
```

## non const global varibles are evil

is best not to use non const global varibles because they can be changed easly which can effect your program.

## global constant varibles across multiful files

poir to C++17 you would define all the globals in a headerfile example

```cpp
#ifndef CONSTANTS_H
#define CONSTANTS_H

// define your own namespace to hold constants
namespace constants
{
    // constants have internal linkage by default
    constexpr double pi { 3.14159 };
    constexpr double avogadro { 6.0221413e23 };
    constexpr double myGravity { 9.2 }; // m/s^2 -- gravity is light on this planet
    // ... other related constants
}
#endif
```

and include this headerfile in every file that needed these constants but there is an issue. you would have to recompile every file that included this file if you were to change it 

after c++17 when inline was added example

```cpp
#ifndef CONSTANTS_H
#define CONSTANTS_H

// define your own namespace to hold constants
namespace constants
{
    inline constexpr double pi { 3.14159 }; // note: now inline constexpr
    inline constexpr double avogadro { 6.0221413e23 };
    inline constexpr double myGravity { 9.2 }; // m/s^2 -- gravity is light on this planet
    // ... other related constants
}
#endif
```
```cpp 
#include "constants.h"

#include <iostream>

int main()
{
    std::cout << "Enter a radius: ";
    double radius{};
    std::cin >> radius;

    std::cout << "The circumference is: " << 2 * radius * constants::pi << '\n';

    return 0;
}
```
 this still leves us with haveing to recompile everything that includes this header tho.

## static local varibles

the keyword static is used differntly accross cpp

for varibles when non-static they have automatic duration ( start at def and end at block end)

static varibles are created at program start and end at its end

example
```cpp
#include <iostream>

void incrementAndPrint()
{
    int value{ 1 }; // automatic duration by default
    ++value;
    std::cout << value << '\n';
} // value is destroyed here

int main()
{
    incrementAndPrint();
    incrementAndPrint();
    incrementAndPrint();

    return 0;
}```
```cpp
#include <iostream>

void incrementAndPrint()
{
    static int s_value{ 1 }; // static duration via static keyword.  This initializer is only executed once.
    ++s_value;
    std::cout << s_value << '\n';
} // s_value is not destroyed here, but becomes inaccessible because it goes out of scope

int main()
{
    incrementAndPrint();
    incrementAndPrint();
    incrementAndPrint();

    return 0;
}```

avoid static local varibles in a fucntion unless the value need to be reset everytime


to refresh a static global varible give it interal linkage which means it cant be used in other files.

## unnamed inline namespaces 

you can call methods in a unnamed space without a prefix

anything in an un namedspace basicly gives it interal namespace 

you can use inline name spaces to version functions 

the inline name space acts a the default namespace 

```cpp
#include <iostream>

namespace V1 // declare a normal namespace named V1
{
    void doSomething()
    {
        std::cout << "V1\n";
    }
}

inline namespace V2 // declare an inline namespace named V2
{
    void doSomething()
    {
        std::cout << "V2\n";
    }
}

int main()
{
    V1::doSomething(); // calls the V1 version of doSomething()
    V2::doSomething(); // calls the V2 version of doSomething()

    doSomething(); // calls the inline version of doSomething() (which is V2)

    return 0;
}```

V1
V2
V2
## 8.5 constexpr if statements

in a constextr if statment the condition conditionals must be know at compile time which means they too much be constexpr

## 8.5 switch statemetns

```cpp 
#include <iostream>

void printDigitName(int x)
{
    switch (x) // x evaluates to 3
    {
        case 1:
            std::cout << "One";
            break;
        case 2:
            std::cout << "Two";
            break;
        case 3:
            std::cout << "Three"; // execution starts here
            break; // jump to the end of the switch block
        default:
            std::cout << "Unknown";
            break;
    }

    // execution continues here
    std::cout << " Ah-Ah-Ah!";
}

int main()
{
    printDigitName(3);
    std::cout << '\n';

    return 0;
}
```


here is a switch statements its best to use these when youre using lots of elseif statmests

in switch statements if you dont add break; or return; it will **fall through** to other cases

sometimes fall throught is wanted and with c++17 compilers give [[fallthrough]] attribute which can be add to a null statement ; eg [[fallthrough]];   before the new case which to fall throught 

example of wanted fall throught
```cpp
bool isVowel(char c)
{
    switch (c)
    {
        case 'a': // if c is 'a'
        case 'e': // or if c is 'e'
        case 'i': // or if c is 'i'
        case 'o': // or if c is 'o'
        case 'u': // or if c is 'u'
        case 'A': // or if c is 'A'
        case 'E': // or if c is 'E'
        case 'I': // or if c is 'I'
        case 'O': // or if c is 'O'
        case 'U': // or if c is 'U'
            return true;
        default:
            return false;
    }
}
```

## 8.7 goto statements

the goto statement is an unconditonal statement which means unlike if or switch it will always preform its action.

with goto you can jump to functions or a labeled statement 
exapmple:
```cpp
int main()
{
    goto skip;   // error: this jump is illegal because...
    int x { 5 }; // this initialized variable is still in scope at statement label 'skip'
skip:
    x += 3;      // what would this even evaluate to if x wasn't initialized?
    return 0;
}
```
```cpp
#include <iostream>
#include <cmath> // for sqrt() function

int main()
{
    double x{};
tryAgain: // this is a statement label
    std::cout << "Enter a non-negative number: ";
    std::cin >> x;

    if (x < 0.0)
        goto tryAgain; // this is the goto statement

    std::cout << "The square root of " << x << " is " << std::sqrt(x) << '\n';
    return 0;
}
```

loops for while do while contuniue halts
