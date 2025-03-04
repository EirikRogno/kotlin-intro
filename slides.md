---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/jtsW--Z6bFw.webp
# some information about your slides (markdown enabled)
title: Kotlin - TeFT 2025
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: none
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

# Kotlin 

Javas Cool younger sibling


<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->
---
layout: image-right
image: https://cdn.jsdelivr.net/gh/slidevjs/slidev-covers@main/static/aQcE3gDSSTY.webp
---
# What is Kotlin

- First revealed in 2011
- Originally created by JetBrains
- Version 1 released in 2016
- Fully compatible with JVM
- Null safe language
- Less boilerplate compared to Java
- Functional and object oriented

<!--
Kotlin is a cross-platform, statically typed, general-purpose high-level programming language with type inference.

It was originally created by the company JetBrains (known for IntelliJ among others)

Similar to how Java shares a name with an island in Indonesia, Kotlin is named after a small
island outside St. Petersburg

The language is fully compatible with the jvm.

It is null safe (which I will talk more about later)

It has a less verbose syntax than java, and skips a lot of the boilerplate code

It supports both functional and object oriented paradigms


Tony Hoare who was one of the creators of the Algol W programming language, has refered to his invention of the null pointer as "The Billion dollar mistake", because of all the bugs and unintended consequences this has caused.
-->

---
layout: image
image: ./SN_nullpointers.PNG
backgroundSize: contain
---
<!--
Here we see a little search from SN in production for "NullPointerException" over 24 hours, 2764 instances found
-->

---
layout: center
zoom: 3
---

```kotlin
fun main() {
    println("Hello, world!")
    // Hello, world!
}
```
<!--
  Alright, time to look at some kotlin

  fun is used to declare a function
  The main() function is where your program starts from (simpler than javas?)
  The body of a function is written within curly braces {}
  println() and print() functions print their arguments to standard output
-->
---
zoom: 2
layout: center
---
<div class="my-8">
```java
// Java
String name = "Tryg"
```
</div>


<div>
```kotlin
// Kotlin
val name: String = "Tryg"
val name = "Tryg"
```
</div>

<!--
variables are declared like this, using a type syntax that is quite familiar for typescrypt users with the type after a colon.

Because of kotlins type inference, we can in many cases skip the explicit typing. When we assign a string to a variable, that is enough for the compiler to know that the variable is a string.

If this is confusing in larger scale projects, you can turn on type hints in intelliJ, wich will show the types that are inferred in gray next to variables in your editor
-->

---
zoom: 2
layout: center
---

```kotlin
// Kotlin
val name: String = "Tryg"
name = "Enter" // Compiler error

var name: String = "Enter"
name = "Tryg"
```

<!--
In kotlin variables can be either mutable or immutable, this is defined using either
the val or the var keyword. If you try to reassign an immutable variable, the compiler will
give you an error. In general it is recommended to use the immutable val keyword, unless you
have a specific need for mutating a variable.
-->

---
layout: center
zoom: 1.5
---
```java
public class Person {
  private String firstName;
  private String lastName;

  public Person(String firstName, String lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  
  public String getFirstName() {
    return this.firstName;
  }

  public String getLastName() {
    return this.lastName;
  }
  
}
```

<!--
Over to classes, here we have a basic class in Java, that defines a person, 
with both a first and a last name. The values are initialized in the constructor,
and have a getter each.

-->
---
layout: center
zoom: 2
---

```kotlin
class Person(
  val firstName: String,
  val lastName: String
)

val eirik = Person(firstName = "Eirik", lastName = "Rognø")
val firstName = eirik.firstName

eirik.firstName = "Erik" // Compiler error
```
<!--
In kotlin you would define the class like this. We do not need any body for this class, 
as it only contains two fields. Kotlin will provide us with a default constructor
which you can see used under the class definition here.

Note also the support for using named parameters. When specifiyng the contructor inputs in 
this way the order does not matter. This is very useful when instanciating classes with many 
fields or also when calling functions with several arguments. Kotlin also doesn't use the new
keyword when calling constructors.

