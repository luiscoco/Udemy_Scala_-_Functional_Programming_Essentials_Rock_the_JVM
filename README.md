# Udemy Scala &amp; Functional Programming Essentials | Rock the JVM

## The Absolute Scala Basics

### 1. Values, Variables and Types.

```scala
package com.rockthejvm.part1basics

object ValuesAndTypes {

  // values
  val meaningOfLife: Int = 42 // const int meaningOfLife = 42

  // reassigning is not allowed
  meaningOfLife = 45

  // type inferrence
  val anInteger = 67 // : Int is optional

  // common types
  val aBoolean: Boolean = false
  val aChar: Char = 'a'
  val anInt: Int = 78 // 4 bytes
  val aShort: Short = 5263 // 2 bytes
  val aLong: Long = 52789572389234L // 8 bytes
  val aFloat: Float = 2.4f // 4 bytes
  val aDouble: Double = 3.14 // 8 bytes

  // string
  val aString: String = "Scala"

  def main(args: Array[String]): Unit = {
    print(aString)
  }
}
```

### 2. Expressions.

```scala
package com.rockthejvm.part1basics

object Expressions {

  // expressions are structures that can be evaluated to a value
  val meaningOfLife = 40 + 2

  // mathematical expressions: +, -, *, /, bitwise |, &, <<, >>, >>>
  val mathExpression = 2 + 3 * 4

  // comparison expressions: <, <=, >, >=, ==, !=
  val equalityTest = 1 == 2

  // boolean expressions: !, ||, &&
  val nonEqualityTest = !equalityTest

  // instructions vs expressions
  // expressions are evaluated, instructions are executed
  // we think in terms of expressions

  // ifs are expressions
  val aCondition = true
  val anIfExpression = if (aCondition) 45 else 99

  // code blocks
  val aCodeBlock = {
    // local values
    val localValue = 78
    // expressions...

    // last expression = value of the block
    localValue + 54
  }

  // everything is an expression

  /**
   * Exercise:
   *  Without running the code, what do you think these values will print out?
   */
  // 1
  val someValue = {
    2 < 3
  }

  // 2
  val someOtherValue = {
    if (someValue) 239 else 986
    42
  }

  // 3
  val yetAnotherValue: Unit = println("Scala")
  val theUnit: Unit = () // Unit == "void" in other languages

  def main(args: Array[String]): Unit = {
    println(someValue) // true
    println(someOtherValue) // 42
    println(yetAnotherValue) // Scala, ()
  }
}
```

## 3. Functions.

```scala
package com.rockthejvm.part1basics

object Functions {

  // function = reusable piece of code that you can invoke with some arguments and return a result
  def aFunction(a: String, b: Int): String =
    a + " " + b // ONE expression

  // function invocation
  val aFunctionInvocation = aFunction("Scala", 999999999)

  def aNoArgFunction(): Int = 45
  def aParamterlessFunction: Int = 45

  // functions can be recursive
  def stringConcatenation(str: String, n: Int): String =
    if (n == 0) ""
    else if (n == 1) str
    else str + stringConcatenation(str, n - 1)

  /*
    sc("Scala", 3) = "Scala" + sc("Scala", 2) = "Scala" + "ScalaScala" = "ScalaScalaScala"
    sc("Scala", 2) = "Scala" + sc("Scala", 1) = "Scala" + "Scala" = "ScalaScala"
    sc("Scala", 1) = "Scala"
   */
  val scalax3 = stringConcatenation("Scala", 3)
  // when you need loops, use RECURSION.

  // "void" functions
  def aVoidFunction(aString: String): Unit =
    println(aString)

  def computeDoubleStringWithSideEffect(aString: String): String = {
    aVoidFunction(aString) // Unit
    aString + aString // meaningful value
  } // discouraging side effects

  def aBigFunction(n: Int): Int = {
    // small, auxiliary functions inside
    def aSmallerFunction(a: Int, b: Int): Int = a + b

    aSmallerFunction(n, n + 1)
  }

  /**
   * Exercises
   * 1. A greeting function (name, age) => "Hi my name is $name and I am $age years old."
   * 2. Factorial function n => 1 * 2 * 3 * .. * n
   * 3. Fibonacci function
   *    fib(1) = 1
   *    fib(2) = 1
   *    fib(3) = 1 + 1
   *    fib(n) = fib(n-1) + fib(n-2)
   *
   * 4. Tests if a number is prime
   */

  // 1
  def greetingForKids(name: String, age: Int): String =
    "Hi, my name is " + name + " and I am " + age + " years old."

  // 2
  /*
    f(5) = 5 * f(4) = 120
    f(4) = 4 * f(3) = 24
    f(3) = 3 * f(2) = 6
    f(2) = 2 * f(1) = 2
    f(1) = 1
   */
  def factorial(n: Int): Int =
    if (n <= 0) 0
    else if (n == 1) 1
    else n * factorial(n - 1)

  // 3
  /*
    fib(5) = fib(4) + fib(3) = 5
    fib(4) = fib(3) + fib(2) = 3
    fib(3) = fib(2) + fib(1) = 2
    fib(2) = 1
    fib(1) = 1
   */
  def fibonacci(n: Int): Int =
    if (n <= 2) 1
    else fibonacci(n - 1) + fibonacci(n - 2)

  // 4
  /*
    isPrime(7) = isPrimeUntil(3) = true
    ipu(3) = 7 % 3 != 0 && ipu(2) = true
    ipu(2) = 7 % 2 != 0 && ipu(1) = true
    ipu(1) = true
   */
  def isPrime(n: Int): Boolean = {
    def isPrimeUntil(t: Int): Boolean =
      if (t <= 1) true
      else n % t != 0 && isPrimeUntil(t - 1)

    isPrimeUntil(n / 2)
  }

  def main(args: Array[String]): Unit = {
    println(greetingForKids("Daniel", 9))
    println(factorial(5))
    println(fibonacci(5))
    println(isPrime(7))
  }
}
```


