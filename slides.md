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
```

```kotlin
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
  val adress: Adress? = null
)

data class Adress(
  val streetName: String,
  val number: Int?,
  val postalCode: String?
)

val eirik = Person(firstName = "Eirik", lastName = "Rognø")
val streetName = eirik.adress.streetName // Compiler error

val streetName = eirik.adress?.streetName
// null
val streetName = eirik.adress?.streetName ?: "Unknown"
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
  val adress: Adress? = null
)

data class Adress(
  val streetName: String,
  val number: Int?,
  val postalCode: String?
)

val eirik = Person(firstName = "Eirik", lastName = "Rognø")
val streetName = eirik.adress.streetName // Compiler error

var streetName;
if (eirik.adress != null) { 
  // Adress field is smart cast from Adress? to Adress
  streetName = eirik.adress.streetName
}

```

<!--
Null chaining, let?, elvis operator, smart casts, compiler errors
-->
---
layout: center
---
## Inheritance

Extending, overriding, abstract classes and interfaces

---
layout: center
---
## Companion objects
---
layout: center
---
## Functions

Named params, default params, higher-order functions

---
layout: center
---
## Extension functions

---
layout: center
---
## Lambdas

Default param, shorthand for lambda arguments

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