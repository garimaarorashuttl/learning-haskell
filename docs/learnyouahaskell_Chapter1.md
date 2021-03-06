Source : http://learnyouahaskell.com/starting-out

```
* Purely functional programming language
* Imperative languages : you give a series of instructions or a flow of control to execute and change state in between. In purely functional programming you don't tell the computer what to do as such but rather you tell it what stuff is.
* Purely functional languages: function has no side-effect. It can't change something, it just calculates something and give out the result.
* Referential transparency: if a function is called twice with same input it gives out the same output.
* Haskell is lazy, it will not execute functions and give out results unless forced to do so, a program is a series of transformations on data
* Infinite data structures. 
          doubleMe -> takes in a list and doubles every element 
          doubleMe(doubleMe(doubleMe(list_input))) in any other language would mean that a list is getting traversed 3 times, once for each doubleMe. 
          In Haskell, since it is a lazy language, the execution happens only when forced to do so. So the oo doubleMe asks the outer doubleMe which asks the inner doubleMe             
          to execute, so the inner double me sends out 2,the outer sends out 4 and the oo sends out 8. So effectively the entire operation occurs on one list pass.
* Statically typed. Type inference: you don't have to explicitly label your piece of code with a type because type system can intelligently figure out a lot about it.
* Ghc : Haskell compiler
* ghci : to invoke interactive mode. :l myfunctions  to load a file myfunctions.hs . :r  or :l myfunctions to reload the file after making changes.
*  If statement in Haskell is an expression, a piece of code that returns a value.
* In function name is generally used to donate a strict version of a function. Function names can't begin with upper case letters.
* A function that does not change anything is a definition. 
* Lists are a homogeneous data structures.
* Appending lists ++, Haskell goes through the entire list in the left.Putting something in the beginning, Haskell uses cons operator - ":" and it is instantaneous.
* !! Operator to get an element out of the list : a !! 6 -> 7th element of the list
* Head -> first element of list
* Tail -> list without head
* Last -> last element of the list
* Init -> list without last element
* Using head, tail , last, init on empty list throws runtime error
* Length , null, drop, take, reverse, maximum, minimum, sum, product, elem (4 'elem' [1,2,3,4,5])
* Ranges -> [1..20], ['a'..'z']. take 24 [13,26..]
* Functions that produce infinite list -> cycle, repeat . take 10 (cycle [1,2,3]) -> [1,2,3,1,2,3,1,2,3,1]. take 5 (repeat 5) -> [5,5,5,5,5]
* Set comprehensions -> used for building more specific sets out of general sets.S = {2.x | x E N, x<=10} . The portion to left of pipe is output function, x is variable , N is input, x<=10 is the predicate
* List comprehensions are like set comprehensions. First 10 even numbers: [x*2 | x <- [1..10]]. 
* Filter out numbers which are greater than 12.  [x*2 | x <- [1..10], x*2 >= 12]
* boomBang xs = ["BOOM" if x < 10 else "BANG | x <- xs, odd x, x/=13] (odd x values which are not 13)
* Tuples, are used when you know exactly how many values you want to combine and its type depends on how many components it has and the types of the components. They are denoted with parentheses and their components are separated by commas.
* [[1,2],[8,11,5],[4,5]] -> no error [(1,2),(8,11,5),(4,5)] -> compilation error
* You can't compare 2 tuples of different sizes, but you can compare two lists of different sizes.
* fst takes a pair and returns its first element: fst (8,11) gives out 8 as output
* snd takes a pair and returns its second element: snd(8,11) gives out 11 as output
* zip: the longer list gets cut to match the length of  the shorter list
* let rightTriangle = [(a,b,c | c<- [1..10], b<- [1..10]), a<-[1..10], a+b+c == 24, a^2+b^2 == c^2]
```