## 4. Type Inference.

## 5. Recursion.
```scala
package com.rockthejvm.part1basics

import scala.annotation.tailrec

object Recursion {

  // "repetition" = recursion
  def sumUntil(n: Int): Int =
    if (n <= 0) 0
    else n + sumUntil(n - 1) // "stack" recursion

  def sumUntil_v2(n: Int): Int = {
    /*
      sut(10, 0) =
      sut(9, 10) =
      sut(8, 9 + 10) =
      sut(7, 8 + 9 + 10) =
      ...
      sut(0, 1 + 2 + 3 + .. + 9 + 10)
      = 1 + 2 + 3 + .. + 10
     */
    @tailrec
    def sumUntilTailrec(x: Int, accumulator: Int): Int =
      if (x <= 0) accumulator
      else sumUntilTailrec(x - 1, accumulator + x) // TAIL recursion = recursive call occurs LAST in its code path
      // no further stack frames necessary = no more risk of SO

    sumUntilTailrec(n, 0)
  }

  def sumNumbersBetween(a: Int, b: Int): Int =
    if (a > b) 0
    else a + sumNumbersBetween(a + 1, b)

  def sumNumbersBetween_v2(a: Int, b: Int): Int = {
    @tailrec
    def sumTailrec(currentNumber: Int, accumulator: Int): Int =
      if (currentNumber > b) accumulator
      else sumTailrec(currentNumber + 1, currentNumber + accumulator)

    sumTailrec(a, 0)
  }

  /**
   * Exercises
   * 1. Concatenate a string n times
   * 2. Fibonacci function, tail recursive
   * 3. Is isPrime function tail recursive or not?
   */

  // 1
  def concatenate(string: String, n: Int): String = {
    @tailrec
    def concatTailrec(remainingTimes: Int, accumulator: String): String =
      if (remainingTimes <= 0) accumulator
      else concatTailrec(remainingTimes - 1, string + accumulator)

    concatTailrec(n, "")
  }

  // 2
  def fibonacci(n: Int): Int = {
    def fiboTailrec(i: Int, last: Int, previous: Int): Int =
      if (i >= n) last
      else fiboTailrec(i + 1, last + previous, last)

    if (n <= 2) 1
    else fiboTailrec(2, 1, 1)
  }

  // 3 - yes, rephrasing:
  def isPrime(n: Int): Boolean = {
    def isPrimeUntil(t: Int): Boolean =
      if (t <= 1) true
      else if (n % t == 0) false
      else isPrimeUntil(t - 1)

    isPrimeUntil(n / 2)
  }

  def main(args: Array[String]): Unit = {
    println(sumUntil_v2(20000))
    println(concatenate("Scala", 5))
    println(fibonacci(7))
  }
}
```

## 6. Call-by-Name and Call-by-Value.

