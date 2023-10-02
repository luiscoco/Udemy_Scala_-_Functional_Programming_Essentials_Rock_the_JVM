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

```scala
package com.rockthejvm.part2oop

object OOBasics {

  // classes
  class Person(val name: String, age: Int) { // constructor signature
    // fields
    val allCaps = name.toUpperCase()

    // methods
    def greet(name: String): String =
      s"${this.name} says: Hi, $name"

    // signature differs
    // OVERLOADING
    def greet(): String =
      s"Hi, everyone, my name is $name"

    // aux constructor
    def this(name: String) =
      this(name, 0)

    def this() =
      this("Jane Doe")
  }

  val aPerson: Person = new Person("John", 26)
  val john = aPerson.name // class parameter != field
  val johnSayHiToDaniel = aPerson.greet("Daniel")
  val johnSaysHi = aPerson.greet()
  val genericPerson = new Person()

  def main(args: Array[String]): Unit = {
    val charlesDickens = new Writer("Charles", "Dickens", 1812)
    val charlesDickensImpostor = new Writer("Charles", "Dickens", 2021)

    val novel = new Novel("Great Expectations", 1861, charlesDickens)
    val newEdition = novel.copy(1871)

    println(charlesDickens.fullName)
    println(novel.authorAge)
    println(novel.isWrittenBy(charlesDickensImpostor)) // false
    println(novel.isWrittenBy(charlesDickens)) // true
    println(newEdition.authorAge)

    val counter = new Counter()
    counter.print() // 0
    counter.increment().print() // 1
    counter.increment() // always returns new instances
    counter.print() // 0

    counter.increment(10).print() // 10
    counter.increment(20000).print() // 20000
  }
}

/**
  Exercise: imagine we're creating a backend for a book publishing house.
  Create a Novel and a Writer class.

  Writer: first name, surname, year
    - method fullname

  Novel: name, year of release, author
    - authorAge
    - isWrittenBy(author)
    - copy (new year of release) = new instance of Novel
 */

class Writer(firstName: String, lastName: String, val yearOfBirth: Int) {
  def fullName: String = s"$firstName $lastName"
}

class Novel(title: String, yearOfRelease: Int, val author: Writer) {
  def authorAge: Int = yearOfRelease - author.yearOfBirth
  def isWrittenBy(author: Writer): Boolean = this.author == author
  def copy(newYear: Int): Novel = new Novel(title, newYear, author)
}

/**
 * Exercise #2: an immutable counter class
 * - constructed with an initial count
 * - increment/decrement => NEW instance of counter
 * - increment(n)/decrement(n) => NEW instance of counter
 * - print()
 *
 * Benefits:
 * + well in distributed environments
 * + easier to read and understand code
 */

class Counter(count: Int = 0) {
  def increment(): Counter =
    new Counter(count + 1)

  def decrement(): Counter =
    if (count == 0) this
    else new Counter(count - 1)

  def increment(n: Int): Counter =
    if (n <= 0) this
    else increment().increment(n - 1) // vulnerable to SOs

  def decrement(n: Int): Counter =
    if (n <= 0) this
    else decrement().decrement(n - 1)

  def print(): Unit =
    println(s"Current count: $count")
}
```

## 11. Object-Oriented Basics (exercises).

## 12. Syntactic Sugar: Method Notations.

```scala
package com.rockthejvm.part2oop

import scala.language.postfixOps

object MethodNotations {

  class Person(val name: String, val age: Int, favoriteMovie: String) {
    infix def likes(movie: String): Boolean =
      movie == favoriteMovie

    infix def +(person: Person): String =
      s"${this.name} is hanging out with ${person.name}"

    infix def +(nickname: String): Person =
      new Person(s"$name ($nickname)", age, favoriteMovie)

    infix def !!(progLanguage: String): String =
      s"$name wonders how can $progLanguage be so cool!"

    // prefix position
    // unary ops: -, +, ~, !
    def unary_- : String =
      s"$name's alter ego"

    def unary_+ : Person =
      new Person(name, age + 1, favoriteMovie)

    def isAlive: Boolean = true

    def apply(): String =
      s"Hi, my name is $name and I really enjoy $favoriteMovie"

    def apply(n: Int): String =
      s"$name watched $favoriteMovie $n times"
  }

  val mary = new Person("Mary", 34, "Inception")
  val john = new Person("John", 36, "Fight Club")

  val negativeOne = -1

  /**
   *  Exercises
   *  - a + operator on the Person class that returns a person with a nickname
   *    mary + "the rockstar" => new Person("Mary the rockstar", _, _)
   *  - a UNARY + operator that increases the person's age
   *    +mary => new Person(_, _, age + 1)
   *  - an apply method with an int arg
   *    mary.apply(2) => "Mary watched Inception 2 times"
   */

  def main(args: Array[String]): Unit = {
    println(mary.likes("Fight Club"))
    // infix notation - for methods with ONE argument
    println(mary likes "Fight Club") // identical

    // "operator" = plain method
    println(mary + john)
    println(mary.+(john)) // identical
    println(2 + 3)
    println(2.+(3)) // same
    println(mary !! "Scala")

    // prefix position
    println(-mary)

    // postfix notation
    println(mary.isAlive)
    println(mary isAlive) // discouraged

    // apply is special
    println(mary.apply())
    println(mary()) // same

    // exercises
    val maryWithNickname = mary + "the rockstar"
    println(maryWithNickname.name)

    val maryOlder = +mary
    println(maryOlder.age) // 35

    println(mary(10))
  }
}
```

