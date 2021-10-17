# Tali Specification (0.0.0)

*Tali: the ridiculously programmable programming language!*

Tali is specifically designed to free users from the /tyranny of
order/ - it is a Lisp in which every S-expression is a hashmap.

## Core Syntax

The following is a summary of Tali's core syntax.

### S-Expressions

In Tali, an S-expression is denoted as a set of key-value pairs:

```
(key-1: value-1
 key-2: value-2
 ...
 key-n: value-n)
```

Parentheses denote a /map/ in Tali, not a list.

### Evaluation

A traditional Lisp evaluates an S-expression by using the first
element of a list as the operator. The equivalent in Tali is a
reserved key, `@`, that denotes the operator.

```
(@: add
 a: 1
 b: 2)
```

Specifying an operator

### Defining functions

A trio of functions provide for documenting, declaring, and
defining functions in Tali: these are `doc`, `dec`, and `def`
respectively.

```
(@: doc
 n: add
 p: (a: "This is an explanation of a")
     b: "This is an explanation of b")
 d: "This is a function that adds two numbers.")

(@: dec
 n: add
 p: (a: Int
     b: Int)
 r: Int)

(@: def
 n: add
 p: {a, b}
 f: (+:
     a: a
     b: b)
```

This conventional order mirrors how one should be approaching
development in general: describe what you want the function to
do, specify the constraints, and finally implement it.

### Comments

Tali is designed to be entirely regular: no syntax is not
expressed outside of an S-expression. To this end, Tali
reserves a special key `#` for providing comments in
an expression. For example:

```
(@: doc
 n: add
 p: (a: "This is an explanation of a")
     b: "This is an explanation of b")
 d: "This is a function that adds two numbers."
 #: "We need this function because + is ugly")

(@: dec
 n: add
 p: (a: Int
     b: Int)
 r: Int
 #: "TODO: We'd like this to accept Dec in the future as well.")

(@: def
 n: add
 p: {a, b}
 f: (+:
     a: a
     b: b
     #: "This is a wrapper around the built-in operator!")
```

Each S-expression can be commented upon in this manner.

What to do with these comments during interpretation is another
matter; it is likely that they will be thrown away. Tali takes
the opinion that a comment should be treated as a parenthetical
aside - i.e., additional context that can be skipped over. If a
comment is integral to a function's description, it should be a
part of the function's documentation.

### Whitespace

A minimum of one character of whitespace is required between
`k:v` pairs.

Valid:
```
(@:add a:1 b:2)

(@: add
 a: 1
 b: 2)
```

Invalid:
```
(@:add a:1 b:2)
```

### Syntactic Sugar

#### Lists

Lists are denoted by white-space delimited symbols enclosed within
square brackets:

```
[a b c]
```

This corresponds to the Tali S-expression

```
(0:a 1:b 2:c len:3)
```

Note that this is shorthand for a Tali list, rather than
a conventional recursive list:

```
(a: a
 b: (a: b
     b: (a: c
         b: ())))
```

Tali lists offer random access and are much less verbose.

#### Sets

Sets are denoted by white-space delimited symbols enclosed within
curly brackets:

```
{a b c}
```

This corresponds to the Tali S-expression

```
(a:a b:b c:c)
```

## Conventions

### Variable Naming 

Tali favors terse, well-documented functions, mirroring the
example set by mathematicians. Single letters are preferable.
This leads to Tali programs with a strong vertical spine. It's
not single-letter variables that are the problem, so much as a
lack of adequate explanation of those variables.

For functions where order doesn't matter or variables
have no canonical names, use lowercase letters of the alphabet.
For example:

```
(@: def
 n: add
 p: {a, b}
 f: ...
 #: "They're both addends; order doesn't matter.")

(@: def
 n: subtract 
 p: {m, s}
 f: ...
 #: "Minuends and subtrahends; order matters.")
```

- Capital letters are preferred for sets (`E`).
- Lowercase letters followed by s are preferred for lists (`xs`)

### Code Formatting

A major aim of Tali is explicitness; nevertheless, using keyword
arguments everywhere can obscure the underlying logic. Thus, it
is preferable to de-emphasize keys relative to their associated
values.

### Code Style

Ultimately, a tool, `tali-format`, will be available to
automatically format code.

There are two ways to write a Tali expression: inline and per-line.

These two styles may be mixed, but no line may exceed 80
characters. A goal of Tali is readability.

```
(@: add
 a: 1
 b: 2
 #: "per-line: note space after the colon")

(@:add a:1 b:2 #:"inline: note lack of space after colon)
```

Tali `doc-dec-def`s should be grouped together, with one line
separating each S-expression within a group, and two lines
separating each trio of expressions. 

```
(@: doc
 ...)

(@: dec
 ...)

(@: def 
 ...)


(@: doc
 ...)

(@: dec
 ...)

(@: def 
 ...)
 
...
```

## Future Work

### Macros

Macros are fundamental to Lisps, and so getting them right
requires some extra thought and consideration.

### Types

#### Defining New Types and Typeclasses

### Configurability

Tali is meant to be a grammar specification, not a syntax
specification. Users should ideally be able to configure the
reserved keywords and symbols to their preference.