In kotlin you don't need to creat getters and setters for your class fields, although there is also support for that if you have custom needs. 
But for a simple data container class like this we can just access the fields on an object
directly. And since they where declare using the "val" keyword, they are also immutable, 
meaning that the compiler will nott allow us to reassign the values after the object has
been created.
-->
---
layout: center
zoom: 2
---

```kotlin
data class Person(
  val firstName: String,
  val lastName: String
)

val eirik = Person(firstName = "Eirik", lastName = "Rognø")
val (firstName, lastName) = eirik
```

<!--
Implements default toString, hashCode, copy

-->

---
layout: center
zoom: 2
---

```kotlin
data class Person(
  val firstName: String,
  val lastName: String
)

val eirik = Person(firstName = "Eirik", lastName = "Rognø")
val greeting = "Hello ${person.firstName}!"
// Hello Eirik!
```

---
layout: center
zoom: 1.5
---

```kotlin
data class Person(
  val firstName: String,
  val lastName: String,
  val address: Address? = null
)

data class Address(
  val streetName: String,
  val number: Int?,
  val postalCode: String?
)

val eirik = Person(firstName = "Eirik", lastName = "Rognø")
val streetName = eirik.address.streetName // Compiler error

val streetName = eirik.address?.streetName
// null
val streetName = eirik.address?.streetName ?: "Unknown"
// "Unknown"
```

<!--
Null chaining, let?, elvis operator, smart casts, compiler errors
-->
---
layout: center
zoom: 1.5
---

```kotlin
data class Person(
  val firstName: String,
  val lastName: String,
  val address: Address? = null
)

data class Address(
  val streetName: String,
  val number: Int?,
  val postalCode: String?
)

val eirik = Person(firstName = "Eirik", lastName = "Rognø")
val streetName = eirik.address.streetName // Compiler error

var streetName;
if (eirik.address != null) { 
  // Address field is smart cast from Address? to Address 
  streetName = eirik.address.streetName
}

```

<!--
Null chaining, let?, elvis operator, smart casts, compiler errors
-->
---
layout: center
zoom: 2
---
<div class="mb-8">
```java
public String createGreeting(String name) {
  return "Hello " + name;
}
```
</div>



<div>
```kotlin
fun createGreeting(name: String): String {
  return "Hello $name";
}

fun createGreeting(name: String): String = "Hello $name"

```
</div>


<!--
Named params, default params, higher-order functions
-->

---
layout: center
zoom: 2
---

<div class="mb-8">
```java
(String x) -> System.out.println(x);
```
</div>

<div class="mb-8">
```kotlin
{ x: String -> println(x) }
{ println(it) } // Default param "it"
```
</div>


---
layout: center
zoom: 2
---

```java
interface Job {
  public String getTitle();
}

class Developer implements Job {

  @Override
  public String getTitle() {
    return "Developer";
  }
}
```

<!--
Inheritance

Extending, overriding, abstract classes and interfaces
-->

---
layout: center
zoom: 2
---

```kotlin
interface Job {
  fun getTitle(): String
}

class Developer : Job {
  override fun getTitle(): String = "Developer"
}
```
---
layout: center
zoom: 1.7
---

```kotlin
interface Job {
  private val workplace: String

  fun getTitle(): String
  
  fun printWorkplace: String {
    println(workplace)
  }
}

class Developer(override val workplace: String = "Office") : Job {
  override fun getTitle(): String = "Developer"
}
```

<!--
In kotlin interfaces can have default implementations for methods and also ,
combining features of java abstract classes and interfaces.

Abstract classes in kotlin can have fields and constructors

also the syntax for "extends" and "implements" is the same, the difference is given by the type implemented
-->
---
layout: center
zoom: 2
---
```java
List<String> strings = Arrays.asList(
  "hello",
  "asdf",
  "qwerty",
  null,
  "123"
);

strings.stream()
    .filter(s -> s != null)
    .map(s -> s.toUpperCase())
    .toList();
```


<!--
Map, filter, find, group by, lambdas
-->
---
layout: center
zoom: 2
---
```kotlin
// Inferred type will be List<String?>
val strings = listOf(
  "hello",
  "asdf",
  "qwerty",
  null,
  "123"
)

strings
    .filter({s -> s != null})
    .map({s -> s?.uppercase()})
```

