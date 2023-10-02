# Udemy Scala &amp; Functional Programming Essentials | Rock the JVM

## The Absolute Scala Basics

1. Values, Variables and Types.

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

3. Expressions.

4. Functions.
   
5. Type Inference.

6. Recursion.

7. Call-by-Name and Call-by-Value.

8. Default and Named Arguments.

9. Smart Operations and Strings.

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
