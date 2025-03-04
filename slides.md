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
You can call java code from kotlin and kotlin code from java no problem.

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
layout: section
---
# Time for some code

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
variables are declared like this, using a type syntax that is quite familiar for typescript 
users with the type declared after the variable name.

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
meaning that the compiler will not allow us to reassign the values after the object has
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
println(eirik)
// Person(firstName=Eirik, lastName=Rognø)

val impostor = eirik.copy(lastName = "Rognæ")
```

<!--

When creating simple classes to hold data like this, we can use the keyword "data" class.

This implements several default methods that you normally need for such classes, like
toString, hashCode/equals, copy, as well as what is known as componentN functions used for 
destructuring member fields.

Here we can see some examples of these in use, we can read firstName and lastName directly
into to variables using destructuring. The toString method will print on the format displayed 
in the comment line here, where as the copy function give you a new object containing all the 
same fields, except the one you choose to override in the function call.

I for instanceoften use the copy function when writing tests, making 
it easy to change some fields before running a specific test case on some data
-->

---
layout: center
zoom: 2
---

```kotlin
val greeting = "Hello ${person.firstName}!"
// Hello Eirik!
```

<!--
Here is a little nicetiy that I thought I would mention: Kotlin has support
for string templating out of the box in normal string  like this.
-->

---
layout: center
zoom: 1.5
---

```kotlin
data class Address(
  val streetName: String,
  val number: Int?,
  val postalCode: String?
)

data class Person(
  val firstName: String,
  val lastName: String,
  val address: Address? = null
)

val eirik = Person(firstName = "Eirik", lastName = "Rognø")
val streetName = eirik.address.streetName // Compiler error

val streetName = eirik.address?.streetName // null
val streetName = eirik.address?.streetName ?: "Unknown" // "Unknown"
```

<!--
Okay, now for some more info about the null safety features of kotlin.
Whenever we declare a type in Kotlin, we can declare it as either nullable, or
non-nullable. The default is that a type is non-nullable. If we want it to be nullable
we add a question mark after the type declariation.

Here we have two data classes, one containing information about an Address, and another
containing information about a person, including a field with type Address. The address field 
on the Person object is a nullable type. And note also that I have added a default parameter.
The default parameter means that you can skip this field when calling the constructor and get
that default instead.

Here I have instatiated an object of type Person. If I know try to access fields within the 
nullable type I would get a compiler error right away screaming at me in the editor. 

The closest comparison to this behaviour in java is the Optional type, but while you will get 
warnings for accessing a value without checking if it is present, you can still ignore that 
warning if you like. Also they are very much an opt-in feature of the language, meaning that
you have to decide to use it everytime.

So: what if I want to access the streetName field through the person object? Then I can use 
what is known as the safe call operator where I put a question mark before the dot when 
accessing a field. This will return null for the entire expression when address is null, 
and only access the field if not. If you have several layers of nullable fields you can chain
these together.

Another fun operator is what is known as the elvis operator, which consists of a question mark
and a colon. This operator means: return the expression on the right if the expression on the 
expression on the left resolves to null. So in this case: because address field is null, the 
entire expression will be null on the left hand side and "Unknown" is returned.

One thing to note here is that for the two last lines here the type for the first is String?, 
while the second is String without question mark, since it always will return a string.

-->
---
layout: center
zoom: 2
---

```kotlin
var streetName;
if (eirik.address != null) { 
  // Address field is smart cast from Address? to Address 
  streetName = eirik.address.streetName
}

val streetName = eirik.address!!.streetName
```
<!--
Another way to deal with nullable fields is to do a null check. Here Kotlin will actually smart
cast the Address field to a non nullable type inside the if block with the null check. Making
the direct access on the streetName field okay again.

There is also a specific operator in kotlin with two exclamation marks, this operator just 
means: throw null pointer exception if this is null. This is mostly there for very specific
cases where you know something is not null, but the compiler doesn't. I would not recommend 
using this as you cannot be sure that your assumptions are true or that the code surrounding 
it will not change independently. Basically you are opting out of the built in null safety in 
that case.
-->
---
layout: center
zoom: 2
---
<div class="mb-8">
```java
public class Greeter {
  public static String createGreeting(String name) {
    return "Hello " + name;
  }
}
```
</div>


<div>
```kotlin
fun createGreeting(name: String): String {
  return "Hello $name"
}

fun createGreeting(name: String): String = "Hello $name"

```
</div>

<!--
Functions! Functions in kotlin are created using the keyword "fun" which is of course
very fun. And by default you have public fun.
Unlike Java you can actually declare functions at the top level in a file, you do not 
need to declare them inside a class. So the static static method in the java code
at the top here would be equivialent just declaring the function directly like this in 
Kotlin. If a function only contains a single expression you can omit the curly brackets
and use an equals sign instead like this.
-->
---
layout: center
zoom: 2
---

```kotlin
fun printGreeting(name: String): Unit {
  println("Hello $name")
}

fun printGreeting(name: String = "World") {
  println("Hello $name")
}

printGreeting(name = "Eirik")
```

<!--
If a function does not return anything, the return type is "Unit" which is the Kotlin 
equivalent of void. This is also the default when declaring a function, so the return
type can be omitted in those cases.

Functions also support default parameters and being called with named parameters, just
like the class constructors we saw earlier.
-->

---
layout: center
zoom: 2
---

<div class="mb-8">
```java
// Java
(String x) -> {System.out.println(x);}
```
</div>

<div class="mb-8">
```kotlin
// Kotlin
{ x: String -> println(x) }
{ println(it) } // Default param "it"
```
</div>

<!-- 
Here is a comparison of java vs kotlin lambdas.
In kotlin the paramater is specified within the curly brackets. In addition, you can
in many cases skip the paramter, and use the implicit default parameter "it".
This is very nice when doing things like map and filter on collections, which we 
will get to later.
-->

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
zoom: 1.5
---

```kotlin
interface Job {
    val workplace: String

    fun getTitle(): String

    fun printWorkplace() {
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
## WHEN

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