## 13. Method Notations (excercises).

## 14. Scala objects.

```scala
package com.rockthejvm.part2oop

object Objects {

  object MySingleton { // type + the only instance of this type
    val aField = 45
    def aMethod(x: Int) = x + 1
  }

  val theSingleton = MySingleton
  val anotherSingleton = MySingleton
  val isSameSingleton = theSingleton == anotherSingleton // true
  // objects can have fields and methods
  val theSingletonField = MySingleton.aField
  val theSingletonMethodCall = MySingleton.aMethod(99)

  class Person(name: String) {
    def sayHi(): String = s"Hi, my name is $name"
  }

  // companions = class + object with the same name in the same file
  object Person { // companion object
    // can access each other's private fields and methods
    val N_EYES = 2
    def canFly(): Boolean = false
  }

  // methods and fields in classes are used for instance-dependent functionality
  val mary = new Person("Mary")
  val mary_v2 = new Person("Mary")
  val marysGreeting = mary.sayHi()
  mary == mary

  // methods and fields in objects are used for instance-independent functionality - "static"
  val humansCanFly = Person.canFly()
  val nEyesHuman = Person.N_EYES

  // equality
  // 1 - equality of reference - usually defined as ==
  val sameMary = mary eq mary_v2 // false, different instances
  val sameSingleton = MySingleton eq MySingleton // true
  // 2 - equality of "sameness" - in Java defined as .equals
  val sameMary_v2 = mary equals mary_v2 // false
  val sameMary_v3 = mary == mary_v2 // same as equals - false
  val sameSingleton_v2 = MySingleton == MySingleton // true

  // objects can extend classes
  object BigFoot extends Person("Big Foot")

  //
  /*
    Scala application:
      object Objects {
        def main(args: Array[String]): Unit = { ... }
      }

    Equivalent Java application:
      public class Objects {
        public static void main(String[] args) { ... }
      }
   */
  def main(args: Array[String]): Unit = {
    println(sameMary_v3)
  }
}
```

## 15. Inheritance.

```scala
package com.rockthejvm.part2oop

object Inheritance {

  class Animal {
    val creatureType = "wild"
    def eat(): Unit = println("nomnomnom")
  }

  class Cat extends Animal { // a cat "is an" animal
    def crunch() = {
      eat()
      println("crunch, crunch")
    }
  }

  val cat = new Cat

  class Person(val name: String, age: Int) {
    def this(name: String) = this(name, 0)
  }

  class Adult(name: String, age: Int, idCard: String) extends Person(name) // must specify super-constructor

  // overriding
  class Dog extends Animal {
    override val creatureType = "domestic"
    override def eat(): Unit = println("mmm, I like this bone")

    // popular overridable method
    override def toString: String = "a dog"
  }

  // subtype polymorphism
  val dog: Animal = new Dog
  dog.eat() // the most specific method will be called

  // overloading vs overriding
  class Crocodile extends Animal {
    override val creatureType = "very wild"
    override def eat(): Unit = println("I can eat anything, I'm a croc")

    // overloading: multiple methods with the same name, different signatures
    // different signature =
    //    different argument list (different number of args + different arg types)
    //    + different return type (optional)
    def eat(animal: Animal): Unit = println("I'm eating this poor fella")
    def eat(dog: Dog): Unit = println("eating a dog")
    def eat(person: Person): Unit = println(s"I'm eating a human with the name ${person.name}")
    def eat(person: Person, dog: Dog): Unit = println("I'm eating a human AND the dog")
    // def eat(): Int = 45 // not a valid overload
    def eat(dog: Dog, person: Person): Unit = println("I'm eating a human AND the dog")

  }

  def main(args: Array[String]): Unit = {
    println(dog) // println(dog.toString)

  }
}
```

