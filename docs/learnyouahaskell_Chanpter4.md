Source: http://learnyouahaskell.com/recursion 

```
maximum' :: (Ord a) => [a] -> a
maximum' [] = error "Maximum of empty list"
maximum' [x] = x
maximum' (x:xs) | x > maxTail = x 
                | otherwise = maxTail
                where maxTail = maximum' xs

----

maximum' :: (Ord a) => [a] -> a  
maximum' [] = error "maximum of empty list"  
maximum' [x] = x  
maximum' (x:xs) = max x (maximum' xs)  


---

replicate' :: (Num i, Ord i) => i -> a -> [a]  
replicate' n x  
    | n <= 0    = []  
    | otherwise = x:replicate' (n-1) x  

Num is not a subclass of Ord, that is why have to specify both Num and Ord constraints.

---
take' :: (Num i, Ord i) => i -> [a] -> [a]
take' n _
     | n <= 0 = [] -- a guard without otherwise will just fall through the next pattern
take' _, [] = []
take' n, (x:xs) = x:take' n-1 xs

---

zip' :: [a] -> [b] -> [(a,b)]
zip' [] _ = []
zip' _ [] = []
zip' (x:xs) (y:ys) = (x,y): zip' xs ys

---

quicksort :: (Ord a) => [a] -> [a]  
quicksort [] = []  
quicksort (x:xs) =   
    let smallerSorted = quicksort [a | a <- xs, a <= x]  
        biggerSorted = quicksort [a | a <- xs, a > x]  
    in  smallerSorted ++ [x] ++ biggerSorted  

```
