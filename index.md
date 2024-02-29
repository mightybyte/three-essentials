% Three Essentials of a Modern Programming Language
% Doug Beardsley

## Assumptions

- Don't assume programmers will get it right
- Automation: make the computer do it for you
- Language should have the right defaults

## Essential Language Features

1. First-class functions

# First-class Functions

## What are first-class functions?

> - You can pass a function to another function
> - You can return a function from another function
> - "Functional"

## Why first-class functions?

Abstract control flow

## Passing a function: map

    names = [];
    for ( var i = 0; i < people.length; i++ ) {
      names[i] = people[i].name;
    }

## Passing a function: map

    names = people.map(function(p) { return p.name; });

or (ECMAScript 6)

    names = people.map(p => p.name);

## Passing a function: filter

    minors = [];
    for ( var i = 0; i < people.length; i++ ) {
      if ( people[i].age < 18 ) {
        minors.push(people[i]);
      }
    }

## Passing a function: filter

    names = people.filter(p => p.age < 18);

## Passing a function: reduce

    var sum = 0;
    for ( var i = 0; i < values.length; i++ ) {
      sum += values[i];
    }

## Passing a function: reduce

    sum = values.reduce((a, b) => a + b, 0);

## More Complex Control Flow

    for ( i = 0; i < p; i++ ) {
      if ( someFunc(arr[i]) > threshold ) {
        for ( j = 0; j < q; j++ ) {
          if ( anotherCondition(foo[i][j]) ) {
            // stuff here
          }
        }
      }
    }

## Returning a function

> - Currying
> - Currying is the idea that a function of multiple arguments can be treated
>   as a function of one argument that returns another function.

## Returning a function: currying

    function foo(x, y, z) {
      return 2 * x^2 + 3 * y - 5 * z;
    } // Call with: foo(x, y, z);

could be written like

    function foo(x) {
      return ((y, z) => 2 * x^2 + 3 * y - 5 * z);
    } // Call with: foo(x)(y, z);

or

    function foo(x) {
      return (y => (z => 2 * x^2 + 3 * y - 5 * z));
    } // Call with: foo(x)(y)(z);

## Currying Distilled

    foo(x, y, z)

turns into

    foo(x)(y)(z)

## Automatic currying in Haskell

    foo x y z = 2 * x^2 + 3 * y - 5 * z

call with

    foo 2 3 4

or

    foo 2 3

or

    foo 2

## Currying Convenience

Instead of this

    values.map(x => plus(1,x));

we can do this

    map (plus 1) values

## Essential Language Features

1. First-class functions
2. Strong static type system w/ type inference

# Strong Static Type System

## The big realization of computing

> - EVERYTHING can be a number
> - Data is numbers
> - Programs are numbers

## What's in a number?

> - 11000001 00110100 11100010 01001101
> - What does that represent?  (What is its type?)
> - Int?
> - List<Bool>?
> - String?
> - Length in feet?
> - Length in meters?

## Types matter

## Strong Types

- Can't treat one type as another type
- Makes things reliable, provides guarantees

## Static Types

- Types are known (or can be calculated) at compile time
- Compiler finds your problems up front
- Make invalid values impossible
- No null pointers
- Catch variable name typos

## Type Inference

    foo x = x + 5

    (+) :: Num a => a -> a -> a

    foo :: Num a => a -> a

If we know that 5 is an Int

    foo :: Int -> Int

NOTE: Lower case a means it's a type variable that can be any type.

## Essential Language Features

1. First-class functions
2. Strong static type system w/ type inference
3. Purity by default

# Purity by Default

## Purity has a precise meaning

> - Control of side effects

## What are side effects?

> - Things that don't meet the mathematical definition of a function
> - Anything that happens that isn't reflected in the arguments or return
>   value
> - Returning different values for the same input
    (doesn't pass the vertical line test from high school algebra)

## Examples of Side Effects

> - Launching the missiles
> - Formatting the hard drive
> - Reading from disk / keyboard
> - Random number generator
> - Mutating a variable

## How is purity useful?

> - public BigInteger add(BigInteger val)
> - Things this function could do:
> - Format your hard drive
> - Phone home to another computer on the internet
> - Launch the missiles
> - val = 666

## In a language with purity

    def addBigInteger(a:BigInteger, b:BigInteger) : IO[BigInteger]

vs

    def addBigInteger(a:BigInteger, b:BigInteger) : BigInteger

or

    addBigInteger :: BigInteger -> BigInteger -> IO BigInteger

vs

    addBigInteger :: BigInteger -> BigInteger -> BigInteger
    
## Strong static types give IO teeth

## Type system allows more granular effects

    def writeFile(path:String, bytes:Array[Byte]) : FileIO[Unit]
    def readFile(path:String) : FileIO[Array[Byte]]

    writeFile :: FilePath -> Bytes -> FileIO ()
    readFile :: FilePath -> FileIO Bytes

# Conclusion

## Essential Language Features

1. First-class functions
2. Strong static type system w/ type inference
3. Purity by default

## Benefits

- More concise code
- Less repetition
- Catch problems sooner
- Eliminates whole categories of bugs
- Allows you to be more confident about what code does

## Questions?

mightybyte@gmail.com
https://dot.cards/mightybyte

http://github.com/mightybyte/three-essentials