## 16. Inheritance, continued: Abstract Classes and Traits.

```scala
package com.rockthejvm.part2oop

object AbstractDataTypes {

  abstract class Animal {
    val creatureType: String // abstract
    def eat(): Unit
    // non-abstract fields/methods allowed
    def preferredMeal: String = "anything" // "accessor methods"
  }

  // abstract classes can't be instantiated
  // val anAnimal: Animal = new Animal

  // non-abstract classes must implement the abstract fields/methods
  class Dog extends Animal {
    override val creatureType = "domestic"
    override def eat(): Unit = println("crunching this bone")
    // overriding is legal for everything
    override val preferredMeal: String = "bones" // overriding accessor method with a field
  }

  val aDog: Animal = new Dog

  // traits
  trait Carnivore { // Scala 3 - traits can have constructor args
    def eat(animal: Animal): Unit
  }

  class TRex extends Carnivore {
    override def eat(animal: Animal): Unit = println("I'm a T-Rex, I eat animals")
  }

  // practical difference abstract classes vs traits
  // one class inheritance
  // multiple traits inheritance
  trait ColdBlooded
  class Crocodile extends Animal with Carnivore with ColdBlooded {
    override val creatureType = "croc"
    override def eat(): Unit = println("I'm a croc, I just crunch stuff")
    override def eat(animal: Animal): Unit = println("croc eating animal")
  }

  /*
    philosophical difference abstract classes vs traits
    - abstract classes are THINGS
    - traits are BEHAVIORS
   */

  /*
    Any
      AnyRef
        All classes we write
          scala.Null (the null reference)
      AnyVal
        Int, Boolean, Char, ...


          scala.Nothing
   */

  val aNonExistentAnimal: Animal = null
  val anInt: Int = throw new NullPointerException

  def main(args: Array[String]): Unit = {

  }
}
```


## 17. Inheritance exercises: implementing our own Collection.



## 18. Generics.

```scala
package com.rockthejvm.part2oop

object Generics {

  // goal: reuse code on different types

  // option 1: copy the code
  abstract class IntList {
    def head: Int
    def tail: IntList
  }
  class EmptyIntList extends IntList {
    override def head = throw new NoSuchElementException
    override def tail = throw new NoSuchElementException
  }
  class NonEmptyIntList(override val head: Int, override val tail: IntList) extends IntList

  abstract class StringList {
    def head: String
    def tail: StringList
  }
  class EmptyStringList extends StringList {
    override def head = throw new NoSuchElementException
    override def tail = throw new NoSuchElementException
  }
  class NonEmptyStringList(override val head: String, override val tail: StringList) extends StringList
  // ... and so on for all the types you want to support
  /*
    Pros:
    - keeps type safety: you know which list holds which kind of elements
    Cons:
    - boilerplate
    - unsustainable
    - copy/paste... really?
   */

  // option 2: make the list hold a big, parent type
  abstract class GeneralList {
    def head: Any
    def tail: GeneralList
  }
  class EmptyGeneralList extends GeneralList {
    override def head = throw new NoSuchElementException
    override def tail = throw new NoSuchElementException
  }
  class NonEmptyGeneralList(override val head: Any, override val tail: GeneralList) extends GeneralList
  /*
    Pros:
    - no more code duplication
    - can support any type
    Cons:
    - lost type safety: can make no assumptions about any element or method
    - can now be heterogeneous: can hold cats and dogs in the same list (not funny)
   */

  // solution: make the list generic with a type argument
  abstract class MyList[A] { // "generic" list; Java equivalent: abstract class MyList<A>
    def head: A
    def tail: MyList[A]
  }

  class Empty[A] extends MyList[A] {
    override def head: A = throw new NoSuchElementException
    override def tail: MyList[A] = throw new NoSuchElementException
  }

  class NonEmpty[A](override val head: A, override val tail: MyList[A]) extends MyList[A]

  // can now use a concrete type argument
  val listOfIntegers: MyList[Int] = new NonEmpty[Int](1, new NonEmpty[Int](2, new Empty[Int]))

  // compiler now knows the real type of the elements
  val firstNumber = listOfIntegers.head
  val adding = firstNumber + 3

  // multiple type arguments
  trait MyMap[Key, Value]

  // generic methods
  object MyList {
    def from2Elements[A](elem1: A, elem2: A): MyList[A] =
      new NonEmpty[A](elem1, new NonEmpty[A](elem2, new Empty[A]))
  }

  // calling methods
  val first2Numbers = MyList.from2Elements[Int](1, 2)
  val first2Numbers_v2 = MyList.from2Elements(1, 2) // compiler can infer generic type from the type of the arguments
  val first2Numbers_v3 = new NonEmpty(1, new NonEmpty(2, new Empty))

  /**
   * Exercise: genericize LList.
   */

  def main(args: Array[String]): Unit = {

  }
}
```


