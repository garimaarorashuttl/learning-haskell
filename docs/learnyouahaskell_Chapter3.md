Source:  http://learnyouahaskell.com/syntax-in-functions summary
```
* Pattern matching consists of specifying pattern to which some data should conform and then checking to see if it does toad deconstructing the data according to the patterns.Define separate function bodies for separate patterns.
* let xs = [(1,3), (4,3), (2,4), (5,3), (5,6), (3,1)].          [ a+b | (a,b) <- xs]  gives out [4,7,6,8,11,4]. If a pattern match fails, move onto the next element.
* x:xs will bind the head of the list to x and the tail to xs. Will only work for list with 1 or more elements.
* head' :: [a] -> a
  head' [ ]= error "can't call on empty list"
  head' (x:_) = x
* sum' :: (Num a) => [a] -> a
  sum' []= 0
  sum' (x:xs) = x + sum' xs 
* Patterns : to give names to the patters matched and also have access to the whole thing. 
* capital :: String -> String
  capital "" = "Empty string"
  capital all@(x:xs) = "This is the first letter of" ++ all ++ " is " ++ [x]
* Guards are way of testing whether some property of a value are true or false. 
bmiTell :: (RealFloat a) => a -> a -> String  
bmiTell weight height  
    | bmi <= skinny = "You're underweight, you emo, you!"  
    | bmi <= normal = "You're supposedly normal. Pffft, I bet you're ugly!"  
    | bmi <= fat    = "You're fat! Lose some weight, fatty!"  
    | otherwise     = "You're a whale, congratulations!"  
    where bmi = weight / height ^ 2  
          (skinny, normal, fat) = (18.5, 25.0, 30.0)

where bindings can also be nested,Its a common idiom to make a function and define some helper function in its where clause and then to give those functions helper functions as well, each with its own where clause.

* Where bindings are syntactical constructs that let you bind to variables at the end of a function and the whole function can see them, including all the guards. Let binidings let you bind to variables anywhere and are expressions themselves, but are very local, so they dont span across guards. let <bindings> in <expression>

(let (a,b,c) = (1,2,3) in a+b+c) * 100  
600

calcBmis :: (RealFloat a) => [(a, a)] -> [a]  
calcBmis xs = [bmi w h | (w, h) <- xs]  
    where bmi weight height = weight / height ^ 2  

calcBmis :: (RealFloat a) => [(a, a)] -> [a]  
calcBmis xs = [bmi | (w, h) <- xs, let bmi = w / h ^ 2] 

* Case expressions are useful for pattern matching against something in middle of expression. 
describeList :: [a] -> String  
describeList xs = "The list is " ++ case xs of [] -> "empty."  
                                               [x] -> "a singleton list."   
                                               xs -> "a longer list."

describeList :: [a] -> String  
describeList xs = "The list is " ++ what xs  
    where what [] = "empty."  
          what [x] = "a singleton list."  
          what xs = "a longer list."
```
