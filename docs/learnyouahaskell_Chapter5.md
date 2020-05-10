Source: http://learnyouahaskell.com/higher-order-functions

- Every function in haskell officially takes in one parameter.
- Curried functions -> with more than one parameter, takes in one first and create a function with that parameter as constant, then applies the second parameter to the same function.
- multThree :: (Num a) => a -> a -> a -> a  
multThree x y z = x * y * z  
multThree :: (Num a) => a -> (a -> (a -> a)). The thing before the -> is the parameter that a function takes and the thing after it is what it returns. So our function takes an a and returns a function of type (Num a) => a -> (a -> a). Similarly, this function takes an a and returns a function of type (Num a) => a -> a. And this function, finally, just takes an a and returns an a.

- Infix functions can also be partially applied by using sections. To section an infix function, simply surround it with parentheses and only supply a parameter on one side. That creates a function that takes one parameter and then applies it to the side that's missing an operand

divideByTen :: (Floating a) => a -> a  
divideByTen = (/10)
divideByTen 200

- Functions aren't instances of the Show typeclass, so we can't get a neat string representation of a function
- applyTwice :: (a -> a) -> a -> a  
  applyTwice f x = f (f x)

applyTwice (++ " HAHA") "HEY"  
"HEY HAHA HAHA"

applyTwice ("HAHA " ++) "HEY"  
"HAHA HAHA HEY"

-
zipWith' :: (a -> b -> c) -> [a] -> [b] -> [c]  
zipWith' _ [] _ = []  
zipWith' _ _ [] = []  
zipWith' f (x:xs) (y:ys) = f x y : zipWith' f xs ys  

where : is used to prepend to an array

-
flip' :: (a -> b -> c) -> b -> a -> c  
flip' f y x = f x y

-
map (map (^2)) [[1,2],[3,4,5,6],[7,8]]  
[[1,4],[9,16,25,36],[49,64]]  

-
sum (takeWhile (<10000) (filter odd (map (^2) [1..])))  is same as
sum (takeWhile (<10000) [n^2 | n <- [1..], odd (n^2)])  

-
let listOfFuns = map (*) [0..] (it is similar to writing [(0*),(1*),(2*),(3*),(4*),(5*)...)
(listOfFuns !! 4) 5
20

-
sum' :: (Num a) => [a] -> a  
sum' = foldl (+) 0

-
map' :: (a -> b) -> [a] -> [b]  
map' f xs = foldr (\x acc -> f x : acc) [] xs
Of course, we could have implemented this function with a left fold too. It would be `map' f xs = foldl (\acc x -> acc ++ [f x]) [] xs` but the thing is that the ++ function is much more expensive than :, so we usually use right folds when we're building up new lists from a list.

- One big difference is that right folds work on infinite lists, whereas left ones don't! To put it plainly, if you take an infinite list at some point and you fold it up from the right, you'll eventually reach the beginning of the list. However, if you take an infinite list at a point and you try to fold it up from the left, you'll never reach an end!

-
reverse' :: [a] -> [a]  
reverse' = foldl (\acc x -> x : acc) []  
OR
reverse' = foldl (flip (:)) []

- say we have a right fold and the binary function is f and the starting value is z. If we're right folding over the list [3,4,5,6], we're essentially doing this: f 3 (f 4 (f 5 (f 6 z))).Similarly, doing a left fold over that list with g as the binary function and z as the accumulator is the equivalent of g (g (g (g z 3) 4) 5) 6

- $ function, also called function application. Whereas normal function application (putting a space between two things) has a really high precedence, the $ function has the lowest precedence. Function application with a space is left-associative (so f a b c is the same as ((f a) b) c)), function application with $ is right-associative.
-sum (filter (> 10) (map (*2) [2..10]))? Well, because $ is right-associative, f (g (z x)) is equal to f $ g $ z x. And so, we can rewrite sum (filter (> 10) (map (*2) [2..10])) as sum $ filter (> 10) $ map (*2) [2..10]

- Apart from getting rid of parentheses, $ means that function application can be treated just like another function. That way, we can, for instance, map function application over a list of functions.
ghci> map ($ 3) [(4+), (10*), (^2), sqrt]  
[7.0,30.0,9.0,1.7320508075688772]


-
- map (\x -> negate (abs x)) [5,-3,-6,7,-3,2,-19,24]  
[-5,-3,-6,-7,-3,-2,-19,-24]
map (negate . abs) [5,-3,-6,7,-3,2,-19,24]  
[-5,-3,-6,-7,-3,-2,-19,-24]

- Function composition is right-associative
- Another common use of function composition is defining functions in the so-called point free style (also called the pointless style).
fn x = ceiling (negate (tan (cos (max 50 x))))  
fn = ceiling . negate . tan . cos . max 50  

- oddSquareSum :: Integer  
oddSquareSum = sum . takeWhile (<10000) . filter odd . map (^2) $ [1..]  

oddSquareSum :: Integer  
oddSquareSum =   
    let oddSquares = filter odd $ map (^2) [1..]  
        belowLimit = takeWhile (<10000) oddSquares  
    in  sum belowLimit