## 19. Anonymous Classes.

```scala
package com.rockthejvm.part2oop

object AnonymousClasses {

  abstract class Animal {
    def eat(): Unit
  }

  // classes used for just one instance are boilerplate-y
  class SomeAnimal extends Animal {
    override def eat(): Unit = println("I'm a weird animal")
  }

  val someAnimal = new SomeAnimal

  val someAnimal_v2 = new Animal { // anonymous class
    override def eat(): Unit = println("I'm a weird animal")
  }

  /*
    equivalent with:

    class AnonymousClasses.AnonClass$1 extends Animal {
      override def eat(): Unit = println("I'm a weird animal")
    }

    val someAnimal_v2 = new AnonymousClasses.AnonClass$1
   */

  // works for classes (abstract or not) + traits
  class Person(name: String) {
    def sayHi(): Unit = println(s"Hi, my name is $name")
  }

  val jim = new Person("Jim") {
    override def sayHi(): Unit = println("MY NAME IS JIM!")
  }

  def main(args: Array[String]): Unit = {

  }
}
```


## 20. Object-oriented exercises: expanding our Collection.



## 21. Case Classes.

```scala
package com.rockthejvm.part2oop

object CaseClasses {

  // lightweight data structures
  case class Person(name: String, age: Int) {
    // do some other stuff
  }

  // 1 - class args are now fields
  val daniel = new Person("Daniel", 99)
  val danielsAge = daniel.age

  // 2 - toString, equals and hashCode
  val danielToString = daniel.toString // Person("Daniel", 99)
  val danielDuped = new Person("Daniel", 99)
  val isSameDaniel = daniel == danielDuped // true

  // 3 - utility methods
  val danielYounger = daniel.copy(age = 78) // new Person("Daniel", 78)

  // 4 - CCs have companion objects
  val thePersonSingleton = Person
  val daniel_v2 = Person("Daniel", 99) // "constructor"

  // 5 - CCs are serializable
  // use-case: Akka

  // 6 - CCs have extractor patterns for PATTERN MATCHING

  // can't create CCs with no arg lists
  /*
    case class CCWithNoArgs {
      // some code
    }

    val ccna = new CCWithNoArgs
    val ccna_v2 = new CCWithNoArgs // all instances would be equal!
  */

  case object UnitedKingdom {
    // fields and methods
    def name: String = "The UK of GB and NI"
  }

  case class CCWithArgListNoArgs[A]() // legal, mainly used in the context of generics

  /**
   * Exercise: use case classes for LList.
   */

  def main(args: Array[String]): Unit = {
    println(daniel)
    println(isSameDaniel)
  }
}
```


## 22. Scala 3: Enums.

```scala
package com.rockthejvm.part2oop

object Enums {

  enum Permissions {
    case READ, WRITE, EXECUTE, NONE

    // add fields/methods
    def openDocument(): Unit =
      if (this == READ) println("opening document...")
      else println("reading not allowed.")
  }

  val somePermissions: Permissions = Permissions.READ

  // constructor args
  enum PermissionsWithBits(bits: Int) {
    case READ extends PermissionsWithBits(4) // 100
    case WRITE extends PermissionsWithBits(2) // 010
    case EXECUTE extends PermissionsWithBits(1) // 001
    case NONE extends PermissionsWithBits(0) // 000
  }

  object PermissionsWithBits {
    def fromBits(bits: Int): PermissionsWithBits = // whatever
      PermissionsWithBits.NONE
  }

  // standard API
  val somePermissionsOrdinal = somePermissions.ordinal
  val allPermissions = PermissionsWithBits.values // array of all possible values of the enum
  val readPermission: Permissions = Permissions.valueOf("READ") // Permissions.READ

  def main(args: Array[String]): Unit = {
    somePermissions.openDocument()
    println(somePermissionsOrdinal)
  }
}
```


## 23. Exceptions.