```scala
package com.rockthejvm.part1basics

object CBNvsCBV {

  // CBV = call by value = arguments are evaluated before function invocation
  def aFunction(arg: Int): Int = arg + 1
  val aComputation = aFunction(23 + 67)

  // CBN = call by name = arguments are passed LITERALLY, evaluated at every reference
  def aByNameFunction(arg: => Int): Int = arg + 1
  val anotherComputation = aByNameFunction(23 + 67)

  def printTwiceByValue(x: Long): Unit = {
    println("By value: " + x)
    println("By value: " + x)
  }

  /*
    CBN major features:
    - delayed evaluation of the argument
    - argument is evaluated every time it is used
   */
  def printTwiceByName(x: => Long): Unit = {
    println("By name: " + x)
    println("By name: " + x)
  }

  /*
    Another benefit of CBN is that it delays the evaluation of the argument until it's used.
    If it's not used, it's not evaluated.
   */
  def infinite(): Int = 1 + infinite()
  def printFirst(x: Int, y: => Int) = println(x)


  def main(args: Array[String]): Unit = {
    printTwiceByValue(System.nanoTime()) // prints the same instant twice
    printTwiceByName(System.nanoTime()) // prints two different instants

    printFirst(42, infinite()) // works
    // printFirst(infinite(), 42) // crashes
  }
}
```

## 7. Default and Named Arguments.

```scala
package com.rockthejvm.part1basics

import scala.annotation.tailrec

object DefaultArgs {

  @tailrec
  def sumUntilTailrec(x: Int, accumulator: Int = 0): Int =
    if (x <= 0) accumulator
    else sumUntilTailrec(x - 1, accumulator + x)

  val sumUntil100 = sumUntilTailrec(100) // additional arg passed automatically

  // when you use a function most of the time with the same value = default arguments
  def savePicture(dirPath: String, name: String, format: String = "jpg", width: Int = 1920, height: Int = 1080): Unit =
    println("Saving picture in format " + format + " in path " + dirPath)


  def main(args: Array[String]): Unit = {
    // default args are injected
    savePicture("/users/daniel/photos", "myphoto")
    // pass explicit different values for default args
    savePicture("/users/daniel/photos", "myphoto", "png")
    // pass values after the default argument
    savePicture("/users/daniel/photos", "myphoto", width = 800, height = 600)
    // naming arguments allow passing in a different order
    savePicture("/users/daniel/photos", "myphoto", height = 600, width = 800)
  }
}
```

## 8. Smart Operations and Strings.

```scala
package com.rockthejvm.part1basics

object StringOps {

  val aString: String = "Hello, I am learning Scala"

  // string functions
  val secondChar = aString.charAt(1)
  val firstWord = aString.substring(0, 5) // "Hello"
  val words = aString.split(" ") // Array("Hello,", "I", "am", "learning", "Scala")
  val startsWithHello = aString.startsWith("Hello") // true
  val allDashes = aString.replace(' ', '-')
  val allUppercase = aString.toUpperCase() // also toLowerCase()
  val nChars = aString.length

  // other functions
  val reversed = aString.reverse
  val aBunchOfChars = aString.take(10)

  // parse to numeric
  val numberAsString = "2"
  val number = numberAsString.toInt

  // s-interpolation
  val name = "Alice"
  val age = 12
  val greeting = "Hello, I'm " + name + " and I am " + age + "years old."
  val greeting_v2 = s"Hello, I'm $name and I'm $age years old."
  val greeting_v3 = s"Hello, I'm $name and I will be turning ${age + 1} years old."

  // f-interpolation
  val speed = 1.2f
  val myth = f"$name can eat $speed%2.5f burgers per minute."

  // raw-interpolation
  val escapes = raw"This is a \n newline"

  def main(args: Array[String]): Unit = {
    println(escapes)
  }
}
```

## Object-Oriented Programming in Scala

## 10. Object-Oriented Basics.




## 11. Object-Oriented Basics (exercises).




## 12. Syntactic Sugar: Method Notations.




## 13. Method Notations (excercises).




## 14. Scala objects.




## 15. Inheritance.




## 16. Inheritance, continued: Abstract Classes and Traits.




## 17. Inheritance exercises: implementing our own Collection.



## 18. Generics.




## 19. Anonymous Classes.




## 20. Object-oriented exercises: expanding our Collection.



## 21. Case Classes.




## 22. Scala 3: Enums.




## 23. Exceptions.




## 24. Packing and Imports.




## Functional Programming in Scala

## 25. What's a Function?



## 26. Anonymous Functions.



27. Higher-Order-Functions and Curries.



28. HOFs and Curries (exercises).




29. map, flatMap, filter and for-comprehensions.




30. A Collections Overview.




31. Sequences: List, Array, Vector.




32. Tuples and Maps.




33. Tuples and Maps (execises).




34. Options.




35. Handling Failure.




## Pattern Matching

36. Pattern Matching.




37. All the patterns.





38. Scala 3: braceless syntax.


