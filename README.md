![Tali Logo](./graphics/tali-full.png)

Tali is a hashmap-y Lisp!

## Show me syntax!

In Tali, order doesn't matter: we use '@' to indicate the symbol
that should be evaluated in a hashmap.

``` tali
-- Tali uses double dashes for comments. How clean!

-- Defining a new function
(@: def
 n: add     -- n for "name"
 p: [a, b]  -- p for "parameters"
 f: (@: +   -- f for "function body"
     a: a   -- + takes two arguments; by convention, 
     b: b)  -- a and b should be used when name does
            -- does not matter
```

``` tali
-- Let's unleash hashmap *power*!

-- Lisp-style lists:
(@: quote
 q: (a: 0
     b: (a: 1
         b: (a: 2
             b: (a: 3
                 b: ()))))

(@: def
 n: car
 p: [xs]
 f: (@: idx
     k: a
     t: xs))

(@: def
 n: cdr
 p: [xs]
 f: (@: idx
     k: b
     t: xs))

-- /Tali/-style lists!:
(@: quote
 q: (0: 1
     1: 2
     2: 3
     3: 4
     len: 4)

-- How /better/ (random access included)!
```

``` tali
-- Let's have some real fun!

-- Mapping over a Tali-style list:
(@: def 
 n: map
 p: [f k xs]        -- k for key: needed to bind args
 f: (@:  map-help
     f:  f
     k:  k
     xs: ls
     a:  ()
     c:  0))

(@: def
 n: map-help
 p: [f k xs a c]
 f: (@: if
     p: (@:= a:c b:(@:dec v:(@:len xs:xs))) -- p for predicate
     t: (@: bind                            -- t for "if true"
         k: 'len 
         v: (@:len xs:xs)
         m: a)
     f: (@:  map-help                       -- f for "if false"
         f:  f
         k:  k
         xs: xs
         a:  (@: bind
              k: (@:c)
              v: (@:f (@:k):(@:idx k:c m:xs))
              m: a)
         c: (inc c))))

```

### Primitive Functions

- idx: returns the element in a hashmap
- bind: mutates a hashmap to set a (k, v) pair
- def: defines a function
- quote: returns arguments without evaluation

## So where's the interpreter?

I'm currently dabbling on one using Python 3
[here](https://github.com/tali-software-foundation/tali-python).

Of course, what's laid out above is simple enough that somebody
far more talented than me could probably bang out their own
interpreter in a weekend, if not a few hours. Tali really doesn't
have a standard yet, though - it's more an inchoate, coalescing
blob of ideas.

## Motivation

### *Another* Lisp, huh?

Yeah! Why not? Tali is designed to explore an extreme end of the
design space: hashmaps for everything, keywords everywhere! 

Will the result be more readable? Incomprehensible?? Let's find
out!

### Did you name this after a Mass Effect character? 

If it piques your interest, sure! If you're a lawyer, definitely
not!

Really, I just think Tali's a great name for a programming
language - fun, short, and homonymically rooted in computing!

## License

If Lisp truly is discovered, and not invented, then it is only
fitting to release Tali under the MIT license, and so I do that.