```scala
package com.rockthejvm.part2oop

object Exceptions {

  val aString: String = null
  // aString.length crashes with a NPE

  // 1 - throw exceptions
  // val aWeirdValue: Int = throw new NullPointerException // returns Nothing

  // Exception hieararchy:
  //
  // Throwable:
  //    Error, e.g. SOError, OOMError
  //    Exception, e.g. NPException, NSEException, ....

  def getInt(withExceptions: Boolean): Int =
    if (withExceptions) throw new RuntimeException("No int for you!")
    else 42

  // 2 - catch exceptions
  val potentialFail = try {
    // code that might fail
    getInt(true) // an Int
  } catch {
    // most specific exceptions first
    case e: NullPointerException => 35
    case e: RuntimeException => 54 // an Int
    // ...
  } finally {
    // executed no matter what
    // closing resources
    // Unit here
  }

  // 3 - custom exceptions
  class MyException extends RuntimeException {
    // fields or methods
    override def getMessage = "MY EXCEPTION"
  }

  val myException = new MyException

  /**
   * Exercises:
   *
   * 1. Crash with SOError
   * 2. Crash with OOMError
   * 3. Find an element matching a predicate in LList
   */

  def soCrash(): Unit = {
    def infinite(): Int = 1 + infinite()
    infinite()
  }

  def oomCrash(): Unit = {
    def bigString(n: Int, acc: String): String =
      if (n == 0) acc
      else bigString(n - 1, acc + acc)

    bigString(56175363, "Scala")
  }


  def main(args: Array[String]): Unit = {
    println(potentialFail)
    // val throwingMyException = throw myException

    // soCrash()
    oomCrash()
  }
}
```


## 24. Packing and Imports.

```scala
package com.rockthejvm.part2oop

import scala.collection.SortedSet

// can define values and methods top-level
// they will be included in a synthetic object
// can be imported via an mypackage.* import
val meaningOfLife = 42
def computeMyLife: String = "Scala"

object PackagesImports { // top-level definition
  // packages = form of organization of definitions, similar to a folder structure in a normal file system

  // fully qualified name
  val aList: com.rockthejvm.practice.LList[Int] = ??? // throws NotImplementedError

  // import
  import com.rockthejvm.practice.LList
  val anotherList: LList[Int] = ???

  // importing under an alias
  import java.util.{List as JList}
  val aJavaList: JList[Int] = ???

  // import everything
  import com.rockthejvm.practice.*
  val aPredicate: Cons[Int] = ???

  // import multiple symbols
  import PhysicsConstants.{SPEED_OF_LIGHT, EARTH_GRAVITY}
  val c = SPEED_OF_LIGHT

  // import everything EXCEPT something
  object PlayingPhysics {
    import PhysicsConstants.{PLANCK as _, *}
    // val plank = PLANK // will not work
  }

  import com.rockthejvm.part2oop.* // import the mol and computeMyLife
  val mol = meaningOfLife

  // default imports:
  // scala.*, scala.Predef.*, java.lang.*

  // exports
  class PhysicsCalculator {
    import PhysicsConstants.*
    def computePhotonEnergy(wavelength: Double): Double =
      PLANCK / wavelength
  }

  object ScienceApp {
    val physicsCalculator = new PhysicsCalculator

    // exports create aliases for fields/methods to use locally
    export physicsCalculator.computePhotonEnergy

    def computeEquivalentMass(wavelength: Double): Double =
      computePhotonEnergy(wavelength) / (SPEED_OF_LIGHT * SPEED_OF_LIGHT)
      // ^^ the computePhotonEnergy method can be used directly (instead of physicsCalculator.computePhotonEnergy)
      // useful especially when these uses are repeated
  }

  def main(args: Array[String]): Unit = {
    // for testing
  }
}

// usually organizing "utils" and constants in separate objects
object PhysicsConstants {
  // constants
  val SPEED_OF_LIGHT = 299792458
  val PLANCK = 6.62e-34 // scientific notation
  val EARTH_GRAVITY = 9.8
}
```


## Functional Programming in Scala

## 25. What's a Function?



## 26. Anonymous Functions.



## 27. Higher-Order-Functions and Curries.



## 28. HOFs and Curries (exercises).




## 29. map, flatMap, filter and for-comprehensions.




## 30. A Collections Overview.




## 31. Sequences: List, Array, Vector.




## 32. Tuples and Maps.




## 33. Tuples and Maps (execises).




## 34. Options.




## 35. Handling Failure.




## Pattern Matching
 
## 36. Pattern Matching.




## 37. All the patterns.





## 38. Scala 3: braceless syntax.


