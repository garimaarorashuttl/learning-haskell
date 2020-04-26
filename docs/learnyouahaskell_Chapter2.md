Source :  http://learnyouahaskell.com/types-and-typeclasses 

```

* :t followed by expression gives out type of the expression. Types are written in capital case.
* addThree :: Int -> Int -> Int -> Int . addThree x y z = x+y+z
* Int has maximum value (32 bit), Integer is unbounded. 
* factorial :: Integer -> Integer
  factorial n = product [1..n]
* : t head
  head :: [a] -> a . It is like a generic function. It does not have any type specific behaviour. Functions that have type variables are called polymorphic functions.
* typeclass is an interface that defines some behaviour. If a type is a part of typical that means it supports and implements the behaviour the typeclass describes. 
* (== ) the equality operator is a function like +,- etc. If a function contains just special characters ,it is considered as infix by default. Can be passed with parentheses.
* :t (==) 
  (==) :: (Eq a) => a-> a -> Bool.  Everything before symbol  => is called class constraint. The equality function takes any two values that have the same type and give       out a boolean. The type of those two values must be a member of Eq class which provides an interface for testing equality.
* Ord -> typeclass for standard comparing functions <. <=, >, >=
* Show -> to present as string. show function takes a value whose type is a member of Show and presents as a string
* Read -> typeclass opposite of Show. read takes in a string and returns a type which the input is a member of.
* read  "5" - 2 returns 3; since we are subtracting 2, compiler can infer the type to return. read  "5" throws exception. Use type annotations to fix the same. 
  read "5" :: Int tells compiler that we want it to be read as int, so it returns 5.
* Enum members are sequentially ordered types. They also have pred and succ functions defined.
* Bounded members have upper and lower bound. minBound, maxBound
  :t minBound  (Bounded a) => a . Polymorphic constants.
  minBound :: Int
* Num is numeric datatype class
* Integral numeric typeclass for only integral numbers. Int and Integer belong here
* Floating includes floating point numbers. Float, Double belong here.
* fromIntegral :: (Num b, Integral a) => a -> b. Takes in an integral and convert it to a number
```
