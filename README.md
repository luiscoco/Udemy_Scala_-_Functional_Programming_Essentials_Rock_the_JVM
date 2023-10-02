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
   
## 4. Type Inference.

## 5. Recursion.

## 6. Call-by-Name and Call-by-Value.

## 7. Default and Named Arguments.

## 8. Smart Operations and Strings.

## Object-Oriented Programming in Sala

10. Object-Oriented Basics.

11. Object-Oriented Basics (exercises).

12. Syntactic Sugar: Method Notations.

13. Method Notations (excercises).

14. Scala objects.

15. Inheritance.

16. Inheritance, continued: Abstract Classes and Traits.

17. Inheritance exercises: implementing our own Collection.

18. Generics.

19. Anonymous Classes.

20. Object-oriented exercises: expanding our Collection.

21. Case Classes.

22. Scala 3: Enums.

23. Exceptions.

24. Packing and Imports.

## Functional Programming in Scala

25. What's a Function?

26. Anonymous Functions.

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
