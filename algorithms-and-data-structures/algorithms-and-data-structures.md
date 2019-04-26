# Big O Notation

### Intro to Big O

- A numeric representation of the performance of code.
- The focus is especially on (1) speed and (2) memory usage.
  - Speed —> Time Complexity
  - Memory Usage —> Space Complexity

### Timing Our Code

- The problem with timing using `performance.now()`: the time varies.
  - different machines record different times
  - the same machine even records different times
  - For really fast algorithms, speed measurement may not be precise enough.
  - For code that takes a long time to run, you don't want to have to wait for one hour until you get a time estimate.

### Counting Operations

- Instead of counting time, we count **the number (n) of simple operations** the computer has to perform.
- As **n** grows, the number of operations grow roughly in proportion with **n**.



### Official Intro to Big O

- It allows us to talk formally about how the runtime of an algorithm grows as the input grows.
- Essentially: it is a relationship between the input size and the runtime.



### Simplifying Big O Expressions

- We are concerned about the *general trend*
- *Constants* don't matter:
  - O(500) —> O(1)
  - O(2n) —> O(n)
  - O(n + 10) —> O(n)
  - O(13n^2) —> O(n^2)
  - O(n^2 + 5n + 8) —> O(n^2)
- Rules of Thumb:
  - Arithmetic operations are constant
  - Variable assignment is constant
  - Accessing elements in an array (by index) or object (by key) is constant
  - In a loop, the complexity is the length of the loop times the complexity of whatever happens inside of the loop.



### Space Complexity

- Most primitives (booleans, numbers, undefined, null) are constant space
- Strings require O(n) space (where *n* is the string length)
- References types are generally O(n) where *n* is the length (for arrays) or the number of keys (for objects)



### Logarithms

- a logarithm is the inverse of exponentiation
- just like multiplication and division are a pair, so also exponents and logarithms are a pair
- log2(value) = exponent —> 2^exponent = value
- log2(8) = 3 —> is like saying: 2, to what power, equals 8? Answer: 3
- log2(8) = 3 —> 2^3 = 8
- log base 2 of 8 equals 3
- Since we are only concerned with the overal trend, we can ommit the 2 in log2

### Recap

- Big O Notation is used to analyze the performance of an algorithm
- Big O Notation gives us a high level understanding of the time or space complexity of an algoritm
- Big O Notation doesn't care about precision, only about general trends (linear, quadratic, constant)
- The time or space complexity (as measured by Big O) depends only on the algorithm, not the hardware used to run the algorithm (some computers are slow than others)

![Screen Shot 2019-04-25 at 8.22.08 PM](/Users/ryanrichetto/Desktop/Screen Shot 2019-04-25 at 8.22.08 PM.png)