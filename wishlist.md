# Wishlist

Here's a list of features I'd like Tali to support.

## Literate Tali

It's long past time programming shed its conformity to terminals.
Languages should still be editable in a text editor, but they
should support nicer, more flexible means of viewing.

It would be tremendous to be able to define an export rule for a
function, e.g., sum, that populates a LaTeX template and renders
it as an actual summation, sigma, bounds, and all.

## Partial Application

This is a major advantage of Tali.

## Built-In Types

I want a number of built-in math types.

- Int
- Dec (sugar: 10.24)
- Rat (sugar: 5/6)
- Img (sugar: 5.4i)
- Com (sugar: 7.6+5i)

- Str (sugar: "string") -> (0:'s', 1:'t', ..., len:6)
- Chr (sugar: 'c')
- Sym

## Key Shorthand

It might be desirable to allow keys to be referenced with a
non-conflicted prefix of the key, to make alignment nicer. Editor
tooling should ideally provide expanded definitions as desired. 

```
(@: Dog
 name: "doggyboi"
 breed: "cuteboi"
 happy: "always"
 price: NaN)

(@: Dog
 n: "doggyboi"
 b: "cuteboi"
 h: "always"
 p: NaN)
```

## Lambda Functions

Using the actual character lambda, of course!

```
(@: (@:λ
     p: {x y z}
     f: (@: and
         a: (@: >
             a: x
             b: 5)
         b: (@: >
             a: y
             b: z)))
 x: 1
 y: 2
 z: 3)
```
