# slang

## Description
Slang is a simple interpreted language mostly created as a learning experience.
Slang is a strictly evaluated, dynamically typed language. Each expression evaluates to a value. The language features referencial transparency through immutable variables. 

## Syntax

### Variable declaration
Variables are declared by the form:

```let varName = expr```

where varName is the name of the variable and expr is a expression.
For example:

```
let varName = {if 10>2 then 5 else 4}
```

### Functions
Functions are declared in the form of:

```
let funcName arg1 arg2 ... argN = expr
```

where funcName is the name of the function and arg1 to argN is the name of the arguments. 
For example:

```
let << a b = if a<b then a else b
```

```
SL > 1 << 2
1.0
SL > 10 << 5
5.0
```

When a function is called prefix the arguments must be surrounded in parentheses:
```
<< (1 2)
```

#### Infix
Functions consisting of symbols can be used infix, for example:

```
1 + 2
1 == 2
```

But can also be used prefix

```
/ (10 5)
```

Note that when used infix the function is binary as only two parameters can be given. 



### Sequences
A sequence is a list of expressions. The sequence takes on the value of the last expression. Each expression is put on a new line or can be seperated by a ';'
Sequences take the form of:

```
{
    let a = 10
    a + 5
}
```

which would return the value `15.0`

### Lists
A list is a collection of heterogeneous expressions. Items are separated by either ';', ',' or a space (' ')
A list takes the following form:

```
[1 2 3 4]
[1,2,3,4]
[1; 2; 3]
```

When given as an argument to a function they are unpacked to arguments.  `+ ([1,2,3])` is equivalent to `+ (1 2 3)`

### If
An if statement takes the form of:

```
if condition then consequence else alternative
```

where condition is an expression that should evaluate to a boolean value (true, false). If the condition evaluates to true then consequence is evaluated, otherwise alternative is evaluated.
Either consequence or alternative will be evaluated (lazy).

### While
A loop takes the form of 

```
while condition do expr where varName = expr
```

The variable `varName` is assigned initially to `expr`. `expr` is executed on each iteration while `condition` evaluates to a Boolean true. After each iteration `varName` takes the value of `expr`.

For example:

```
Loops
SL > let a = while x < 10 do { x + 1 } where x = 0
10.0
```


## Basic Functions

### Lists
There are various operators that work on lists

Two lists can be appended by `++`
For example:
```
SL > ++ (["hey" "there" "mufasa"])
["hey", "there", "mufasa"]
```

Multiple lists can be intercalated by an list:
```
SL > " " ++= ["hey" "there"]
"hey there"
SL > ", " ++= ["hey" "there"]
"hey, there"

SL > ++= ([0,1] [[1,2],[3,4],[5,6]])
[1.0, 2.0, 0.0, 1.0, 3.0, 4.0, 0.0, 1.0, 5.0, 6.0]
```

An item can be inserted to the beginning of a list by the cons operator (`:`)
```
SL > 1 : [3,4]
[1.0, 3.0, 4.0]
```

If only a few elements of a list are needed:
* `take (n xs)` takes the first `n` elements of `xs`
* `drop (n xs)` removes the first `n` elements of `xs`

A certain element of a list can be obtained using the `@` function
which takes the form
`xs @ n`
and returns the `n`-th element (zero based indexing) in `xs`

For example:

```
SL > [1,2,3,4] @ 2
3.0
```

### Arithmetic 
Regular addition. Takes multiple arguments.

```
1 + 1 = 2
+ (1 2 3 4) = 10
```

In addition (no pun intended), the following arithmetical functions exist:

* -
* /
* *

Arithmetical operators can take any number of parameters.


### Ordinality
These are binary operators that take two numbers and produce a boolean value; either true or false
* <    -- Less than
* >    -- Greater than

For example: 

```
SL > 1 < 2
true
SL > 3 > 4
false
```


### Equality
This function returns whether two objects have the same value
```
expr1 == expr2
```

For example:
```
SL > "test" == "test"
true
```

### ToNum

```
ToNum (val)
```

Tries to convert `val` to a number

For example:

```
SL > ToNum ("1.65")
1.65
```

### ShowVal

```
ShowVal (val)
```

Converts `val` to a string representation

For example:

```
SL > ShowVal (["the, hamster"])
""the, hamster""
```

### ReadToEnd

```
ReadToEnd (filename)
```

`filename` is a string

Reads all contents from file `filename` and stores its contents as a string

For example:

```
SL > ReadToEnd ("test.s")
"let b =  {
            if 10==10
                then 10
                else 20
        }"
SL >
```

### OpenFileR

```
OpenFileR(filename)
```

`filename` is a string

Returns a handle to read from file

### OpenFileW

```
OpenFileW(filename)
```

`filename` is a string

Returns a handle to write to file

### WriteLine

```
WriteLine(handle, line)
```

`handle` is a handle. `line` is a string

Writes a single line to the handle

### ReadLine

```
ReadLine(handle)
```

`handle` is a handle.

Reads a single line from the handle

## General IO
The standard input buffer handle is given by `stdin` and the standard output buffer handle by `stdout`


