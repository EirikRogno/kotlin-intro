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
* Null safety
* Type inference
* Less boilerplate
* Functional and object oriented

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
name = "Enter"

var name: String = "Enter"
name = "Tryg"
```
</div>

---
layout: center
---
## Functions

---
layout: center
---
## Classes
---
layout: center
---
## Data classes
---
layout: center
---
## Inheritance
---