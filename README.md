# *"SIMPLE"*     Language-Design-&-Documentation

--------------

The project for the course is to write a compiler for a our own designed language which is 'simple'.
## Requirements
The language designed meets with these requirements are mentioned.
* *Data Types*: Signed and Unsigned integers, char, bool, 1D and 2D arrays.
* *Arithmetic Operations*: add, sub, mul, div, modulo
* *Boolean Operations*: and, or, not
* *Control Statements*: if-then, if-then-else, for loop, while loop, cond?opt1:opt2, break
* *Functions*: Call by Value parameter passing mechanism, recursion support
* I/O Routines

## Lexical Considerations
* All 'Simple' keywords are lowercase. Keywords and identifiers are case-sensitive.
For example, if is a keyword, but IF is a variable name; foo and Foo are two different names referring to two distinct variables.
* The reserved words are:
  Func , if, else, while, for, bool, int, uint,
1Darr,2Darr, and , or, not, break
* Comments are started by ## and are terminated by the end of the line.
* White space may appear between any lexical tokens. White space is defined as one or more spaces, tabs, page and line-breaking characters, and comments.
* A char is any printable ASCII character 
## Reference Grammar
_Meta-notation_ : 

| symbol        | semantics                                                            |
|---------------|:--------------------------------------------------------------------:|
|< foo >        | x is a non terminal symbol                                           |
| foo           | (in bold, means that foo is a terminal symbol, i.e; a token          |
| [x]           | means zero or one occurrence of x, i.e, x is optional                |
| x*            | means zero or more occurrence of x                                   |
| x <sup>+</sup>| means a comma-separated list of one or more x’s                      |
| \|            | or ; denotes separate alternatives                                   |
|'{}'           | for grouping                                                         |
|a-z, A-Z, 0-9  |Ranges of lower case, upper case and single digit numbers respectively|


#### MacroSyntax
program → Simple '{′  field_decl* method_decl* '}′

field_decl → {id  | 1Darr id ′[′  int_literal ′]′ | 2Darr id ′[′  int_literal ′]′′[′ int_literal ′]′ }<sup>+</sup> type, ;

method_decl -> id ([{id type}<sup>+</sup> ,]) {type | void} block

block -> ′{′ var decl* stmt* ′}′

var_decl -> id<sup>+</sup> type, ;

type -> unint | int | bool | char

stmt  -> location assign_op  expr ;

stmt  -> method call;

stmt  -> if ( expr ) block [else block]

stmt  -> for id = expr , expr block

stmt  -> return [expr];

stmt  -> break ;

stmt  -> block

assign op  -> = | += |-=

method_call -> method ([expr]<sup>+</sup>,)

method_name -> id

location -> id | id '[' expr ']'

expr -> location 

expr -> method_call

expr -> literal

expr -> expr bin_op expr

expr -> - expr

expr -> ! expr

expr -> ( expr )

bin_op -> arith_op | rel_op | eq_op | cond_op

#### MicroSyntax

arith_op -> + | - | * | / | %

rel_op -> < | > | <= | >=

eq_op -> == | !=

cond_op -> && | ||

literal -> int_literal | char_iteral | bool_literal

id -> alpha | alpha_num*

alpha_num -> alpha | digit

alpha -> a|b|c|d...|z|A|B|C|.....|Z

digit -> 0|1|2|3...|9

hex_digit -> digit | a | b | c | d | e | f | A | B | C | D | E | F

int literal -> decimal_literal | hex_literal

decimal_literal -> digit digit*

hex_literal -> 0x hex_digit hex_digit*

bool_literal -> true | false

char_literal -> ' char '

string_literal -> " char* "

## Types


### int datatype
A variable of type int, can store the set of integers, positive, negative and 0. Negative numbers
start with a - before the number.
### bool datatype
A variable of type bool, takes only two values which are themselves key words, true and false.
### uint datatype
A variable of type uint, store non-negative numbers. int and uint can be computed with a binary operator, but the uint variable is typecast into int, due to which it can be interpreted as a negative number also
### char datatype
A variable of type char, consists of ASCII symbols and store a single character
### 1D-array
It indicates a sequence of
variables with the same type and lying adjacent in memory. The size of the array is initialized in during declaration and cannot be changed.
For a 1D array during declaration, we observe '1Darr [ N ] type'
where N is an integer greater than 1 and denotes the size.
### 2D-array
It indicates a sequence of
variables with the same type and lying adjacent in memory. The size of the array is initialized in during declaration and cannot be changed.
For a 2D array during declaration, we observe '2Darr [ M ][ N ] type'
where N and M are integer greater than 1 and denotes the size.
* In 'Simple' arrays can’t be initialized to any value. So, each element has to be initialized individually if needed.

## Scope Rules
This is a static type language
It consists of a single class declaration for a class called **Simple**
Execution of a **Simple** program starts at method main.

### for statement

The for statement is similar to a for loop in **C**. 
It's syntax is 
```
i int;
for(i = 0;  i < some_var ; i++) {
    *series of statements*
}
```
if any new variable is declared inside the loop in the **series of statements**, then its scope is confined to the loop(local scope).The **check condition** happens before the **update statement** in each iteration

### if statement

The if statement is same as if loop in **C**. 
It's syntax is 
```
i int;
if(cond) {
    *series of statements*
}
else {
    *diff series of statements*
}
```
The if statement has the usual semantics. First, the expr is evaluated. If the result is true, the true arm is executed. Otherwise, the else arm is executed, if it exists. Since Decaf requires that the true and else arms be enclosed in braces, there is no ambiguity in matching an else arm with its corresponding if statement.


### *Operators precedence order*:


| Operators      | Comments                          |
|----------------|:---------------------------------:|
|-               |unary minus                        |
|!               |logical not                        |
|* / %           |multiplication, division, remainder|
|+ -             |addition, subtraction              |
|< , <= , >= , > |relational                         |
|== , !=         |equality                           |
|&&              |conditional and                    |
|\|\|            |conditional or                     |


## Semantic Rules
These are the rules for which semantic checks are performed
* No identifier is declared twice in the same scope
* No identifier is used before it is declared
* The arguments being passed in the function call must be same as the no of arguments the particular declared function has and each argument in the function call passed via call by value should have the same type of the declared function
* An id used as a location must name a declared local/global variable or formal parameter
* The expression in a return statement must have the same type as the declared result type
of the enclosing method definition
* All break and continue statements must be contained within the body of a for
* A function named as main has to be present in the program for the program to be executed