<!--
-->
---
layout: center
zoom: 2
---
```kotlin
// Inferred type will be List<String?>
val strings = listOf(
  "hello",
  "asdf",
  "qwerty",
  null,
  "123"
)

strings
    .filter { it != null }
    .map { it?.uppercase() }
```

<!--
-->
---
layout: center
zoom: 2
---
```kotlin
// Inferred type will be List<String?>
val strings = listOf(
  "hello",
  "asdf",
  "qwerty",
  null,
  "123"
)
// Inferred type of return here is List<String>
strings
    .filterNotNull()
    .map { it.uppercase() }

strings
    .mapNotNull { it?.uppercase() }

```

<!--
-->
---
layout: center
zoom: 2
---
```kotlin
// Inferred type will be List<String?>
val strings = listOf(
  "hello",
  "asdf",
  "qwerty",
  null,
  "123"
)
// Inferred type of return here is List<String>
strings
    .filterNotNull()
    .map { it.uppercase() }

strings
    .mapNotNull { it?.uppercase() }

```

<!--
-->
---
layout: center
zoom: 2
---
```kotlin
data class Person(
    val firstName: String,
    val lastName: String,
    val age: Int
)

val people = listOf(
    Person("Anders", "Hansen", 32),
    Person("Synne", "Hansen", 30),
    Person("Ronny", "Hansen", 64),
    Person("Siri", "Fredriksen", 65),
    Person("Johnny", "Fredriksen", 33),
)
```

<!--
-->
---
layout: center
zoom: 1.5
---
```kotlin
val families = people
    .groupBy { it.lastName }
/*
{
  Hansen=[
    Person(firstName=Anders, lastName=Hansen, age=32),
    Person(firstName=Synne, lastName=Hansen, age=30),
    Person(firstName=Ronny, lastName=Hansen, age=64)
  ],
  Fredriksen=[
    Person(firstName=Siri, lastName=Fredriksen, age=65),
    Person(firstName=Johnny, lastName=Fredriksen, age=33)
  ]
}
*/
```

<!--
-->
---
layout: center
zoom: 1.5
---
```kotlin

val oldest = people.maxBy { it.age }
// Person(firstName=Siri, lastName=Fredriksen, age=65)

val ronny = people.find { it.firstName == "Ronny" }
// Person(firstName=Ronny, lastName=Hansen, age=64)
// this one returns type String?
```

<!--
-->
---
layout: center
zoom: 1.7
---

<div class="mb-8">
```java
public class Util {
    public static void printNumbers(List<Integer> numbers) {
      numbers.forEach(System.out::println);
    }
}

```
</div>

<div>
```kotlin
class Util {
  companion object {
    fun printNumbers(numbers: List<Int>) {
      numbers.forEach { println(it) }
    }
  }
}
```
</div>

<!--
Companion objects, similar to javas static fields or static methods
-->
---
layout: center
zoom: 2
---

```kotlin
fun printNumbers(numbers: List<Int>) {
  numbers.forEach { println(it) }
}
```

<!--
Kotlin supports functional paradigms so you can just declare util functions directly
outside classes
-->
---
layout: center
zoom: 1.7
---

```kotlin
data class Person(val firstName: String, val lastName: String) {
  companion object {
    fun from(data: Map<String, String>) = Person(
      firstName = data.getOrDefault("FirstName", "Unknown"),
      lastName = data.getOrDefault("LastName", "Unknown"),
    )
  }
}

val eirik = Person.from(mapOf(
  "FirstName" to "Eirik",
  "LastName" to "Rognø"
))
// Person(firstName=Eirik, lastName=Rognø)
```
<!--
I like to use companion objects for instantion from other classes for instance,
here I am again using type inference for the function return (Person), 
and using named parameters,
and skipping curly brackets since the function is a single statement
-->
---
layout: center
---
## Extension functions



---
layout: center
---

### Last part: Spring boot examples

---
layout: center
---
## Further resources
* https://play.kotlinlang.org/byExample

Courses, documentation, simplest service in tip?, link to this presentation
---