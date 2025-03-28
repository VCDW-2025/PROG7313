# 🌼 **Object-Oriented Programming**

---

## 🧩 What is OOP?

**OOP** is a programming paradigm where you structure code using:
- **Classes**: Blueprints for creating objects  
- **Objects**: Instances of classes  
- **Encapsulation**: Group related data and functions together  
- **Inheritance**: Create new classes based on existing ones  
- **Polymorphism**: Use a unified interface for different underlying objects

---

## 🧩 OOP Concepts in Kotlin (with Examples)

---

### 🧠 1. **Class and Object**

A **class** defines a structure; an **object** is an instance of a class.

```kotlin
class Car(val brand: String, val year: Int) {
    fun startEngine() {
        println("$brand engine started.")
    }
}

val myCar = Car("Mercedes", 2022)
myCar.startEngine()
```

---

### 🔨 2. **Constructor**

Kotlin uses **primary constructors** right in the class header.

```kotlin
class Student(val name: String, var age: Int)
val student = Student("Liam", 20)
```

---

### 🔐 3. **Encapsulation**

Use `private`, `protected`, `internal`, and `public` (default) to control access.

```kotlin
class BankAccount {
    private var balance: Double = 0.0

    fun deposit(amount: Double) {
        if (amount > 0) balance += amount
    }

    fun getBalance(): Double = balance
}
```

---

### 🧲 4. **Inheritance**

A class can inherit from another using `:` and the `open` modifier (because classes are final by default in Kotlin).

```kotlin
open class Animal {
    fun eat() = println("Animal is eating")
}

class Dog : Animal() {
    fun bark() = println("Dog is barking")
}

val dog = Dog()
dog.eat()
dog.bark()
```

---

### 🛠 5. **Polymorphism**

You can override a method to give different behavior.

```kotlin
open class Shape {
    open fun draw() = println("Drawing a shape")
}

class Circle : Shape() {
    override fun draw() = println("Drawing a circle")
}

fun render(shape: Shape) {
    shape.draw()
}

render(Shape())
render(Circle())
```

---

### 🧱 6. **Abstract Classes and Interfaces**

Use `abstract` for base classes with incomplete behavior, and `interface` for contracts.

```kotlin
abstract class Vehicle {
    abstract fun drive()
}

class Bike : Vehicle() {
    override fun drive() = println("Riding bike")
}

interface Clickable {
    fun click()
}

class Button : Clickable {
    override fun click() = println("Button clicked")
}
```

---

## 📌 Summary

| Concept              | Purpose                                      |
|----------------------|----------------------------------------------|
| Class/Object         | Blueprint and instance                       |
| Encapsulation        | Hide internal state                          |
| Inheritance          | Reuse and extend existing classes            |
| Polymorphism         | Shared interface, different behavior         |
| Abstract/Interface   | Design contracts or incomplete blueprints    |

