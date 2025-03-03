---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
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
---
# What is Kotlin

* Developed by JetBrains
* First revealed in 2011
* Version 1 released in 2016
* Fully compatible with JVM
* Widely used for Android development
* Type inference
* Less boilerplate
* Functional and object oriented
---
---
## Null safety

Bilde fra elastic på NPE i prod?
Million dollar mistake osv.

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
    fun is used to declare a function

    The main() function is where your program starts from

    The body of a function is written within curly braces {}

    println() and print() functions print their arguments to standard output
-->
---
zoom: 2
layout: center
---
### Types and variables

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

---
zoom: 2
layout: center
---

<div>
```kotlin
// Kotlin
val name: String = "Tryg"
name = "Enter" // Compiler error

var name: String = "Enter"
name = "Tryg"
```
</div>

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
---
layout: center
zoom: 2
---

```kotlin
class Person(
  val firstName: String,
  val lastName: String
)
```
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
---
## Companion objects
---
layout: center
---
## Extension functions

---
layout: center
---
## Collections <3

Map, filter, find, group by, lambdas



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