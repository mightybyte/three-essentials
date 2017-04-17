% Three Essentials of a Modern Programming Language
% Doug Beardsley
% Takt

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

    for ( i = 0; i < p; i++ ) {
      if ( someFunc(arr[i]) > threshold ) {
        for ( j = 0; j < q; j++ ) {
          if ( anotherCondition(foo[i][j]) ) {
            // stuff here
          }
        }
      }
    }

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
> - What does that represent?
> - Int?
> - List<Bool>?
> - String?
> - Length in feet?
> - Length in meters?

## Types matter

## Strong Types

- Can't treat one type as another type

## Static Types

- Compiler finds your problems up front
- Make invalid values impossible
- No null pointers

## Type Inference

    foo x = x + 5

    (+) :: Num a => a -> a -> a

    foo :: Num a => a -> a

If we know that 5 is an Int

    foo :: Int -> Int


## Essential Language Features

1. First-class functions
2. Strong static type system w/ type inference
3. Purity by default

# Purity by Default

## Purity has a precise meaning

> - Control of side effects

## What are side effects?

> - Anything that isn't passed in as an argument or returned
> - High school algebra: must pass the vertical line test

## Examples of Side Effects

> - Launching the missiles
> - Formatting the hard drive
> - Reading from disk / keyboard
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

## Questions?

doug@takt.com

http://github.com/mightybyte/three-essentials
