# 📚 Java Complete Guide - From Basics to Advanced

## Table of Contents

### Core Java Levels
- [Level 1: Fundamentals](#📗-level-1-fundamentals)
- [Level 2: Object-Oriented Programming](#📘-level-2-object-oriented-programming)
- [Level 3: Core APIs](#📙-level-3-core-apis)
- [Level 4: Collections Framework](#📕-level-4-collections-framework)
- [Level 5: Multithreading & Concurrency](#📕-level-5-multithreading--concurrency)
- [Level 6: SOLID Principles](#📕-level-6-solid-principles)
- [Level 7: Design Patterns](#📕-level-7-design-patterns)
- [Level 8: Spring Framework](#📕-level-8-spring-framework)
- [Level 9: Annotations](#📕-level-9-annotations)

### Collections Framework
- [Performance Comparison](#📊-performance-comparison)
- [Key Takeaways](#🎯-key-takeaways)
- [Interview Tips](#🚀-interview-tips)
- [Collection Trade-offs Decision Guide](#🎯-collection-trade-offs-decision-guide)

### Design Patterns
- [Creational Patterns](#creational-patterns) (Singleton, Factory, Builder)
- [Structural Patterns](#structural-patterns) (Adapter, Decorator, Facade)
- [Behavioral Patterns](#behavioral-patterns) (Observer, Strategy, Command, Template)
- [Design Patterns Comparison](#📊-design-patterns-comparison)
- [Pattern Selection Guide](#🎓-pattern-selection-guide)

### Spring Framework
- [Spring Core Concepts](#spring-core-concepts) (DI, Bean Lifecycle, Scopes)
- [Spring Boot](#spring-boot) (Auto-configuration, REST Controllers)
- [Spring Data JPA](#spring-data-jpa) (Entities, Repositories, Relationships)
- [Spring AOP](#spring-aop-aspect-oriented-programming) (Aspects, Advice, Pointcuts)
- [Spring Security](#spring-security) (JWT, Authentication, Authorization)
- [Scheduling & Cron Jobs](#scheduling--cron-jobs)
- [Spring Boot Actuator](#spring-boot-actuator)
- [Spring Validation](#spring-validation)
- [Spring Transactions](#spring-transactions)
- [Spring Profiles](#spring-profiles)
- [Spring Boot Testing](#spring-boot-testing)
- [Spring Interview Questions](#spring-interview-questions)

### Annotations
- [How Annotations Work](#how-annotations-work)
- [Creating Custom Annotations](#creating-custom-annotations)
- [Annotation Processing](#how-spring-processes-annotations)

### Complete Project
- [Task Management API](#🎯-complete-spring-boot-project) (Full working project)

---

## 📗 LEVEL 1: FUNDAMENTALS

### 1. Data Types & Variables

**What are they?**  
Data types define what kind of data a variable can hold. Java has two categories:

#### Primitive Types (8 types)
- **Numeric**: `byte`, `short`, `int`, `long`, `float`, `double`
- **Character**: `char`
- **Boolean**: `boolean`

#### Reference Types
- Classes, Interfaces, Arrays

```java
// Primitives - store actual values
int age = 25;                    // Integer (4 bytes)
double salary = 50000.50;        // Decimal numbers (8 bytes)
char grade = 'A';                // Single character (2 bytes)
boolean isActive = true;         // true or false (1 bit)

byte b = 127;                    // -128 to 127 (1 byte)
short s = 32000;                 // -32,768 to 32,767 (2 bytes)
long population = 7800000000L;   // Very large numbers (8 bytes)
float pi = 3.14f;                // Decimal (4 bytes)

// Reference Types - store memory address
String name = "John";            // String is a class (reference type)
int[] numbers = {1, 2, 3};       // Array (reference type)
```

#### Type Conversion

```java
// Implicit (Automatic) - smaller to larger
int num = 100;
double d = num;                  // int → double (automatic)
System.out.println(d);           // 100.0

// Explicit (Manual Casting) - larger to smaller
double price = 99.99;
int rupees = (int) price;        // double → int (needs casting)
System.out.println(rupees);      // 99 (decimal part lost)

// String to Number
String str = "123";
int number = Integer.parseInt(str);
double decimal = Double.parseDouble("45.67");

// Number to String
String s1 = String.valueOf(number);
String s2 = Integer.toString(number);
```

---

### 2. Operators

#### Arithmetic Operators
```java
int a = 10, b = 3;
System.out.println(a + b);       // 13 (Addition)
System.out.println(a - b);       // 7  (Subtraction)
System.out.println(a * b);       // 30 (Multiplication)
System.out.println(a / b);       // 3  (Division - integer)
System.out.println(a % b);       // 1  (Modulus - remainder)

// Unary operators
int x = 5;
System.out.println(++x);         // 6 (pre-increment)
System.out.println(x++);         // 6 (post-increment, then x becomes 7)
System.out.println(--x);         // 6 (pre-decrement)
System.out.println(x--);         // 6 (post-decrement, then x becomes 5)
```

#### Relational (Comparison) Operators
```java
int p = 10, q = 20;
System.out.println(p == q);      // false (equal to)
System.out.println(p != q);      // true  (not equal to)
System.out.println(p > q);       // false (greater than)
System.out.println(p < q);       // true  (less than)
System.out.println(p >= q);      // false (greater than or equal)
System.out.println(p <= q);      // true  (less than or equal)
```

#### Logical Operators
```java
boolean isAdult = true;
boolean hasLicense = false;

// AND - both must be true
System.out.println(isAdult && hasLicense);    // false

// OR - at least one must be true
System.out.println(isAdult || hasLicense);    // true

// NOT - reverses the value
System.out.println(!isAdult);                  // false
```

#### Assignment Operators
```java
int num = 10;
num += 5;                        // num = num + 5  → 15
num -= 3;                        // num = num - 3  → 12
num *= 2;                        // num = num * 2  → 24
num /= 4;                        // num = num / 4  → 6
num %= 4;                        // num = num % 4  → 2
```

#### Ternary Operator
```java
int age = 18;
String result = (age >= 18) ? "Adult" : "Minor";
System.out.println(result);      // Adult
```

#### Bitwise Operators
```java
int m = 5;   // 0101 in binary
int n = 3;   // 0011 in binary

System.out.println(m & n);       // 1 (AND: 0001)
System.out.println(m | n);       // 7 (OR:  0111)
System.out.println(m ^ n);       // 6 (XOR: 0110)
System.out.println(~m);          // -6 (NOT: inverts bits)
System.out.println(m << 1);      // 10 (Left shift: 1010)
System.out.println(m >> 1);      // 2  (Right shift: 0010)
```

#### Operator Precedence (High to Low)
1. Postfix: `expr++`, `expr--`
2. Unary: `++expr`, `--expr`, `+`, `-`, `!`, `~`
3. Multiplicative: `*`, `/`, `%`
4. Additive: `+`, `-`
5. Shift: `<<`, `>>`, `>>>`
6. Relational: `<`, `>`, `<=`, `>=`
7. Equality: `==`, `!=`
8. Bitwise AND: `&`
9. Bitwise XOR: `^`
10. Bitwise OR: `|`
11. Logical AND: `&&`
12. Logical OR: `||`
13. Ternary: `? :`
14. Assignment: `=`, `+=`, `-=`, etc.

---

### 3. Control Flow

#### if/else Statements
```java
int marks = 85;

if (marks >= 90) {
    System.out.println("Grade: A+");
} else if (marks >= 80) {
    System.out.println("Grade: A");
} else if (marks >= 70) {
    System.out.println("Grade: B");
} else {
    System.out.println("Grade: C");
}
```

#### switch Statement
```java
int day = 3;
String dayName;

switch (day) {
    case 1:
        dayName = "Monday";
        break;
    case 2:
        dayName = "Tuesday";
        break;
    case 3:
        dayName = "Wednesday";
        break;
    default:
        dayName = "Invalid day";
}

// Enhanced switch (Java 14+)
String result = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    default -> "Invalid day";
};
```

#### for Loop
```java
// Traditional for loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);           // 0, 1, 2, 3, 4
}

// Enhanced for loop (for-each)
int[] numbers = {10, 20, 30, 40};
for (int num : numbers) {
    System.out.println(num);
}
```

#### while Loop
```java
int count = 0;
while (count < 5) {
    System.out.println(count);
    count++;
}
```

#### do-while Loop
```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);

// Executes at least once even if condition is false
int j = 10;
do {
    System.out.println("Runs once");  // Prints even though condition is false
} while (j < 5);
```

#### Jump Statements
```java
// break - exits the loop
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    System.out.println(i);           // 0, 1, 2, 3, 4
}

// continue - skips current iteration
for (int i = 0; i < 5; i++) {
    if (i == 2) continue;
    System.out.println(i);           // 0, 1, 3, 4
}

// return - exits from method
public int findNumber(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;                // Returns immediately
        }
    }
    return -1;
}

// Labeled break (for nested loops)
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == 1 && j == 1) {
            break outer;             // Breaks out of outer loop
        }
        System.out.println(i + "," + j);
    }
}
```

---

### 4. Arrays

#### 1D Arrays
```java
// Declaration and initialization
int[] numbers = new int[5];          // Array of size 5
numbers[0] = 10;
numbers[1] = 20;

// Direct initialization
int[] nums = {10, 20, 30, 40, 50};

// Accessing elements
System.out.println(nums[0]);         // 10
System.out.println(nums.length);     // 5

// Iterating through array
for (int i = 0; i < nums.length; i++) {
    System.out.println(nums[i]);
}

// Enhanced for loop
for (int num : nums) {
    System.out.println(num);
}
```

#### 2D Arrays (Matrix)
```java
// Declaration
int[][] matrix = new int[3][4];      // 3 rows, 4 columns

// Direct initialization
int[][] grid = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Accessing elements
System.out.println(grid[0][0]);      // 1
System.out.println(grid[1][2]);      // 6

// Iterating
for (int i = 0; i < grid.length; i++) {
    for (int j = 0; j < grid[i].length; j++) {
        System.out.print(grid[i][j] + " ");
    }
    System.out.println();
}

// Enhanced for loop
for (int[] row : grid) {
    for (int val : row) {
        System.out.print(val + " ");
    }
    System.out.println();
}
```

#### Jagged Arrays (Irregular Arrays)
```java
// Different number of columns in each row
int[][] jagged = new int[3][];
jagged[0] = new int[2];              // Row 0 has 2 columns
jagged[1] = new int[4];              // Row 1 has 4 columns
jagged[2] = new int[3];              // Row 2 has 3 columns

// Direct initialization
int[][] irregular = {
    {1, 2},
    {3, 4, 5, 6},
    {7, 8, 9}
};

// Printing jagged array
for (int i = 0; i < irregular.length; i++) {
    for (int j = 0; j < irregular[i].length; j++) {
        System.out.print(irregular[i][j] + " ");
    }
    System.out.println();
}
```

#### Arrays Utility Class
```java
import java.util.Arrays;

int[] arr = {5, 2, 8, 1, 9};

// Sort
Arrays.sort(arr);
System.out.println(Arrays.toString(arr));  // [1, 2, 5, 8, 9]

// Binary Search (array must be sorted)
int index = Arrays.binarySearch(arr, 5);
System.out.println(index);                 // 2

// Fill
int[] filled = new int[5];
Arrays.fill(filled, 10);
System.out.println(Arrays.toString(filled)); // [10, 10, 10, 10, 10]

// Copy
int[] copy = Arrays.copyOf(arr, arr.length);
int[] partialCopy = Arrays.copyOfRange(arr, 1, 4);

// Compare
int[] arr1 = {1, 2, 3};
int[] arr2 = {1, 2, 3};
boolean isEqual = Arrays.equals(arr1, arr2);  // true

// Convert to String
System.out.println(Arrays.toString(arr));
```

---

### 5. Methods

**What are methods?**  
Methods are blocks of code that perform specific tasks. They help organize code and make it reusable.

```java
// Basic method structure
public static int add(int a, int b) {
    return a + b;
}

// Calling the method
int result = add(5, 3);              // 8

// Method with no return value
public static void greet(String name) {
    System.out.println("Hello, " + name);
}

greet("Alice");                      // Hello, Alice
```

#### Method Overloading
**Same method name, different parameters**

```java
public class Calculator {
    // Method 1: Add two integers
    public int add(int a, int b) {
        return a + b;
    }
    
    // Method 2: Add three integers
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Method 3: Add two doubles
    public double add(double a, double b) {
        return a + b;
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 3));           // 8
        System.out.println(calc.add(5, 3, 2));        // 10
        System.out.println(calc.add(5.5, 3.2));       // 8.7
    }
}
```

#### Varargs (Variable Arguments)
**Accept variable number of arguments**

```java
public class VarargsExample {
    // Method that accepts variable number of arguments
    public static int sum(int... numbers) {
        int total = 0;
        for (int num : numbers) {
            total += num;
        }
        return total;
    }
    
    public static void main(String[] args) {
        System.out.println(sum(1, 2));                // 3
        System.out.println(sum(1, 2, 3));             // 6
        System.out.println(sum(1, 2, 3, 4, 5));       // 15
    }
}

// Rules for varargs:
// 1. Varargs must be the last parameter
// 2. Only one varargs per method
public void display(String message, int... numbers) {
    // Valid
}
```

#### Recursion
**A method calling itself**

```java
public class RecursionExample {
    // Factorial using recursion
    public static int factorial(int n) {
        if (n == 0 || n == 1) {           // Base case
            return 1;
        }
        return n * factorial(n - 1);      // Recursive call
    }
    
    // Fibonacci using recursion
    public static int fibonacci(int n) {
        if (n <= 1) {                     // Base case
            return n;
        }
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
    
    // Sum of digits
    public static int sumOfDigits(int num) {
        if (num == 0) {
            return 0;
        }
        return num % 10 + sumOfDigits(num / 10);
    }
    
    public static void main(String[] args) {
        System.out.println(factorial(5));          // 120
        System.out.println(fibonacci(6));          // 8
        System.out.println(sumOfDigits(123));      // 6
    }
}
```

---

## 📘 LEVEL 2: OBJECT-ORIENTED PROGRAMMING

### 1. Classes & Objects

**Class**: Blueprint/Template for creating objects  
**Object**: Instance of a class (actual entity)

```java
// Class definition
public class Car {
    // Instance variables (attributes)
    String brand;
    String color;
    int year;
    
    // Constructor - special method to initialize object
    public Car(String brand, String color, int year) {
        this.brand = brand;           // 'this' refers to current object
        this.color = color;
        this.year = year;
    }
    
    // Method
    public void displayInfo() {
        System.out.println(brand + " " + color + " " + year);
    }
    
    public void honk() {
        System.out.println(brand + " says: Beep beep!");
    }
}

// Creating objects
public class Main {
    public static void main(String[] args) {
        // Creating objects using constructor
        Car car1 = new Car("Toyota", "Red", 2020);
        Car car2 = new Car("Honda", "Blue", 2021);
        
        car1.displayInfo();           // Toyota Red 2020
        car1.honk();                  // Toyota says: Beep beep!
        
        car2.displayInfo();           // Honda Blue 2021
    }
}
```

#### Constructors

```java
public class Student {
    String name;
    int age;
    String course;
    
    // Default constructor (no parameters)
    public Student() {
        name = "Unknown";
        age = 0;
        course = "Not Assigned";
    }
    
    // Parameterized constructor
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
        this.course = "General";
    }
    
    // Another parameterized constructor
    public Student(String name, int age, String course) {
        this.name = name;
        this.age = age;
        this.course = course;
    }
    
    public void display() {
        System.out.println(name + ", " + age + ", " + course);
    }
}

// Using constructors
Student s1 = new Student();                      // Default
Student s2 = new Student("John", 20);            // 2 params
Student s3 = new Student("Alice", 22, "CS");     // 3 params
```

#### `this` Keyword
```java
public class Person {
    String name;
    int age;
    
    public Person(String name, int age) {
        this.name = name;            // this.name refers to instance variable
        this.age = age;              // name/age refers to parameter
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    public Person getSelf() {
        return this;                 // Returns current object
    }
    
    public void display() {
        this.printInfo();            // Calls another method of same class
    }
    
    public void printInfo() {
        System.out.println(this.name + " - " + this.age);
    }
}
```

---

### 2. Inheritance

**What is it?**  
Mechanism where one class acquires properties and methods of another class.

```java
// Parent class (Superclass)
public class Animal {
    String name;
    int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void eat() {
        System.out.println(name + " is eating");
    }
    
    public void sleep() {
        System.out.println(name + " is sleeping");
    }
}

// Child class (Subclass) - inherits from Animal
public class Dog extends Animal {
    String breed;
    
    // Constructor
    public Dog(String name, int age, String breed) {
        super(name, age);            // Calls parent constructor
        this.breed = breed;
    }
    
    // Additional method specific to Dog
    public void bark() {
        System.out.println(name + " is barking");
    }
    
    // Can use inherited methods
    public void displayInfo() {
        System.out.println(name + " is a " + breed + ", age " + age);
        eat();                       // Inherited method
        sleep();                     // Inherited method
        bark();                      // Own method
    }
}

// Another child class
public class Cat extends Animal {
    public Cat(String name, int age) {
        super(name, age);
    }
    
    public void meow() {
        System.out.println(name + " says meow");
    }
}

// Using inheritance
public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("Buddy", 3, "Golden Retriever");
        dog.displayInfo();
        
        Cat cat = new Cat("Whiskers", 2);
        cat.eat();                   // Inherited method
        cat.meow();                  // Own method
    }
}
```

#### `super` Keyword

```java
public class Vehicle {
    String type;
    int speed;
    
    public Vehicle(String type, int speed) {
        this.type = type;
        this.speed = speed;
    }
    
    public void display() {
        System.out.println("Type: " + type);
    }
}

public class Bike extends Vehicle {
    String brand;
    
    public Bike(String type, int speed, String brand) {
        super(type, speed);          // Call parent constructor
        this.brand = brand;
    }
    
    public void display() {
        super.display();             // Call parent method
        System.out.println("Brand: " + brand);
        System.out.println("Speed: " + super.speed);  // Access parent variable
    }
}
```

#### Constructor Chaining

```java
public class Parent {
    public Parent() {
        System.out.println("Parent constructor");
    }
}

public class Child extends Parent {
    public Child() {
        super();                     // Implicit call to parent constructor
        System.out.println("Child constructor");
    }
}

// Output when creating Child object:
// Parent constructor
// Child constructor
```

**Types of Inheritance:**
- **Single**: Class B extends Class A
- **Multilevel**: Class C extends B, B extends A
- **Hierarchical**: Multiple classes extend same parent
- **Multiple** (NOT supported in Java with classes, use interfaces)

---

### 3. Polymorphism

**What is it?**  
"Many forms" - Same method/object behaves differently in different contexts.

#### Method Overloading (Compile-time Polymorphism)
**Same method name, different parameters**

```java
public class MathOperations {
    // Method 1
    public int multiply(int a, int b) {
        return a * b;
    }
    
    // Method 2 - different number of parameters
    public int multiply(int a, int b, int c) {
        return a * b * c;
    }
    
    // Method 3 - different parameter types
    public double multiply(double a, double b) {
        return a * b;
    }
}
```

#### Method Overriding (Runtime Polymorphism)
**Child class provides its own implementation of parent method**

```java
public class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound");
    }
    
    public void eat() {
        System.out.println("Animal eats");
    }
}

public class Dog extends Animal {
    @Override                        // Optional but recommended annotation
    public void makeSound() {
        System.out.println("Dog barks: Woof!");
    }
    
    // eat() not overridden, so uses parent version
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Cat meows: Meow!");
    }
}

// Demonstrating polymorphism
public class Main {
    public static void main(String[] args) {
        Animal a1 = new Animal();
        Animal a2 = new Dog();       // Upcasting
        Animal a3 = new Cat();       // Upcasting
        
        a1.makeSound();              // Animal makes a sound
        a2.makeSound();              // Dog barks: Woof!
        a3.makeSound();              // Cat meows: Meow!
        
        // All calls to same method name, but different behavior
    }
}
```

#### Overloading vs Overriding

| Feature | Overloading | Overriding |
|---------|-------------|------------|
| **When** | Compile-time | Runtime |
| **Where** | Same class | Parent-child classes |
| **Parameters** | Must be different | Must be same |
| **Return type** | Can be different | Must be same (or covariant) |
| **Access modifier** | Can be any | Cannot be more restrictive |
| **Purpose** | Multiple versions of method | Change parent behavior |

```java
// Example showing both
public class Shape {
    // Overloading in same class
    public double area(double radius) {
        return Math.PI * radius * radius;
    }
    
    public double area(double length, double width) {
        return length * width;
    }
    
    public void display() {
        System.out.println("Shape");
    }
}

public class Circle extends Shape {
    // Overriding parent method
    @Override
    public void display() {
        System.out.println("Circle");
    }
}
```

---

### 4. Abstraction

**What is it?**  
Hiding implementation details and showing only essential features.

#### Abstract Classes

```java
// Abstract class - cannot be instantiated
public abstract class Animal {
    String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    // Abstract method - no body, must be implemented by child
    public abstract void makeSound();
    
    // Abstract method
    public abstract void move();
    
    // Concrete method - has implementation
    public void sleep() {
        System.out.println(name + " is sleeping");
    }
}

// Concrete class - must implement all abstract methods
public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " barks");
    }
    
    @Override
    public void move() {
        System.out.println(name + " runs on four legs");
    }
}

public class Bird extends Animal {
    public Bird(String name) {
        super(name);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " chirps");
    }
    
    @Override
    public void move() {
        System.out.println(name + " flies");
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        // Animal a = new Animal("Test");  // ERROR: Cannot instantiate abstract class
        
        Animal dog = new Dog("Buddy");
        Animal bird = new Bird("Tweety");
        
        dog.makeSound();                    // Buddy barks
        dog.move();                         // Buddy runs on four legs
        dog.sleep();                        // Buddy is sleeping (inherited concrete method)
        
        bird.makeSound();                   // Tweety chirps
        bird.move();                        // Tweety flies
    }
}
```

#### Interfaces
**100% abstract (before Java 8)**

```java
// Interface - all methods are abstract by default
public interface Drawable {
    void draw();                 // public abstract by default
    void resize();
}

public interface Colorable {
    void setColor(String color);
}

// Class implementing interface must implement all methods
public class Circle implements Drawable, Colorable {
    private String color;
    
    @Override
    public void draw() {
        System.out.println("Drawing circle");
    }
    
    @Override
    public void resize() {
        System.out.println("Resizing circle");
    }
    
    @Override
    public void setColor(String color) {
        this.color = color;
        System.out.println("Circle color: " + color);
    }
}

// Can implement multiple interfaces
public class Rectangle implements Drawable, Colorable {
    private String color;
    
    @Override
    public void draw() {
        System.out.println("Drawing rectangle");
    }
    
    @Override
    public void resize() {
        System.out.println("Resizing rectangle");
    }
    
    @Override
    public void setColor(String color) {
        this.color = color;
    }
}
```

#### Interface Features (Java 8+)

```java
public interface Vehicle {
    // Abstract method
    void start();
    
    // Default method - has implementation
    default void stop() {
        System.out.println("Vehicle stopped");
    }
    
    // Static method
    static void service() {
        System.out.println("Vehicle servicing");
    }
    
    // Constants (public static final by default)
    int MAX_SPEED = 120;
}

public class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car started");
    }
    
    // Can override default method (optional)
    @Override
    public void stop() {
        System.out.println("Car stopped with brakes");
    }
}

// Usage
Car car = new Car();
car.start();                     // Car started
car.stop();                      // Car stopped with brakes
Vehicle.service();               // Vehicle servicing
System.out.println(Vehicle.MAX_SPEED);  // 120
```

#### Abstract Class vs Interface

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| **Multiple inheritance** | No | Yes |
| **Method types** | Abstract + Concrete | Abstract + Default + Static |
| **Variables** | Any type | public static final only |
| **Constructor** | Yes | No |
| **Access modifiers** | Any | public only |
| **When to use** | Common base with shared code | Define contract/capability |

---

### 5. Encapsulation

**What is it?**  
Bundling data and methods together, hiding internal details.

#### Access Modifiers

| Modifier | Same Class | Same Package | Subclass | Other Package |
|----------|-----------|--------------|----------|---------------|
| **private** | ✓ | ✗ | ✗ | ✗ |
| **default** | ✓ | ✓ | ✗ | ✗ |
| **protected** | ✓ | ✓ | ✓ | ✗ |
| **public** | ✓ | ✓ | ✓ | ✓ |

```java
public class Student {
    // Private variables - cannot be accessed directly
    private String name;
    private int age;
    private double gpa;
    
    // Public constructor
    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        setGpa(gpa);             // Using setter for validation
    }
    
    // Getter methods - provide read access
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    public double getGpa() {
        return gpa;
    }
    
    // Setter methods - provide controlled write access
    public void setName(String name) {
        if (name != null && !name.isEmpty()) {
            this.name = name;
        }
    }
    
    public void setAge(int age) {
        if (age > 0 && age < 120) {
            this.age = age;
        }
    }
    
    public void setGpa(double gpa) {
        if (gpa >= 0.0 && gpa <= 4.0) {
            this.gpa = gpa;
        }
    }
    
    // Private helper method
    private boolean isEligibleForScholarship() {
        return gpa >= 3.5;
    }
    
    public void displayInfo() {
        System.out.println(name + ", Age: " + age + ", GPA: " + gpa);
        if (isEligibleForScholarship()) {
            System.out.println("Eligible for scholarship");
        }
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Student s = new Student("Alice", 20, 3.8);
        
        // Direct access not allowed
        // System.out.println(s.name);      // ERROR: name is private
        
        // Must use getters
        System.out.println(s.getName());    // Alice
        
        // Use setters with validation
        s.setGpa(5.0);                      // Invalid, won't be set
        System.out.println(s.getGpa());     // Still 3.8
        
        s.setGpa(3.9);                      // Valid
        System.out.println(s.getGpa());     // 3.9
    }
}
```

#### Benefits of Encapsulation

```java
public class BankAccount {
    private String accountNumber;
    private double balance;
    private String password;
    
    public BankAccount(String accountNumber, String password) {
        this.accountNumber = accountNumber;
        this.password = password;
        this.balance = 0.0;
    }
    
    // Controlled access to deposit
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        } else {
            System.out.println("Invalid amount");
        }
    }
    
    // Controlled access to withdraw
    public boolean withdraw(double amount, String password) {
        if (!this.password.equals(password)) {
            System.out.println("Invalid password");
            return false;
        }
        if (amount > balance) {
            System.out.println("Insufficient balance");
            return false;
        }
        if (amount <= 0) {
            System.out.println("Invalid amount");
            return false;
        }
        balance -= amount;
        System.out.println("Withdrawn: " + amount);
        return true;
    }
    
    // Read-only access to balance
    public double getBalance(String password) {
        if (this.password.equals(password)) {
            return balance;
        }
        System.out.println("Invalid password");
        return -1;
    }
}
```

---

## 📙 LEVEL 3: CORE APIS

### 1. String Handling

#### String Basics

```java
// Creating strings
String s1 = "Hello";                 // String literal
String s2 = new String("Hello");     // Using new keyword
String s3 = "Hello";

// String comparison
System.out.println(s1 == s3);        // true (same reference in pool)
System.out.println(s1 == s2);        // false (different references)
System.out.println(s1.equals(s2));   // true (same content)
```

#### String Pool (String Interning)

```java
// String literals are stored in String Pool
String a = "Java";
String b = "Java";
System.out.println(a == b);          // true (both point to same pool object)

// new String() creates object in heap (not pool)
String c = new String("Java");
System.out.println(a == c);          // false (different memory locations)
System.out.println(a.equals(c));     // true (same content)

// Intern method - moves string to pool
String d = c.intern();
System.out.println(a == d);          // true (both from pool)
```

#### Immutability
**Strings cannot be changed once created**

```java
String str = "Hello";
str.concat(" World");                // Creates new string, doesn't modify original
System.out.println(str);             // Hello (unchanged)

String result = str.concat(" World");
System.out.println(result);          // Hello World (new string)

// Why immutability?
String s1 = "Java";
String s2 = s1;
s1 = s1 + " Programming";            // s1 now points to new object
System.out.println(s1);              // Java Programming
System.out.println(s2);              // Java (unchanged)
```

#### Common String Methods

```java
String str = "Hello World";

// Length
System.out.println(str.length());              // 11

// Character at index
System.out.println(str.charAt(0));             // H
System.out.println(str.charAt(6));             // W

// Substring
System.out.println(str.substring(0, 5));       // Hello
System.out.println(str.substring(6));          // World

// Case conversion
System.out.println(str.toLowerCase());         // hello world
System.out.println(str.toUpperCase());         // HELLO WORLD

// Trim whitespace
String s = "  Java  ";
System.out.println(s.trim());                  // Java

// Replace
System.out.println(str.replace("World", "Java"));  // Hello Java
System.out.println(str.replaceAll("l", "L"));      // HeLLo WorLd

// Split
String csv = "John,25,Developer";
String[] parts = csv.split(",");
for (String part : parts) {
    System.out.println(part);        // John, 25, Developer
}

// Contains
System.out.println(str.contains("World"));     // true
System.out.println(str.contains("Java"));      // false

// StartsWith / EndsWith
System.out.println(str.startsWith("Hello"));   // true
System.out.println(str.endsWith("World"));     // true

// IndexOf
System.out.println(str.indexOf("o"));          // 4 (first occurrence)
System.out.println(str.lastIndexOf("o"));      // 7 (last occurrence)
System.out.println(str.indexOf("World"));      // 6

// Equals (case-sensitive)
System.out.println(str.equals("hello world")); // false
System.out.println(str.equalsIgnoreCase("hello world")); // true

// IsEmpty / IsBlank
String empty = "";
String blank = "   ";
System.out.println(empty.isEmpty());           // true
System.out.println(blank.isEmpty());           // false
System.out.println(blank.isBlank());           // true (Java 11+)
```

#### StringBuilder (Mutable)
**When you need to modify strings frequently**

```java
// Problem with String concatenation
String result = "";
for (int i = 0; i < 1000; i++) {
    result += i;                     // Creates 1000 new String objects!
}

// Solution: StringBuilder
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i);                    // Modifies same object
}
String finalResult = sb.toString();

// StringBuilder methods
StringBuilder builder = new StringBuilder("Hello");

builder.append(" World");            // Hello World
builder.insert(5, ",");              // Hello, World
builder.delete(5, 6);                // Hello World
builder.reverse();                   // dlroW olleH
builder.replace(0, 5, "Java");       // Java olleH

System.out.println(builder.toString());
System.out.println(builder.length());
System.out.println(builder.capacity());

// StringBuilder vs StringBuffer
// StringBuilder: Fast, not thread-safe
// StringBuffer: Slower, thread-safe (synchronized)
```

#### String Formatting

```java
// Using String.format()
String name = "Alice";
int age = 25;
double salary = 50000.50;

String formatted = String.format("Name: %s, Age: %d, Salary: %.2f", 
                                  name, age, salary);
System.out.println(formatted);       // Name: Alice, Age: 25, Salary: 50000.50

// Common format specifiers
// %s - String
// %d - Integer
// %f - Float/Double
// %c - Character
// %b - Boolean

// Using printf()
System.out.printf("Name: %s, Age: %d%n", name, age);

// Number formatting
System.out.printf("%d%n", 100);      // 100
System.out.printf("%5d%n", 100);     // "  100" (width 5)
System.out.printf("%05d%n", 100);    // "00100" (zero-padded)
System.out.printf("%.2f%n", 3.14159);// 3.14 (2 decimal places)
```

---

### 2. Exception Handling

**What is an Exception?**  
An event that disrupts normal program flow.

#### Exception Hierarchy
```
Throwable
├── Error (Serious issues - OutOfMemoryError, StackOverflowError)
└── Exception
    ├── RuntimeException (Unchecked)
    │   ├── NullPointerException
    │   ├── ArrayIndexOutOfBoundsException
    │   ├── ArithmeticException
    │   └── ...
    └── Checked Exceptions
        ├── IOException
        ├── SQLException
        ├── ClassNotFoundException
        └── ...
```

#### try-catch-finally

```java
public class ExceptionExample {
    public static void main(String[] args) {
        try {
            // Code that might throw exception
            int result = 10 / 0;         // ArithmeticException
            System.out.println(result);
        } catch (ArithmeticException e) {
            // Handle specific exception
            System.out.println("Cannot divide by zero");
            System.out.println("Error: " + e.getMessage());
        } finally {
            // Always executes (even if exception occurs)
            System.out.println("Finally block executed");
        }
        
        System.out.println("Program continues...");
    }
}
```

#### Multiple catch Blocks

```java
public void processArray(String[] args) {
    try {
        int num = Integer.parseInt(args[0]);     // NumberFormatException
        int result = 100 / num;                  // ArithmeticException
        int[] arr = {1, 2, 3};
        System.out.println(arr[5]);              // ArrayIndexOutOfBoundsException
        
    } catch (NumberFormatException e) {
        System.out.println("Invalid number format");
    } catch (ArithmeticException e) {
        System.out.println("Cannot divide by zero");
    } catch (ArrayIndexOutOfBoundsException e) {
        System.out.println("Array index out of bounds");
    } catch (Exception e) {                       // Generic catch (must be last)
        System.out.println("Some error occurred: " + e);
    } finally {
        System.out.println("Cleanup code");
    }
}

// Multi-catch (Java 7+)
try {
    // code
} catch (IOException | SQLException e) {
    System.out.println("IO or SQL error: " + e);
}
```

#### throw and throws

```java
// throw - manually throw exception
public void checkAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("Age must be 18 or above");
    }
    System.out.println("Age is valid");
}

// throws - declare that method might throw exception
public void readFile(String filename) throws IOException {
    FileReader file = new FileReader(filename);  // May throw IOException
    // ... read file
}

// Caller must handle or declare
public void processFile() {
    try {
        readFile("data.txt");
    } catch (IOException e) {
        System.out.println("File error: " + e.getMessage());
    }
}

// Or propagate
public void processFile2() throws IOException {
    readFile("data.txt");            // Passing exception to caller
}
```

#### Custom Exceptions

```java
// Custom checked exception
public class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

// Custom unchecked exception
public class InsufficientBalanceException extends RuntimeException {
    private double balance;
    private double withdrawAmount;
    
    public InsufficientBalanceException(String message, double balance, double withdrawAmount) {
        super(message);
        this.balance = balance;
        this.withdrawAmount = withdrawAmount;
    }
    
    public double getBalance() {
        return balance;
    }
    
    public double getWithdrawAmount() {
        return withdrawAmount;
    }
}

// Using custom exceptions
public class BankAccount {
    private double balance;
    
    public void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException(
                "Cannot withdraw " + amount + ", balance is " + balance,
                balance,
                amount
            );
        }
        balance -= amount;
    }
}

public class AgeValidator {
    public void validateAge(int age) throws InvalidAgeException {
        if (age < 0 || age > 120) {
            throw new InvalidAgeException("Invalid age: " + age);
        }
        System.out.println("Age is valid");
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();
        try {
            account.withdraw(1000);
        } catch (InsufficientBalanceException e) {
            System.out.println(e.getMessage());
            System.out.println("Balance: " + e.getBalance());
        }
        
        AgeValidator validator = new AgeValidator();
        try {
            validator.validateAge(150);
        } catch (InvalidAgeException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

#### try-with-resources (Java 7+)
**Automatically closes resources**

```java
// Old way
BufferedReader reader = null;
try {
    reader = new BufferedReader(new FileReader("file.txt"));
    String line = reader.readLine();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try {
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// New way - try-with-resources
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    String line = reader.readLine();
} catch (IOException e) {
    e.printStackTrace();
}
// reader.close() called automatically

// Multiple resources
try (FileReader fr = new FileReader("input.txt");
     FileWriter fw = new FileWriter("output.txt")) {
    // Use resources
} catch (IOException e) {
    e.printStackTrace();
}
```

#### Checked vs Unchecked Exceptions

| Checked Exceptions | Unchecked Exceptions |
|-------------------|---------------------|
| Compile-time checking | Runtime checking |
| Must handle or declare | Optional to handle |
| Extend Exception | Extend RuntimeException |
| IOException, SQLException | NullPointerException, ArrayIndexOutOfBoundsException |
| Use for recoverable conditions | Use for programming errors |

---

### 3. Generics

**What are Generics?**  
Allow you to write code that works with different types while maintaining type safety.

#### Basic Generics

```java
// Without generics - not type safe
class Box {
    private Object value;
    
    public void set(Object value) {
        this.value = value;
    }
    
    public Object get() {
        return value;
    }
}

Box box = new Box();
box.set("Hello");
String str = (String) box.get();     // Manual casting needed
box.set(123);
String str2 = (String) box.get();    // Runtime error!

// With generics - type safe
class GenericBox<T> {
    private T value;
    
    public void set(T value) {
        this.value = value;
    }
    
    public T get() {
        return value;
    }
}

GenericBox<String> stringBox = new GenericBox<>();
stringBox.set("Hello");
String str = stringBox.get();        // No casting needed!
// stringBox.set(123);               // Compile-time error!

GenericBox<Integer> intBox = new GenericBox<>();
intBox.set(123);
int num = intBox.get();
```

#### Generic Methods

```java
public class GenericMethods {
    // Generic method
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }
    
    // Generic method with return type
    public static <T> T getFirst(T[] array) {
        if (array.length > 0) {
            return array[0];
        }
        return null;
    }
    
    // Multiple type parameters
    public static <K, V> void printKeyValue(K key, V value) {
        System.out.println(key + " : " + value);
    }
    
    public static void main(String[] args) {
        Integer[] intArray = {1, 2, 3, 4, 5};
        String[] strArray = {"A", "B", "C"};
        
        printArray(intArray);            // 1 2 3 4 5
        printArray(strArray);            // A B C
        
        Integer first = getFirst(intArray);
        System.out.println(first);       // 1
        
        printKeyValue("Name", "John");   // Name : John
        printKeyValue(1, "First");       // 1 : First
    }
}
```

#### Bounded Type Parameters

```java
// Upper bound - T must be Number or its subclass
public class Calculator<T extends Number> {
    private T value;
    
    public Calculator(T value) {
        this.value = value;
    }
    
    public double square() {
        return value.doubleValue() * value.doubleValue();
    }
}

Calculator<Integer> intCalc = new Calculator<>(5);
System.out.println(intCalc.square());        // 25.0

Calculator<Double> doubleCalc = new Calculator<>(3.5);
System.out.println(doubleCalc.square());     // 12.25

// Calculator<String> strCalc = new Calculator<>("Hi");  // Error!

// Multiple bounds
public class MyClass<T extends Number & Comparable<T>> {
    // T must be Number AND implement Comparable
}
```

#### Wildcards

```java
import java.util.*;

public class WildcardExample {
    // Unknown type - can read but not write
    public static void printList(List<?> list) {
        for (Object obj : list) {
            System.out.println(obj);
        }
        // list.add("element");          // Error! Cannot add
    }
    
    // Upper bounded wildcard - read as Number
    public static double sumList(List<? extends Number> list) {
        double sum = 0;
        for (Number num : list) {
            sum += num.doubleValue();
        }
        return sum;
    }
    
    // Lower bounded wildcard - write integers
    public static void addNumbers(List<? super Integer> list) {
        list.add(1);
        list.add(2);
        list.add(3);
        // Integer num = list.get(0);    // Error! Don't know exact type
    }
    
    public static void main(String[] args) {
        List<Integer> intList = Arrays.asList(1, 2, 3);
        List<String> strList = Arrays.asList("A", "B", "C");
        
        printList(intList);              // Works
        printList(strList);              // Works
        
        List<Integer> integers = Arrays.asList(1, 2, 3, 4, 5);
        List<Double> doubles = Arrays.asList(1.1, 2.2, 3.3);
        
        System.out.println(sumList(integers));  // 15.0
        System.out.println(sumList(doubles));   // 6.6
        
        List<Number> numbers = new ArrayList<>();
        List<Object> objects = new ArrayList<>();
        
        addNumbers(numbers);             // Works
        addNumbers(objects);             // Works
    }
}
```

#### PECS (Producer Extends, Consumer Super)

```java
// Producer (you read from it) - use extends
public void processProducer(List<? extends Number> list) {
    for (Number num : list) {          // Reading - OK
        System.out.println(num);
    }
    // list.add(5);                    // Writing - NOT OK
}

// Consumer (you write to it) - use super
public void processConsumer(List<? super Integer> list) {
    list.add(5);                       // Writing - OK
    list.add(10);
    // Integer num = list.get(0);      // Reading as Integer - NOT OK
    Object obj = list.get(0);          // Reading as Object - OK
}

// Example: Collections.copy()
public static <T> void copy(List<? super T> dest,    // Consumer
                            List<? extends T> src) {  // Producer
    for (T item : src) {
        dest.add(item);
    }
}
```

#### Type Erasure
**Generics are compile-time only**

```java
// Your code
List<String> list1 = new ArrayList<>();
List<Integer> list2 = new ArrayList<>();

// After type erasure (at runtime)
List list1 = new ArrayList();
List list2 = new ArrayList();

// Implications
System.out.println(list1.getClass() == list2.getClass());  // true

// Cannot do this:
// if (list instanceof List<String>) { }     // Error!
// T obj = new T();                          // Error!
// T[] array = new T[10];                    // Error!
```

---

## 📕 LEVEL 4: COLLECTIONS FRAMEWORK

**What is Collections Framework?**  
A set of classes and interfaces that implement commonly reusable data structures.

```
Collection (interface)
├── List (interface) - ordered, allows duplicates
│   ├── ArrayList
│   ├── LinkedList
│   ├── Vector
│   └── Stack
├── Set (interface) - no duplicates
│   ├── HashSet
│   ├── LinkedHashSet
│   └── TreeSet
└── Queue (interface) - FIFO order
    ├── PriorityQueue
    ├── Deque (interface)
    └── LinkedList

Map (interface) - key-value pairs
├── HashMap
├── LinkedHashMap
├── TreeMap
├── Hashtable
└── ConcurrentHashMap
```

### 1. List Interface

#### ArrayList
**Resizable array, fast random access**

##### 🔧 Internal Structure
- **Underlying Data Structure**: Dynamic Array (`Object[]` array)
- **Default Capacity**: 10 elements
- **Growth Factor**: 1.5x (grows by 50% when full)

##### 🎯 How It Works

**1. Initialization**
- When created, an empty array or array with initial capacity is allocated
- The array is of type `Object[]` to support any type
- Maintains a `size` variable tracking actual elements (different from capacity)

**2. Add Operation (at end)**

Algorithm:
1. Check if `size` equals current capacity
2. If full, create new array with capacity = `oldCapacity + (oldCapacity >> 1)` (1.5x)
3. Copy all elements from old array to new array using `System.arraycopy()`
4. Add new element at `index = size`
5. Increment `size`

**Time Complexity:**
- Average Case: O(1) - amortized constant time
- Worst Case: O(n) - when resizing needed

**3. Add Operation (at specific index)**

Algorithm:
1. Check if resize needed
2. Shift all elements from index to end one position right
3. Insert element at specified index
4. Increment size

**Time Complexity:** O(n) - due to shifting

**4. Get Operation**

Algorithm:
1. Check if index is within bounds (0 to size-1)
2. Return `array[index]`

**Time Complexity:** O(1) - direct array access

**5. Remove Operation**

Algorithm:
1. Get element at index
2. Calculate number of elements to shift = `(size - index - 1)`
3. Shift all elements after index one position left
4. Set last element to null (for garbage collection)
5. Decrement size

**Time Complexity:** O(n) - due to shifting

**Real-life analogy:**
ArrayList is like a parking lot with numbered spaces. Finding a car by space number is instant (O(1)), but if someone leaves from the middle, all cars behind must move forward.

##### 📊 Key Points
- ✅ Fast random access (index-based)
- ✅ Good for read-heavy operations
- ❌ Slow insertion/deletion in middle
- ❌ Not thread-safe
- ✅ Allows null values and duplicates
- ✅ Maintains insertion order

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **O(1) random access** | O(n) insertion/deletion in middle |
| **Memory efficient** | Wasted capacity when not full |
| **Cache-friendly (contiguous memory)** | Resizing causes temporary memory spike |
| **Simple implementation** | Not thread-safe (need external sync) |
| **Fast iteration** | Slow when frequent insertions/deletions |

**When to choose ArrayList:**
- ✅ Need fast random access by index
- ✅ Read-heavy operations (get, iterate)
- ✅ Mostly append operations
- ❌ Avoid if frequent insertions/deletions in middle
- ❌ Avoid if need thread-safety without external sync

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListExample {
    public static void main(String[] args) {
        // Creating ArrayList
        List<String> fruits = new ArrayList<>();
        
        // Adding elements
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        fruits.add("Apple");             // Duplicates allowed
        
        System.out.println(fruits);      // [Apple, Banana, Orange, Apple]
        
        // Add at specific index
        fruits.add(1, "Mango");
        System.out.println(fruits);      // [Apple, Mango, Banana, Orange, Apple]
        
        // Get element
        String fruit = fruits.get(0);
        System.out.println(fruit);       // Apple
        
        // Update element
        fruits.set(0, "Grapes");
        System.out.println(fruits);      // [Grapes, Mango, Banana, Orange, Apple]
        
        // Remove element
        fruits.remove("Mango");          // Remove by value
        fruits.remove(2);                // Remove by index
        System.out.println(fruits);      // [Grapes, Banana, Apple]
        
        // Size
        System.out.println(fruits.size());  // 3
        
        // Contains
        System.out.println(fruits.contains("Banana"));  // true
        
        // IndexOf
        System.out.println(fruits.indexOf("Apple"));    // 2
        
        // Iterating
        for (String f : fruits) {
            System.out.println(f);
        }
        
        // Clear all elements
        fruits.clear();
        System.out.println(fruits.isEmpty());  // true
    }
}
```

#### LinkedList
**Doubly-linked list, fast insertion/deletion**

##### 🔧 Internal Structure
- **Underlying Data Structure**: Doubly Linked List
- **Node Structure**: Each node contains:
  - `data` (element)
  - `next` (reference to next node)
  - `prev` (reference to previous node)
- **Pointers**: Maintains `head` (first) and `tail` (last) references
- Also maintains `size` variable

##### 🎯 How It Works

**1. Node Structure**
```java
private static class Node<E> {
    E item;
    Node<E> next;
    Node<E> prev;
}
```

**2. Add Operation (at end)**

Algorithm:
1. Create new node with given element
2. Set new node's `prev = current tail`
3. Set new node's `next = null`
4. If list is empty: Set `head = new node`
5. Else: Set current tail's `next = new node`
6. Set `tail = new node`
7. Increment size

**Time Complexity:** O(1)

**3. Add Operation (at specific index)**

Algorithm:
1. If `index = 0`: Add at beginning (O(1))
2. If `index = size`: Add at end (O(1))
3. Else:
   - Traverse to index (from head or tail, whichever closer)
   - Get node at index
   - Create new node
   - Adjust pointers:
     - `newNode.next = current node`
     - `newNode.prev = current node's prev`
     - `current node's prev.next = newNode`
     - `current node's prev = newNode`
4. Increment size

**Time Complexity:** O(n) - traversal needed

**4. Get Operation**

Algorithm:
1. If `index < size/2`: Start from head, traverse forward
2. Else: Start from tail, traverse backward
3. Return node's data

**Time Complexity:** O(n) - always needs traversal

**5. Remove Operation**

Algorithm:
1. Traverse list to find element
2. Once found:
   - If node is head: `head = node.next`
   - If node is tail: `tail = node.prev`
   - Adjust surrounding pointers:
     - `node.prev.next = node.next`
     - `node.next.prev = node.prev`
3. Set node references to null
4. Decrement size

**Time Complexity:** O(n)

**Real-life analogy:**
LinkedList is like a train - each car (node) is connected to the next and previous. Adding/removing cars at the ends is easy, but finding a specific car requires walking through the train.

##### 📊 Key Points
- ✅ Fast insertion/deletion at both ends (O(1))
- ✅ Implements both List and Deque interfaces
- ❌ Slow random access (no indexing)
- ❌ Uses more memory (extra pointers per element)
- ❌ Not thread-safe
- ✅ Better for frequent insertions/deletions

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **O(1) insertion/deletion at ends** | O(n) random access by index |
| **No wasted capacity** | More memory per element (2 pointers) |
| **Dynamic size (no resizing)** | Poor cache locality (scattered memory) |
| **Implements List + Deque** | Slower iteration than ArrayList |
| **Good for queue/stack operations** | Not suitable for random access patterns |

**When to choose LinkedList:**
- ✅ Frequent insertions/deletions at beginning/end
- ✅ Need deque operations (addFirst, addLast)
- ✅ Implementing queue or stack
- ❌ Avoid if need random access by index
- ❌ Avoid if memory is constrained

```java
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        LinkedList<Integer> numbers = new LinkedList<>();
        
        // Add elements
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);
        
        // Add at beginning/end
        numbers.addFirst(5);
        numbers.addLast(40);
        System.out.println(numbers);     // [5, 10, 20, 30, 40]
        
        // Get first/last
        System.out.println(numbers.getFirst());    // 5
        System.out.println(numbers.getLast());     // 40
        
        // Remove first/last
        numbers.removeFirst();
        numbers.removeLast();
        System.out.println(numbers);     // [10, 20, 30]
        
        // Use as Stack (LIFO)
        numbers.push(50);                // Add to front
        System.out.println(numbers.pop());  // Remove from front: 50
        
        // Use as Queue (FIFO)
        numbers.offer(60);               // Add to end
        System.out.println(numbers.poll());  // Remove from front: 10
    }
}
```

#### Vector and Stack
**Thread-safe alternatives (synchronized)**

```java
import java.util.Vector;
import java.util.Stack;

// Vector - similar to ArrayList but synchronized
Vector<String> vector = new Vector<>();
vector.add("A");
vector.add("B");

// Stack - LIFO (Last In First Out)
Stack<Integer> stack = new Stack<>();
stack.push(10);                      // Add to top
stack.push(20);
stack.push(30);
System.out.println(stack.peek());    // 30 (see top without removing)
System.out.println(stack.pop());     // 30 (remove and return top)
System.out.println(stack.pop());     // 20
System.out.println(stack.isEmpty()); // false
```

#### ArrayList vs LinkedList

| Feature | ArrayList | LinkedList |
|---------|-----------|------------|
| **Internal structure** | Dynamic array | Doubly linked list |
| **Access by index** | Fast O(1) | Slow O(n) |
| **Add/Remove at end** | Fast O(1) | Fast O(1) |
| **Add/Remove at beginning** | Slow O(n) | Fast O(1) |
| **Add/Remove in middle** | Slow O(n) | Fast O(1) if position known |
| **Memory** | Less | More (extra pointers) |
| **Use case** | Random access, read-heavy | Frequent insertions/deletions |

---

### 2. Set Interface

#### HashSet
**Unordered set, no duplicates, fast operations**

##### 🔧 Internal Structure
- **Underlying**: HashMap
- **Storage**: Elements stored as HashMap keys
- **Values**: Dummy `PRESENT` object for all elements

##### 🎯 How It Works

**Operations:**
All operations delegate to internal HashMap:
- `add(element)`: `HashMap.put(element, PRESENT)` - O(1)
- `contains(element)`: `HashMap.containsKey(element)` - O(1)
- `remove(element)`: `HashMap.remove(element)` - O(1)

**Real-life analogy:**
Like a guest list at a party - you can quickly check if someone is on the list, no duplicates allowed.

##### 📊 Key Points
- ✅ No duplicates
- ✅ Allows one null
- ❌ No ordering
- ✅ Fast operations O(1)
- ❌ Not thread-safe

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **O(1) add/contains/remove** | No ordering guarantees |
| **No duplicates automatically** | Requires good hashCode() implementation |
| **Memory efficient** | Wasted capacity in underlying HashMap |
| **Fast membership testing** | Cannot retrieve elements by index |
| **Simple API** | Not thread-safe |

**When to choose HashSet:**
- ✅ Need fast membership testing (contains)
- ✅ Need to eliminate duplicates
- ✅ Don't care about order
- ❌ Avoid if need ordering
- ❌ Avoid if need indexed access

```java
import java.util.HashSet;
import java.util.Set;

public class HashSetExample {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        
        set.add("Apple");
        set.add("Banana");
        set.add("Apple");        // Duplicate - won't be added
        
        System.out.println(set);  // [Apple, Banana] - no duplicates
        System.out.println(set.contains("Apple"));  // true
    }
}
```

---

#### LinkedHashSet
**Ordered set, maintains insertion order**

##### 🔧 Internal Structure
- **Extends**: HashSet
- **Underlying**: LinkedHashMap
- **Maintains**: Insertion order using doubly linked list

##### 🎯 How It Works
- Creates LinkedHashMap instead of HashMap
- All operations O(1) + linked list maintenance
- Iteration follows insertion order

##### 📊 Key Points
- ✅ Maintains insertion order
- ✅ Fast operations O(1)
- ❌ Slightly slower than HashSet
- ❌ Uses more memory (extra pointers)

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **Predictable iteration order** | ~20% slower than HashSet |
| **O(1) operations** | More memory (doubly linked list) |
| **Insertion order preserved** | Slightly more complex implementation |
| **No duplicates** | Cannot sort elements |

**When to choose LinkedHashSet:**
- ✅ Need insertion order + fast operations
- ✅ Building ordered unique collections
- ✅ Cache with predictable iteration
- ❌ Avoid if memory is critical
- ❌ Avoid if order doesn't matter (use HashSet)

```java
Set<String> linkedSet = new LinkedHashSet<>();
linkedSet.add("C");
linkedSet.add("A");
linkedSet.add("B");
System.out.println(linkedSet);  // [C, A, B] - insertion order maintained
```

---

#### TreeSet
**Sorted set, elements in natural order**

##### 🔧 Internal Structure
- **Underlying**: TreeMap (Red-Black Tree)
- **Storage**: Elements as TreeMap keys
- **Ordering**: Natural order or custom Comparator

##### 🎯 How It Works
- All operations delegate to TreeMap
- `add()`: O(log n)
- `contains()`: O(log n)
- `remove()`: O(log n)
- Sorted iteration

##### 📊 Key Points
- ✅ Sorted order
- ✅ NavigableSet operations (ceiling, floor, etc.)
- ❌ No null elements
- ❌ Slower than HashSet
- ❌ Elements must be comparable

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **Sorted order automatically** | O(log n) operations (vs O(1) in HashSet) |
| **Range queries (subSet, headSet)** | Elements must implement Comparable |
| **NavigableSet operations** | More memory (tree structure) |
| **Predictable performance** | Cannot store null |
| **No duplicates** | Slower than HashSet |

**When to choose TreeSet:**
- ✅ Need sorted unique elements
- ✅ Need range queries (elements between X and Y)
- ✅ Need ceiling/floor operations
- ❌ Avoid if performance is critical (use HashSet)
- ❌ Avoid if elements not comparable

```java
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(30);
treeSet.add(10);
treeSet.add(20);
System.out.println(treeSet);  // [10, 20, 30] - sorted
```

---

### 3. Map Interface

#### HashMap
**Key-value pairs, fast lookup, no ordering**

##### 🔧 Internal Structure
- **Underlying Data Structure**: Array of Nodes (buckets) + Linked Lists/Red-Black Trees
- **Default Capacity**: 16 buckets
- **Load Factor**: 0.75 (resizes when 75% full)
- **Node Structure**: Each node contains:
  - `hash` (cached hash code)
  - `key`
  - `value`
  - `next` (reference to next node in chain)

##### 🎯 How It Works

**1. Hashing Mechanism**

Hash Calculation:
1. Get key's `hashCode()`
2. Apply additional hash function to reduce collisions (XOR higher bits with lower bits)
3. Calculate bucket index = `hash & (capacity - 1)`
   - Equivalent to `hash % capacity` but faster
   - Works because capacity is always power of 2

**2. Put Operation**

Algorithm:
1. Calculate hash of key
2. Determine bucket index using `hash & (n-1)`
3. Check if bucket is empty:
   - Empty: Create new node, place directly in bucket
4. If bucket occupied (collision):
   - **Case A** - Key exists: Traverse chain/tree, replace old value
   - **Case B** - Key doesn't exist:
     - If chain length < 8: Add to linked list
     - If chain length ≥ 8 AND capacity ≥ 64: Convert to Red-Black Tree (treeification)
5. Increment size
6. Check if `size > threshold` (capacity × load factor):
   - If yes, resize (double capacity)

**Time Complexity:**
- Average: O(1)
- Worst Case (before Java 8): O(n) - long chain
- Worst Case (Java 8+): O(log n) - tree structure

**3. Resize Operation**

Algorithm:
1. Create new array with double capacity
2. For each bucket in old array:
   - Rehash all nodes
   - Recalculate bucket positions in new array
3. Replace old array with new array

**Time Complexity:** O(n) - must rehash all elements

**4. Get Operation**

Algorithm:
1. Calculate hash of key
2. Find bucket index
3. Check bucket:
   - If empty: Return null
   - If single node: Check if key matches, return value
   - If linked list: Traverse and find matching key
   - If tree: Search tree (O(log n))
4. Return value if found, else null

**Time Complexity:** O(1) average, O(log n) worst case

**5. Collision Handling Evolution**

**Before Java 8:**
- Only linked lists for collisions
- Worst case O(n) for chains

**Java 8+:**
- Linked list → Red-Black Tree conversion
- **Treeification Threshold**: 8 nodes
- **Untreeification Threshold**: 6 nodes
- **Minimum Capacity for Trees**: 64 buckets
- Dramatically improves worst-case performance

**Real-life analogy:**
HashMap is like a library with sections (buckets). Books are organized by category (hash). If too many books in one section, create a better organization system (tree).

##### 📊 Key Points
- ✅ Fast operations O(1) average
- ❌ Not thread-safe
- ✅ Allows one null key and multiple null values
- ❌ No ordering guarantees
- ✅ Capacity always power of 2
- ⚖️ Load factor affects space-time tradeoff

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **O(1) average operations** | O(n) worst case if poor hash function |
| **Flexible key-value storage** | No ordering (unpredictable iteration) |
| **Allows null key/values** | Requires good hashCode() + equals() |
| **Dynamic resizing** | Resizing is expensive O(n) |
| **Memory efficient (75% load)** | Wasted capacity (25% empty buckets) |
| **Fast for most use cases** | Not thread-safe |

**When to choose HashMap:**
- ✅ Need fast key-value lookups
- ✅ Don't care about order
- ✅ Single-threaded or external synchronization
- ❌ Avoid if need ordering (use LinkedHashMap)
- ❌ Avoid if need sorting (use TreeMap)
- ❌ Avoid if concurrent access (use ConcurrentHashMap)

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> ages = new HashMap<>();
        
        ages.put("Alice", 25);
        ages.put("Bob", 30);
        ages.put("Charlie", 28);
        
        System.out.println(ages.get("Bob"));     // 30
        System.out.println(ages.containsKey("Alice"));  // true
        
        // Iterate
        for (Map.Entry<String, Integer> entry : ages.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

---

#### LinkedHashMap
**Ordered map, maintains insertion or access order**

##### 🔧 Internal Structure
- **Extends**: HashMap (inherits bucket array)
- **Additional Structure**: Doubly linked list connecting all entries
- **Maintains**: Insertion order (default) or access order
- **Node Structure**: HashMap.Node + `before`/`after` pointers

##### 🎯 How It Works

**1. Entry Structure**
Each entry extends HashMap's node and adds:
- `before`: Reference to previous entry in iteration order
- `after`: Reference to next entry in iteration order

Also maintains:
- `head`: First entry in iteration order
- `tail`: Last entry in iteration order

**2. Put Operation**

Algorithm:
1. Perform standard HashMap put operation
2. After insertion:
   - Link new entry to tail of linked list
   - Set previous tail's `after = new entry`
   - Set new entry's `before = previous tail`
   - Update `tail = new entry`
3. If access-order mode enabled: Move accessed entries to end

**Time Complexity:** O(1) - same as HashMap

**3. Access Order Mode (LRU Cache)**

When enabled:
- On `get()`: Move accessed entry to tail
- On `put()` (existing key): Move to tail
- Override `removeEldestEntry()` to implement LRU

```java
// LRU Cache implementation
Map<String, Integer> lruCache = new LinkedHashMap<>(16, 0.75f, true) {
    protected boolean removeEldestEntry(Map.Entry eldest) {
        return size() > 100;  // Max 100 entries
    }
};
```

**Real-life analogy:**
Like a playlist - songs play in order you added them (insertion order), or most recently played songs come first (access order).

##### 📊 Key Points
- ✅ Predictable iteration order
- ✅ Perfect for LRU cache implementation
- ❌ Slightly slower than HashMap
- ❌ Uses more memory (extra pointers)
- ❌ Still not thread-safe

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **Insertion order maintained** | ~10-20% slower than HashMap |
| **Access order mode (LRU)** | More memory (doubly linked list) |
| **O(1) operations** | Additional pointer maintenance overhead |
| **Predictable iteration** | Still not thread-safe |
| **Easy LRU cache** | Slightly more complex than HashMap |

**When to choose LinkedHashMap:**
- ✅ Need insertion order preserved
- ✅ Implementing LRU cache
- ✅ Need predictable iteration order
- ❌ Avoid if memory is critical (use HashMap)
- ❌ Avoid if order doesn't matter (use HashMap)
- ❌ Avoid if need concurrent access (use ConcurrentHashMap)

---

#### TreeMap
**Sorted map, Red-Black Tree implementation**

##### 🔧 Internal Structure
- **Underlying Data Structure**: Red-Black Tree (self-balancing BST)
- **Node Structure**: Each node contains:
  - `key`, `value`
  - `left` child reference
  - `right` child reference
  - `parent` reference
  - `color` (RED or BLACK)

##### 🎯 How It Works

**1. Red-Black Tree Properties**
1. Every node is either RED or BLACK
2. Root is always BLACK
3. All leaves (null nodes) are BLACK
4. RED node cannot have RED children
5. Every path from root to leaf has same number of BLACK nodes

**Why Red-Black Trees?**
- Guarantees O(log n) operations
- Faster than AVL trees for insertions/deletions
- Maximum height = 2 × log(n+1)

**2. Put Operation**

Algorithm:
1. **BST Insertion**:
   - Start at root
   - Compare key (using Comparator or Comparable)
   - If key < current: Go left
   - If key > current: Go right
   - If key == current: Replace value
   - Insert new node as RED

2. **Fix Violations (Rebalancing)**:
   - Check if parent is RED (violation)
   - Determine case based on uncle's color:
     - **Case 1** - Uncle is RED: Recolor
     - **Case 2** - Uncle is BLACK (Triangle): Rotate to Case 3
     - **Case 3** - Uncle is BLACK (Line): Rotate + recolor

3. Ensure root is BLACK

**Time Complexity:** O(log n)

**3. Get Operation**

Algorithm:
1. Start at root
2. Compare search key with current node
3. If equal: Return value
4. If less: Go to left child
5. If greater: Go to right child
6. Repeat until found or reach null

**Time Complexity:** O(log n)

**Real-life analogy:**
TreeMap is like a sorted filing cabinet where files are always in alphabetical order. Finding a file takes log(n) time (binary search), but everything stays organized.

##### 📊 Key Points
- ✅ Sorted order (natural or custom comparator)
- ✅ NavigableMap operations (ceiling, floor, subMap)
- ❌ No null keys allowed
- ❌ Slower than HashMap
- ✅ Predictable O(log n) performance

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **Always sorted** | O(log n) operations (vs O(1) in HashMap) |
| **Range queries (subMap)** | More memory (tree structure + colors) |
| **NavigableMap operations** | Keys must be comparable |
| **Predictable performance** | Slower than HashMap for basic operations |
| **No resize overhead** | Cannot store null keys |

**When to choose TreeMap:**
- ✅ Need sorted keys
- ✅ Need range queries (keys between X and Y)
- ✅ Need ceiling/floor/higher/lower operations
- ✅ Need consistent O(log n) performance
- ❌ Avoid if speed is critical (use HashMap)
- ❌ Avoid if keys not comparable
- ❌ Avoid if don't need sorting

```java
import java.util.TreeMap;
import java.util.Map;

public class TreeMapExample {
    public static void main(String[] args) {
        Map<String, Integer> treeMap = new TreeMap<>();
        
        treeMap.put("Charlie", 28);
        treeMap.put("Alice", 25);
        treeMap.put("Bob", 30);
        
        System.out.println(treeMap);  // {Alice=25, Bob=30, Charlie=28} - sorted by key
    }
}
```

---

### 4. Queue Interface

#### PriorityQueue
**Heap-based priority queue, min-heap by default**

##### 🔧 Internal Structure
- **Underlying**: Binary Heap (Min-Heap)
- **Array Representation**: Complete binary tree stored in array
- **Default Capacity**: 11

##### 🎯 How It Works

**1. Binary Heap Properties**
- Complete binary tree in array
- Parent at `(i-1)/2`
- Left child at `2i+1`
- Right child at `2i+2`

**2. Offer Operation (Add)**

Algorithm:
1. Add element at end of array
2. **Heapify Up**:
   - Compare with parent
   - Swap if smaller (for min-heap)
   - Continue until heap property satisfied

**Time Complexity:** O(log n)

**3. Poll Operation (Remove min)**

Algorithm:
1. Store root (minimum element)
2. Replace root with last element
3. **Heapify Down**:
   - Compare with smaller child
   - Swap if larger
   - Continue until heap property satisfied

**Time Complexity:** O(log n)

**4. Peek Operation**
- Return root element without removal
- **Time Complexity:** O(1)

**Real-life analogy:**
PriorityQueue is like an emergency room - patients are treated based on severity (priority), not arrival order.

##### 📊 Key Points
- ✅ Efficient min/max extraction
- ❌ Not sorted, heap-ordered
- ❌ No null elements
- ❌ Not thread-safe
- ✅ Custom comparator supported

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **O(log n) insertion/removal** | O(n) for arbitrary element removal |
| **O(1) peek at min/max** | Not fully sorted (only heap property) |
| **Efficient priority handling** | Cannot access by index |
| **Dynamic sizing** | No random access |
| **Custom ordering** | Elements must be comparable |

**When to choose PriorityQueue:**
- ✅ Need to process elements by priority
- ✅ Implementing algorithms (Dijkstra, Huffman)
- ✅ Task scheduling by priority
- ❌ Avoid if need full sorting (use TreeSet)
- ❌ Avoid if need random access
- ❌ Avoid if concurrent access needed

```java
import java.util.PriorityQueue;
import java.util.Queue;

public class PriorityQueueExample {
    public static void main(String[] args) {
        Queue<Integer> pq = new PriorityQueue<>();
        
        pq.offer(30);
        pq.offer(10);
        pq.offer(20);
        
        System.out.println(pq.poll());  // 10 (minimum)
        System.out.println(pq.poll());  // 20
        System.out.println(pq.poll());  // 30
    }
}
```

---

#### ArrayDeque
**Double-ended queue, circular array implementation**

##### 🔧 Internal Structure
- **Underlying**: Circular Array
- **Pointers**: `head` and `tail` indices
- **Default Capacity**: 16

##### 🎯 How It Works

**1. Circular Array**
- Array treated as circular with wraparound
- When tail reaches end, wraps to beginning

**2. Operations**
- `addFirst()`: Decrement head, add element - O(1)
- `addLast()`: Add at tail, increment tail - O(1)
- `removeFirst()`: Remove at head, increment head - O(1)
- `removeLast()`: Decrement tail, remove - O(1)

**3. Resize**
- Doubles capacity when full
- Copies elements in order

**Real-life analogy:**
ArrayDeque is like a circular conveyor belt - you can add/remove items from both ends efficiently.

##### 📊 Key Points
- ✅ Faster than LinkedList for deque operations
- ✅ No capacity restrictions
- ❌ Null not allowed
- ✅ Better than Stack class for stack operations

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **O(1) operations at both ends** | No random access by index |
| **Faster than LinkedList** | Resizing overhead when full |
| **Memory efficient** | Null elements not allowed |
| **Better than Stack** | Not thread-safe |
| **Cache-friendly (array)** | Circular logic slightly complex |

**When to choose ArrayDeque:**
- ✅ Need stack operations (use instead of Stack)
- ✅ Need queue operations (faster than LinkedList)
- ✅ Need deque (double-ended queue)
- ✅ Performance is important
- ❌ Avoid if need null elements
- ❌ Avoid if need thread-safety

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class ArrayDequeExample {
    public static void main(String[] args) {
        Deque<String> deque = new ArrayDeque<>();
        
        deque.addFirst("A");
        deque.addLast("B");
        deque.addLast("C");
        
        System.out.println(deque);  // [A, B, C]
        System.out.println(deque.removeFirst());  // A
        System.out.println(deque.removeLast());   // C
    }
}
```

---

### 5. Concurrent Collections

#### ConcurrentHashMap
**Thread-safe map without locking entire map**

##### 🔧 Internal Structure (Java 8+)
- **Node array** with synchronized buckets
- **No segment locks** (unlike Java 7)
- **CAS-based operations** (Compare-And-Swap)

##### 🎯 How It Works

**1. Put Operation**

Algorithm:
1. Calculate hash
2. **Empty bucket**: Use CAS to insert (lock-free)
3. **Bucket being moved**: Help with transfer
4. **Normal bucket**: Synchronize on first node only, add/update

**Time Complexity:** O(1) average

**2. Get Operation**
- No locking required
- Volatile reads ensure visibility
- **Time Complexity:** O(1) average

**3. Resize (Transfer)**
- Cooperative resizing (multiple threads help)
- Forwarding nodes redirect to new array

**Real-life analogy:**
ConcurrentHashMap is like a library with multiple librarians - each section can be accessed independently without locking the entire library.

##### 📊 Key Points
- ✅ Thread-safe without external synchronization
- ✅ Lock-free reads
- ✅ Fine-grained locking for writes
- ❌ No null keys/values
- ✅ Weakly consistent iterators

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **Thread-safe without sync** | Slightly slower than HashMap (single-threaded) |
| **Lock-free reads** | More complex implementation |
| **Fine-grained locking** | More memory overhead |
| **Scales with threads** | Weakly consistent (not strongly consistent) |
| **No ConcurrentModificationException** | Cannot use null keys/values |
| **Better than Hashtable** | Size() is approximate (not exact) |

**When to choose ConcurrentHashMap:**
- ✅ Multi-threaded environment
- ✅ High read concurrency
- ✅ Moderate write concurrency
- ✅ Need better performance than synchronized map
- ❌ Avoid if single-threaded (use HashMap)
- ❌ Avoid if need null keys/values
- ❌ Avoid if need strong consistency

```java
import java.util.concurrent.ConcurrentHashMap;
import java.util.Map;

public class ConcurrentHashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> concurrentMap = new ConcurrentHashMap<>();
        
        // Thread-safe operations
        concurrentMap.put("A", 1);
        concurrentMap.put("B", 2);
        
        // Atomic operations
        concurrentMap.putIfAbsent("C", 3);
        concurrentMap.computeIfAbsent("D", k -> 4);
    }
}
```

---

#### CopyOnWriteArrayList
**Thread-safe list for read-heavy workloads**

##### 🔧 Internal Structure
- **Volatile array reference**
- **ReentrantLock** for modifications

##### 🎯 How It Works

**1. Add Operation**

Algorithm:
1. Acquire lock
2. Copy array to new array (size+1)
3. Add element to new array
4. Update volatile reference
5. Release lock

**Time Complexity:** O(n)

**2. Get Operation**
- No locking
- Read volatile array reference
- **Time Complexity:** O(1)

**3. Iterator**
- Snapshot of array at creation time
- Never throws `ConcurrentModificationException`
- Modifications not visible to iterator

**When to Use:**
- ✅ Read-heavy workloads
- ✅ Event listener lists
- ✅ Small collections
- ✅ Iterator consistency crucial

**Real-life analogy:**
CopyOnWriteArrayList is like a newspaper - once printed (snapshot), readers see that version even if new editions are published.

##### 📊 Key Points
- ✅ Perfect thread-safety for reads
- ❌ Expensive writes (full copy)
- ❌ Memory overhead
- ✅ Best for observer patterns

##### ⚖️ Trade-offs

| Benefit | Cost |
|---------|------|
| **Thread-safe reads (no locking)** | O(n) write operations (full copy) |
| **No ConcurrentModificationException** | High memory usage (multiple copies) |
| **Snapshot iterators** | Not suitable for write-heavy workloads |
| **Simple concurrent model** | Stale reads possible (eventual consistency) |
| **Perfect for event listeners** | Poor performance for large collections |

**When to choose CopyOnWriteArrayList:**
- ✅ Read operations >> Write operations (90%+ reads)
- ✅ Small to medium collections
- ✅ Event listener lists
- ✅ Iterator consistency is critical
- ❌ Avoid if frequent modifications
- ❌ Avoid if large collections (memory cost)
- ❌ Avoid if need real-time consistency

```java
import java.util.concurrent.CopyOnWriteArrayList;
import java.util.List;

public class CopyOnWriteExample {
    public static void main(String[] args) {
        List<String> list = new CopyOnWriteArrayList<>();
        
        list.add("A");
        list.add("B");
        
        // Safe to iterate while other threads modify
        for (String item : list) {
            System.out.println(item);
            list.add("C");  // Won't affect this iteration
        }
    }
}
```

---

## 📊 Performance Comparison

### Time Complexity Summary

| Operation | ArrayList | LinkedList | HashMap | TreeMap | PriorityQueue |
|-----------|-----------|------------|---------|---------|---------------|
| **Add (end)** | O(1)* | O(1) | O(1)* | O(log n) | O(log n) |
| **Add (index)** | O(n) | O(n) | - | - | - |
| **Get** | O(1) | O(n) | O(1)* | O(log n) | O(1)** |
| **Remove** | O(n) | O(n) | O(1)* | O(log n) | O(log n) |
| **Contains** | O(n) | O(n) | O(1)* | O(log n) | O(n) |

\* Amortized  
\*\* peek only

---

### When to Use Each Collection

**Lists:**
- **ArrayList**: Random access, iterating, read-heavy
- **LinkedList**: Queue/deque operations, frequent insertions at ends
- **CopyOnWriteArrayList**: Read-heavy concurrent, event listeners

**Sets:**
- **HashSet**: Fast lookup, no ordering needed
- **LinkedHashSet**: Need insertion order
- **TreeSet**: Need sorted order, range queries

**Maps:**
- **HashMap**: Fast lookup, no ordering needed
- **LinkedHashMap**: LRU cache, need ordering
- **TreeMap**: Sorted keys, range queries, ceiling/floor operations
- **ConcurrentHashMap**: Concurrent access without external sync

**Queues:**
- **PriorityQueue**: Priority-based processing
- **ArrayDeque**: Stack/queue operations (better than Stack/LinkedList)

---

## 🎯 Key Takeaways

1. **Hashing**: O(1) average, needs good `hashCode()`
2. **Trees**: O(log n), needs comparable elements
3. **Arrays**: Fast access, slow insertion
4. **Linked**: Fast insertion, slow access
5. **Concurrent**: Lock-free when possible
6. **Trade-offs**: Time vs Space, Simplicity vs Performance

---

## 🚀 Interview Tips

**1. ArrayList vs LinkedList?**
> "ArrayList uses dynamic array (fast random access O(1), slow insertion O(n)). LinkedList uses doubly linked list (slow access O(n), fast insertion at ends O(1)). Use ArrayList for random access, LinkedList for frequent insertions."

**2. How does HashMap work?**
> "HashMap uses array of buckets with hashing. Calculates hash, finds bucket using hash & (n-1), handles collisions with linked lists (converts to trees if chain ≥ 8). Average O(1) operations, resizes at 75% capacity."

**3. HashMap vs TreeMap?**
> "HashMap is O(1) but unordered. TreeMap is O(log n) but maintains sorted order using Red-Black Tree. Use HashMap for speed, TreeMap when you need sorting or range queries."

**4. How to make ArrayList thread-safe?**
> "Use Collections.synchronizedList() or CopyOnWriteArrayList for read-heavy, or use ConcurrentHashMap if you need map operations."

**5. What causes ConcurrentModificationException?**
> "Modifying collection while iterating (except through iterator's remove()). Fix: Use Iterator.remove(), ConcurrentHashMap, or CopyOnWriteArrayList."

---

## 🎯 Collection Trade-offs Decision Guide

### Quick Decision Tree

**Need to store unique elements?**
- ❌ No → Use **List** (ArrayList or LinkedList)
- ✅ Yes → Use **Set** (HashSet, LinkedHashSet, or TreeSet)

**Need key-value pairs?**
- ✅ Yes → Use **Map** (HashMap, LinkedHashMap, or TreeMap)

**Need ordering?**
- ❌ No → **HashMap** or **HashSet**
- ✅ Insertion order → **LinkedHashMap** or **LinkedHashSet**
- ✅ Sorted order → **TreeMap** or **TreeSet**

**Need thread-safety?**
- ✅ Yes → **ConcurrentHashMap** or **CopyOnWriteArrayList**
- ❌ No → Standard collections

**Need priority-based processing?**
- ✅ Yes → **PriorityQueue**

**Need stack/queue operations?**
- ✅ Yes → **ArrayDeque** (best choice)
---

## 📕 LEVEL 5: MULTITHREADING & CONCURRENCY

### 🧵 Thread Basics

**What is a Thread?**
A thread is a lightweight process that allows concurrent execution.

> Think of threads as multiple workers doing tasks simultaneously instead of one worker doing everything sequentially.

**Thread Lifecycle States:**
```
NEW → RUNNABLE → RUNNING → TERMINATED
         ↓          ↓
      BLOCKED   WAITING
```

---

### Creating Threads

**Method 1: Extend Thread class**
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + getName());
    }
}

MyThread t = new MyThread();
t.start();  // Don't call run() directly!
```

**Method 2: Implement Runnable (Preferred)**
```java
class MyTask implements Runnable {
    public void run() {
        System.out.println("Task running");
    }
}

Thread t = new Thread(new MyTask());
t.start();
```

**Method 3: Lambda (Java 8+)**
```java
Thread t = new Thread(() -> {
    System.out.println("Lambda thread running");
});
t.start();
```

---

### Thread vs Runnable

| Aspect | Thread | Runnable |
|--------|--------|----------|
| **Inheritance** | Can't extend other class | Can extend other class |
| **Design** | Tight coupling | Better OOP design |
| **Reusability** | Not reusable | Same task in multiple threads |
| **Interview Pick** | ❌ | ✅ Preferred |

**Interview Tip:**
> "Always prefer Runnable over Thread because Java doesn't support multiple inheritance. Runnable provides better design flexibility."

---

### Important Thread Methods

| Method | Purpose | Note |
|--------|---------|------|
| `start()` | Begins thread execution | Creates new call stack |
| `run()` | Code to execute | Don't call directly! |
| `sleep(ms)` | Pause thread | Releases CPU, NOT lock |
| `join()` | Wait for thread to complete | Blocks calling thread |
| `interrupt()` | Request thread to stop | Sets interrupt flag |
| `isAlive()` | Check if running | Returns boolean |
| `setDaemon(bool)` | Make background thread | Must set before start |

---

### 🔒 Synchronization

**Problem: Race Condition**
Multiple threads accessing shared data simultaneously → unpredictable results.

**Solution: Synchronization**
Ensures only one thread accesses critical section at a time.

---

### Synchronized Method

```java
class Counter {
    private int count = 0;
    
    // Synchronized - thread-safe
    public synchronized void increment() {
        count++;
    }
    
    public synchronized int getCount() {
        return count;
    }
}
```

**Real-life analogy:**
Like a bathroom - only one person can use it at a time (lock), others wait outside.

---

### Synchronized Block

```java
class BankAccount {
    private double balance;
    
    public void withdraw(double amount) {
        // Code before sync block runs concurrently
        System.out.println("Processing withdrawal...");
        
        synchronized(this) {  // Only this section is locked
            if (balance >= amount) {
                balance -= amount;
            }
        }
    }
}
```

**Benefits:**
- ✅ Fine-grained control
- ✅ Better performance (smaller critical section)

---

### 🔐 ReentrantLock

**Problems with synchronized:**
- Cannot interrupt waiting thread
- No timeout option
- Cannot try lock without blocking

**ReentrantLock advantages:**
```java
import java.util.concurrent.locks.ReentrantLock;

class BankAccount {
    private double balance;
    private final ReentrantLock lock = new ReentrantLock();
    
    public void deposit(double amount) {
        lock.lock();
        try {
            balance += amount;
        } finally {
            lock.unlock();  // ALWAYS unlock in finally
        }
    }
    
    public boolean tryWithdraw(double amount) {
        if (lock.tryLock()) {  // Non-blocking attempt
            try {
                if (balance >= amount) {
                    balance -= amount;
                    return true;
                }
                return false;
            } finally {
                lock.unlock();
            }
        }
        return false;  // Couldn't acquire lock
    }
}
```

---

### 🏊 ExecutorService (Thread Pools)

**Problem with raw threads:**
- Thread creation is expensive
- Too many threads = resource exhaustion
- Hard to manage lifecycle

**Solution: Thread Pools**

```java
import java.util.concurrent.*;

// Fixed thread pool (3 threads)
ExecutorService executor = Executors.newFixedThreadPool(3);

// Submit tasks
for (int i = 0; i < 10; i++) {
    executor.submit(() -> {
        System.out.println("Task running on " + Thread.currentThread().getName());
    });
}

// Shutdown
executor.shutdown();
executor.awaitTermination(1, TimeUnit.MINUTES);
```

---

### Thread Pool Types

| Type | Use When | Example |
|------|----------|---------|
| **FixedThreadPool(n)** | Known max concurrent tasks | Web server with fixed workers |
| **CachedThreadPool()** | Many short-lived tasks | Async I/O operations |
| **SingleThreadExecutor()** | Sequential execution needed | Event processing |
| **ScheduledThreadPool(n)** | Delayed/periodic tasks | Scheduled jobs |

---

### 🎯 Callable & Future

**Runnable limitations:**
- Cannot return result
- Cannot throw checked exceptions

**Callable solution:**
```java
import java.util.concurrent.*;

Callable<Integer> task = () -> {
    Thread.sleep(1000);
    return 42;  // Can return result
};

ExecutorService executor = Executors.newFixedThreadPool(1);
Future<Integer> future = executor.submit(task);

// Get result (blocks until available)
Integer result = future.get();
System.out.println("Result: " + result);

executor.shutdown();
```

---

### 🔧 Concurrency Utilities

**1. CountDownLatch**
Wait for multiple threads to complete before proceeding.

```java
CountDownLatch latch = new CountDownLatch(3);

// 3 threads count down
for (int i = 0; i < 3; i++) {
    new Thread(() -> {
        System.out.println("Task completed");
        latch.countDown();
    }).start();
}

latch.await();  // Wait for all 3
System.out.println("All tasks done!");
```

**Real-life analogy:**
Like waiting for all your friends to arrive before starting a movie.

---

**2. CyclicBarrier**
Threads wait for each other at a barrier point.

```java
CyclicBarrier barrier = new CyclicBarrier(3, () -> {
    System.out.println("All reached barrier!");
});

for (int i = 0; i < 3; i++) {
    new Thread(() -> {
        System.out.println("Working...");
        barrier.await();  // Wait for others
        System.out.println("Continuing...");
    }).start();
}
```

**Real-life analogy:**
Like a relay race - all runners must reach the checkpoint before continuing.

---

**3. Semaphore**
Controls access to resources with permits.

```java
Semaphore semaphore = new Semaphore(3);  // 3 permits

// Acquire permit
semaphore.acquire();
try {
    // Use resource
    System.out.println("Using resource");
} finally {
    semaphore.release();  // Return permit
}
```

**Real-life analogy:**
Like parking spaces - only 3 cars can park, others must wait.

---

**4. BlockingQueue (Producer-Consumer)**
Thread-safe queue for producer-consumer pattern.

```java
BlockingQueue<String> queue = new ArrayBlockingQueue<>(10);

// Producer
new Thread(() -> {
    queue.put("Task1");  // Blocks if full
}).start();

// Consumer
new Thread(() -> {
    String task = queue.take();  // Blocks if empty
    System.out.println("Processing: " + task);
}).start();
```

---

### 🎯 Interview Questions

**1. Thread vs Runnable?**
> "Runnable is preferred because Java doesn't support multiple inheritance. Runnable allows class to extend another class while still being used as a thread task."

**2. What is synchronization?**
> "Synchronization prevents race conditions by ensuring only one thread accesses critical section at a time using locks. Use synchronized keyword or ReentrantLock."

**3. Difference between wait() and sleep()?**
> "sleep() pauses thread for specified time, doesn't release lock. wait() releases lock and waits for notify(), used for inter-thread communication."

**4. What is thread pool?**
> "Thread pool reuses existing threads instead of creating new ones. ExecutorService manages thread lifecycle, queuing, and resource limits. More efficient than raw threads."

**5. CountDownLatch vs CyclicBarrier?**
> "CountDownLatch is one-time use, threads wait for count to reach zero. CyclicBarrier is reusable, threads wait for each other. Use CountDownLatch for initialization, CyclicBarrier for iterative algorithms."

---

### 🚀 Best Practices

**✅ Do:**
- Use Runnable over Thread
- Use ExecutorService instead of raw threads
- Always use try-finally with locks
- Handle InterruptedException properly
- Use concurrent collections (ConcurrentHashMap)
- Set initial capacity for thread pools

**❌ Don't:**
- Call run() directly (use start())
- Use Thread.stop() (deprecated, unsafe)
- Hold locks for long operations
- Use synchronized on String literals
- Ignore InterruptedException
- Create unlimited threads

---

## 📕 LEVEL 6: SOLID PRINCIPLES

### 🎯 What are SOLID Principles?

SOLID is an acronym for five design principles that make software more maintainable, flexible, and scalable.

| Letter | Principle | Simple Meaning |
|--------|-----------|----------------|
| **S** | Single Responsibility | One class, one job |
| **O** | Open/Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | Subclass should work like parent |
| **I** | Interface Segregation | Small, specific interfaces |
| **D** | Dependency Inversion | Depend on abstractions, not concrete classes |

---

### 1️⃣ Single Responsibility Principle (SRP)

**Definition:**
> A class should have only ONE reason to change.

**Simple meaning:**
One class = One job

**Why it matters:**
- ✅ Easier to understand
- ✅ Easier to test
- ✅ Changes don't affect unrelated code
- ✅ Better maintainability

**How to identify violations:**
- Class description uses "and" (does X AND Y)
- Class has multiple unrelated methods
- Changes in one area require modifying the class

---

**❌ Bad Example:**
```java
// UserManager does TOO MANY things
class UserManager {
    void saveToDatabase(User user) {
        // Database logic
    }
    
    void sendEmail(User user) {
        // Email logic
    }
    
    void generateReport(User user) {
        // Report logic
    }
}
```

**✅ Good Example:**
```java
// Each class has ONE responsibility
class UserRepository {
    void save(User user) {
        // Only database operations
    }
}

class EmailService {
    void send(String to, String message) {
        // Only email operations
    }
}

class ReportGenerator {
    Report generate(User user) {
        // Only report generation
    }
}
```

**Real-life analogy:**
A restaurant has separate roles - chef (cooking), waiter (serving), cashier (billing). Each person has one job, not all jobs.

---

### 2️⃣ Open/Closed Principle (OCP)

**Definition:**
> Open for extension, closed for modification.

**Simple meaning:**
Add new features without changing existing code.

**Why it matters:**
- ✅ Reduces risk of breaking existing code
- ✅ Makes code more maintainable
- ✅ Supports polymorphism
- ✅ Easier to add new features

**How to achieve:**
- Use interfaces/abstract classes
- Rely on polymorphism
- Use design patterns (Strategy, Template Method)

---

**❌ Bad Example:**
```java
// Need to modify this class for every new shape
class AreaCalculator {
    double calculateArea(Object shape) {
        if (shape instanceof Circle) {
            Circle c = (Circle) shape;
            return Math.PI * c.radius * c.radius;
        } else if (shape instanceof Square) {
            Square s = (Square) shape;
            return s.side * s.side;
        }
        // Need to add more if-else for new shapes!
        return 0;
    }
}
```

**✅ Good Example:**
```java
// Can add new shapes without modifying existing code
interface Shape {
    double area();
}

class Circle implements Shape {
    private double radius;
    
    public double area() {
        return Math.PI * radius * radius;
    }
}

class Square implements Shape {
    private double side;
    
    public double area() {
        return side * side;
    }
}

// Add new shape - no existing code changed!
class Triangle implements Shape {
    private double base, height;
    
    public double area() {
        return 0.5 * base * height;
    }
}

// Calculator doesn't need modification
class AreaCalculator {
    double calculateArea(Shape shape) {
        return shape.area();  // Polymorphism!
    }
}
```

**Real-life analogy:**
Like a power outlet - you can plug in new devices (extension) without changing the outlet itself (modification).

---

### 3️⃣ Liskov Substitution Principle (LSP)

**Definition:**
> Subclass should be substitutable for its parent class without breaking the application.

**Simple meaning:**
If you replace parent with child, everything should still work.

**Why it matters:**
- ✅ Ensures proper inheritance
- ✅ Prevents unexpected behavior
- ✅ Maintains code contracts
- ✅ Enables safe polymorphism

**Rules:**
- Subclass should not throw new exceptions
- Subclass should not have stricter requirements
- Subclass behavior should match parent expectations

---

**❌ Bad Example:**
```java
// Penguin violates LSP - can't fly like other birds
class Bird {
    void fly() {
        System.out.println("Flying...");
    }
}

class Penguin extends Bird {
    @Override
    void fly() {
        throw new UnsupportedOperationException("Penguins can't fly!");
    }
}

// This breaks!
Bird bird = new Penguin();
bird.fly();  // Exception! LSP violated
```

**✅ Good Example:**
```java
// Separate flying and non-flying birds
abstract class Bird {
    abstract void move();
}

abstract class FlyingBird extends Bird {
    void move() {
        fly();
    }
    
    abstract void fly();
}

class Sparrow extends FlyingBird {
    void fly() {
        System.out.println("Sparrow flying");
    }
}

class Penguin extends Bird {
    void move() {
        swim();
    }
    
    void swim() {
        System.out.println("Penguin swimming");
    }
}

// Now both work correctly
Bird sparrow = new Sparrow();
sparrow.move();  // Flies

Bird penguin = new Penguin();
penguin.move();  // Swims
```

**Real-life analogy:**
If a recipe says "use any fruit," you should be able to use apple, orange, or banana without the recipe failing. If tomato breaks the recipe, it violates the principle.

---

### 4️⃣ Interface Segregation Principle (ISP)

**Definition:**
> Clients should not be forced to depend on interfaces they don't use.

**Simple meaning:**
Many small interfaces > One large interface

**Why it matters:**
- ✅ Reduces coupling
- ✅ Classes implement only what they need
- ✅ Easier to understand
- ✅ More flexible

**Signs of violation:**
- Empty method implementations
- Throwing `UnsupportedOperationException`
- Methods that do nothing

---

**❌ Bad Example:**
```java
// Fat interface - not all workers need all methods
interface Worker {
    void work();
    void eat();
    void sleep();
}

// Robot forced to implement eat() and sleep()
class Robot implements Worker {
    public void work() {
        System.out.println("Robot working");
    }
    
    public void eat() {
        // Robots don't eat!
        throw new UnsupportedOperationException();
    }
    
    public void sleep() {
        // Robots don't sleep!
        throw new UnsupportedOperationException();
    }
}
```

**✅ Good Example:**
```java
// Small, specific interfaces
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

interface Sleepable {
    void sleep();
}

// Robot implements only what it needs
class Robot implements Workable {
    public void work() {
        System.out.println("Robot working");
    }
}

// Human implements all
class Human implements Workable, Eatable, Sleepable {
    public void work() {
        System.out.println("Human working");
    }
    
    public void eat() {
        System.out.println("Human eating");
    }
    
    public void sleep() {
        System.out.println("Human sleeping");
    }
}
```

**Real-life analogy:**
Like a restaurant menu - vegetarian customers shouldn't be forced to see meat options. Separate menus (interfaces) for different needs.

---

### 5️⃣ Dependency Inversion Principle (DIP)

**Definition:**
> High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Simple meaning:**
Depend on interfaces, not concrete classes.

**Why it matters:**
- ✅ Reduces coupling
- ✅ Easier to test (can mock dependencies)
- ✅ Flexible to change implementations
- ✅ Supports plugin architectures

**Key concepts:**
- **High-level**: Business logic (UserService)
- **Low-level**: Implementation details (MySQLDatabase)
- **Abstraction**: Interface (Database)

---

**❌ Bad Example:**
```java
// UserService directly depends on MySQL
class MySQLDatabase {
    void save(String data) {
        System.out.println("Saving to MySQL: " + data);
    }
}

class UserService {
    private MySQLDatabase db = new MySQLDatabase();  // Tight coupling!
    
    void saveUser(String user) {
        db.save(user);
    }
}

// Problem: Can't switch to PostgreSQL without changing UserService
```

**✅ Good Example:**
```java
// Abstraction (interface)
interface Database {
    void save(String data);
}

// Low-level implementations
class MySQLDatabase implements Database {
    public void save(String data) {
        System.out.println("Saving to MySQL: " + data);
    }
}

class PostgreSQLDatabase implements Database {
    public void save(String data) {
        System.out.println("Saving to PostgreSQL: " + data);
    }
}

class MongoDatabase implements Database {
    public void save(String data) {
        System.out.println("Saving to MongoDB: " + data);
    }
}

// High-level module depends on abstraction
class UserService {
    private Database db;
    
    // Constructor Injection (Dependency Injection)
    public UserService(Database db) {
        this.db = db;  // Flexible!
    }
    
    void saveUser(String user) {
        db.save(user);
    }
}

// Usage - easy to switch implementations
public class Main {
    public static void main(String[] args) {
        // Can use any database implementation
        Database db = new MySQLDatabase();
        UserService service = new UserService(db);
        service.saveUser("John");
        
        // Easy to switch
        Database mongoDB = new MongoDatabase();
        UserService mongoService = new UserService(mongoDB);
        mongoService.saveUser("Alice");
    }
}
```

**Real-life analogy:**
Like a phone charger - you don't build phone for specific wall outlet. Phone uses USB interface (abstraction), can work with any USB charger (implementation).

---

### 🎯 SOLID Principles Summary

| Principle | One-Line Summary | Key Benefit |
|-----------|------------------|-------------|
| **SRP** | One class, one job | Easy to maintain |
| **OCP** | Extend, don't modify | Safe to add features |
| **LSP** | Subclass works like parent | Safe polymorphism |
| **ISP** | Small, specific interfaces | No forced dependencies |
| **DIP** | Depend on abstractions | Flexible, testable |

---

### 🚀 Interview Tips

**1. Explain SRP with example:**
> "SRP means one class should have one responsibility. Example: UserRepository handles database, EmailService handles emails. Don't mix them in one class."

**2. What is Open/Closed Principle?**
> "Open for extension, closed for modification. Use interfaces and polymorphism to add new features without changing existing code. Example: Add new Shape without modifying AreaCalculator."

**3. Explain Dependency Inversion:**
> "High-level modules shouldn't depend on low-level modules. Both depend on abstractions (interfaces). Use dependency injection to inject implementations. Makes code flexible and testable."

**4. Why is Liskov Substitution important?**
> "Ensures subclasses can replace parent classes without breaking code. If Penguin extends Bird but can't fly, it violates LSP. Better to have separate hierarchies for flying and non-flying birds."

**5. When do you use Interface Segregation?**
> "When interface has methods not all implementations need. Split into smaller interfaces so classes implement only what they need. Example: Robot shouldn't implement eat() and sleep()."

---

### 💡 Real-World Application

**When building a payment system:**

```java
// SRP - Separate responsibilities
class PaymentProcessor { }
class PaymentValidator { }
class PaymentLogger { }

// OCP - Easy to add new payment methods
interface PaymentMethod {
    void pay(double amount);
}
class CreditCard implements PaymentMethod { }
class PayPal implements PaymentMethod { }
class Crypto implements PaymentMethod { }  // New method - no changes needed

// DIP - Depend on interface
class CheckoutService {
    private PaymentMethod paymentMethod;
    
    CheckoutService(PaymentMethod paymentMethod) {
        this.paymentMethod = paymentMethod;
    }
}
```

---

### 🎓 Key Takeaways

1. **SRP**: Keep classes focused (one responsibility)
2. **OCP**: Use polymorphism to extend behavior
3. **LSP**: Ensure proper inheritance (subclass works like parent)
4. **ISP**: Create small, role-specific interfaces
5. **DIP**: Inject dependencies, depend on abstractions

**Remember:**
> "SOLID principles are guidelines, not strict rules. Apply them when they add value, not blindly. The goal is maintainable, flexible code."

---

## 📕 LEVEL 7: DESIGN PATTERNS

### 🎯 What are Design Patterns?

Design patterns are proven solutions to common programming problems.

> Think of them as recipes for solving recurring design challenges in software development.

**Categories:**
1. **Creational** - How objects are created (Singleton, Factory, Builder)
2. **Structural** - How objects are composed (Adapter, Decorator, Facade)
3. **Behavioral** - How objects interact (Observer, Strategy, Command, Template)

---

## Creational Patterns

### 1️⃣ Singleton Pattern

**Purpose:**
> Ensure a class has only ONE instance and provide global access to it.

**When to use:**
- Database connection
- Configuration manager
- Logger
- Thread pool

**Real-life analogy:**
Like a country's president - there can be only one at a time, everyone accesses the same person.

---

**Implementation:**

```java
public class DatabaseConnection {
    // 1. Private static instance
    private static DatabaseConnection instance;
    
    // 2. Private constructor (prevents external instantiation)
    private DatabaseConnection() {
        System.out.println("Database connection created");
    }
    
    // 3. Public static method to get instance
    public static DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }
    
    public void query(String sql) {
        System.out.println("Executing: " + sql);
    }
}

// Usage
DatabaseConnection db1 = DatabaseConnection.getInstance();
DatabaseConnection db2 = DatabaseConnection.getInstance();
System.out.println(db1 == db2);  // true - same instance
```

---

**Thread-Safe Singleton:**

```java
public class ThreadSafeSingleton {
    // Eager initialization (created at class loading)
    private static final ThreadSafeSingleton instance = new ThreadSafeSingleton();
    
    private ThreadSafeSingleton() { }
    
    public static ThreadSafeSingleton getInstance() {
        return instance;
    }
}

// OR Double-checked locking (lazy + thread-safe)
public class LazyThreadSafeSingleton {
    private static volatile LazyThreadSafeSingleton instance;
    
    private LazyThreadSafeSingleton() { }
    
    public static LazyThreadSafeSingleton getInstance() {
        if (instance == null) {
            synchronized (LazyThreadSafeSingleton.class) {
                if (instance == null) {
                    instance = new LazyThreadSafeSingleton();
                }
            }
        }
        return instance;
    }
}
```

**Interview Tip:**
> "Singleton ensures one instance. Use eager initialization for simplicity or double-checked locking for lazy initialization with thread-safety. Beware: can make testing difficult."

---

### 2️⃣ Factory Pattern

**Purpose:**
> Create objects without specifying exact class. Let subclasses decide which class to instantiate.

**When to use:**
- Object creation is complex
- Need to return different types based on input
- Want to hide creation logic

**Real-life analogy:**
Like ordering at a restaurant - you ask for "pizza" and the kitchen decides whether to make margherita, pepperoni, or veggie based on your preferences.

---

**Implementation:**

```java
// Product interface
interface Vehicle {
    void drive();
}

// Concrete products
class Car implements Vehicle {
    public void drive() {
        System.out.println("Driving a car");
    }
}

class Bike implements Vehicle {
    public void drive() {
        System.out.println("Riding a bike");
    }
}

class Truck implements Vehicle {
    public void drive() {
        System.out.println("Driving a truck");
    }
}

// Factory class
class VehicleFactory {
    public static Vehicle createVehicle(String type) {
        switch (type.toLowerCase()) {
            case "car":
                return new Car();
            case "bike":
                return new Bike();
            case "truck":
                return new Truck();
            default:
                throw new IllegalArgumentException("Unknown vehicle type");
        }
    }
}

// Usage
Vehicle vehicle = VehicleFactory.createVehicle("car");
vehicle.drive();  // Driving a car

Vehicle bike = VehicleFactory.createVehicle("bike");
bike.drive();  // Riding a bike
```

**Benefits:**
- ✅ Loose coupling (client doesn't know concrete classes)
- ✅ Easy to add new types
- ✅ Centralized creation logic

**Interview Tip:**
> "Factory pattern creates objects without exposing creation logic. Client requests object by type, factory returns appropriate instance. Example: VehicleFactory creates Car, Bike, or Truck based on input."

---

### 3️⃣ Builder Pattern

**Purpose:**
> Construct complex objects step by step. Separate construction from representation.

**When to use:**
- Many constructor parameters (4+)
- Optional parameters
- Immutable objects
- Step-by-step construction

**Real-life analogy:**
Like building a custom burger - you choose bread, patty, cheese, toppings step by step, then get the final burger.

---

**Implementation:**

```java
// Product class
class User {
    // Required parameters
    private final String username;
    private final String email;
    
    // Optional parameters
    private final String phone;
    private final String address;
    private final int age;
    
    // Private constructor
    private User(UserBuilder builder) {
        this.username = builder.username;
        this.email = builder.email;
        this.phone = builder.phone;
        this.address = builder.address;
        this.age = builder.age;
    }
    
    // Static nested Builder class
    public static class UserBuilder {
        // Required parameters
        private final String username;
        private final String email;
        
        // Optional parameters (with defaults)
        private String phone = "";
        private String address = "";
        private int age = 0;
        
        // Constructor with required parameters
        public UserBuilder(String username, String email) {
            this.username = username;
            this.email = email;
        }
        
        // Setter methods return 'this' for chaining
        public UserBuilder phone(String phone) {
            this.phone = phone;
            return this;
        }
        
        public UserBuilder address(String address) {
            this.address = address;
            return this;
        }
        
        public UserBuilder age(int age) {
            this.age = age;
            return this;
        }
        
        // Build method creates the User
        public User build() {
            return new User(this);
        }
    }
    
    @Override
    public String toString() {
        return "User{username='" + username + "', email='" + email + 
               "', phone='" + phone + "', address='" + address + 
               "', age=" + age + "}";
    }
}

// Usage - Fluent API
User user = new User.UserBuilder("john_doe", "john@example.com")
                .phone("123-456-7890")
                .address("123 Main St")
                .age(30)
                .build();

// Can skip optional parameters
User simpleUser = new User.UserBuilder("jane_doe", "jane@example.com")
                    .build();
```

**Benefits:**
- ✅ Readable code (method chaining)
- ✅ Immutable objects
- ✅ No telescoping constructors
- ✅ Optional parameters handled elegantly

**Interview Tip:**
> "Builder pattern constructs complex objects step by step using method chaining. Useful when object has many optional parameters. Example: User with required username/email and optional phone/address/age."

---

## Structural Patterns

### 4️⃣ Adapter Pattern

**Purpose:**
> Convert interface of a class into another interface clients expect. Makes incompatible interfaces work together.

**When to use:**
- Integrate legacy code with new code
- Use third-party library with different interface
- Make incompatible classes work together

**Real-life analogy:**
Like a power adapter - converts US plug (110V) to EU socket (220V), making incompatible devices work together.

---

**Implementation:**

```java
// Target interface (what client expects)
interface MediaPlayer {
    void play(String filename);
}

// Adaptee (existing class with different interface)
class AdvancedMediaPlayer {
    void playMp4(String filename) {
        System.out.println("Playing MP4: " + filename);
    }
    
    void playVlc(String filename) {
        System.out.println("Playing VLC: " + filename);
    }
}

// Adapter (makes AdvancedMediaPlayer compatible with MediaPlayer)
class MediaAdapter implements MediaPlayer {
    private AdvancedMediaPlayer advancedPlayer;
    
    public MediaAdapter() {
        this.advancedPlayer = new AdvancedMediaPlayer();
    }
    
    @Override
    public void play(String filename) {
        if (filename.endsWith(".mp4")) {
            advancedPlayer.playMp4(filename);
        } else if (filename.endsWith(".vlc")) {
            advancedPlayer.playVlc(filename);
        }
    }
}

// Client code
class AudioPlayer implements MediaPlayer {
    private MediaAdapter adapter;
    
    @Override
    public void play(String filename) {
        if (filename.endsWith(".mp3")) {
            System.out.println("Playing MP3: " + filename);
        } else {
            // Use adapter for other formats
            adapter = new MediaAdapter();
            adapter.play(filename);
        }
    }
}

// Usage
MediaPlayer player = new AudioPlayer();
player.play("song.mp3");
player.play("video.mp4");
player.play("movie.vlc");
```

**Interview Tip:**
> "Adapter pattern makes incompatible interfaces work together. Like a power adapter converting plugs. Example: Wrap legacy class with new interface that client expects."

---

### 5️⃣ Decorator Pattern

**Purpose:**
> Add new functionality to objects dynamically without altering their structure.

**When to use:**
- Add responsibilities to objects at runtime
- Extend functionality without subclassing
- Combine multiple features

**Real-life analogy:**
Like decorating a pizza - start with base pizza, add toppings (cheese, pepperoni, olives) one by one. Each topping adds to the price and description.

---

**Implementation:**

```java
// Component interface
interface Coffee {
    String getDescription();
    double getCost();
}

// Concrete component
class SimpleCoffee implements Coffee {
    public String getDescription() {
        return "Simple Coffee";
    }
    
    public double getCost() {
        return 2.0;
    }
}

// Decorator base class
abstract class CoffeeDecorator implements Coffee {
    protected Coffee coffee;
    
    public CoffeeDecorator(Coffee coffee) {
        this.coffee = coffee;
    }
    
    public String getDescription() {
        return coffee.getDescription();
    }
    
    public double getCost() {
        return coffee.getCost();
    }
}

// Concrete decorators
class Milk extends CoffeeDecorator {
    public Milk(Coffee coffee) {
        super(coffee);
    }
    
    public String getDescription() {
        return coffee.getDescription() + ", Milk";
    }
    
    public double getCost() {
        return coffee.getCost() + 0.5;
    }
}

class Sugar extends CoffeeDecorator {
    public Sugar(Coffee coffee) {
        super(coffee);
    }
    
    public String getDescription() {
        return coffee.getDescription() + ", Sugar";
    }
    
    public double getCost() {
        return coffee.getCost() + 0.2;
    }
}

class Whip extends CoffeeDecorator {
    public Whip(Coffee coffee) {
        super(coffee);
    }
    
    public String getDescription() {
        return coffee.getDescription() + ", Whipped Cream";
    }
    
    public double getCost() {
        return coffee.getCost() + 0.7;
    }
}

// Usage - Stack decorators
Coffee coffee = new SimpleCoffee();
System.out.println(coffee.getDescription() + " = $" + coffee.getCost());
// Simple Coffee = $2.0

coffee = new Milk(coffee);
System.out.println(coffee.getDescription() + " = $" + coffee.getCost());
// Simple Coffee, Milk = $2.5

coffee = new Sugar(coffee);
coffee = new Whip(coffee);
System.out.println(coffee.getDescription() + " = $" + coffee.getCost());
// Simple Coffee, Milk, Sugar, Whipped Cream = $3.4
```

**Benefits:**
- ✅ Add features dynamically at runtime
- ✅ Flexible alternative to subclassing
- ✅ Combine multiple decorators

**Interview Tip:**
> "Decorator pattern adds functionality to objects dynamically without changing their structure. Like adding toppings to pizza. Each decorator wraps the object and adds behavior."

---

### 6️⃣ Facade Pattern

**Purpose:**
> Provide simplified interface to complex subsystem. Hide complexity behind simple interface.

**When to use:**
- Complex system with many classes
- Want to provide simple API
- Decouple client from subsystem

**Real-life analogy:**
Like a hotel receptionist - you don't directly contact housekeeping, restaurant, and maintenance. Receptionist provides simple interface to all services.

---

**Implementation:**

```java
// Complex subsystem classes
class CPU {
    void freeze() { System.out.println("CPU: Freezing..."); }
    void jump(long position) { System.out.println("CPU: Jumping to " + position); }
    void execute() { System.out.println("CPU: Executing..."); }
}

class Memory {
    void load(long position, byte[] data) {
        System.out.println("Memory: Loading data at " + position);
    }
}

class HardDrive {
    byte[] read(long lba, int size) {
        System.out.println("HardDrive: Reading " + size + " bytes from " + lba);
        return new byte[size];
    }
}

// Facade - Simple interface to complex subsystem
class ComputerFacade {
    private CPU cpu;
    private Memory memory;
    private HardDrive hardDrive;
    
    public ComputerFacade() {
        this.cpu = new CPU();
        this.memory = new Memory();
        this.hardDrive = new HardDrive();
    }
    
    // Simple method hiding complex operations
    public void start() {
        System.out.println("Starting computer...\n");
        cpu.freeze();
        memory.load(0, hardDrive.read(0, 1024));
        cpu.jump(0);
        cpu.execute();
        System.out.println("\nComputer started!");
    }
}

// Usage - Simple!
ComputerFacade computer = new ComputerFacade();
computer.start();  // One method does everything
```

**Benefits:**
- ✅ Simplifies complex systems
- ✅ Reduces dependencies
- ✅ Easy to use

**Interview Tip:**
> "Facade pattern provides simple interface to complex subsystem. Like a hotel receptionist coordinating multiple services. Client calls one method, facade handles complexity internally."

---

## Behavioral Patterns

### 7️⃣ Observer Pattern

**Purpose:**
> Define one-to-many dependency. When one object changes state, all dependents are notified automatically.

**When to use:**
- Event handling systems
- Publish-subscribe systems
- MVC architecture (Model notifies View)

**Real-life analogy:**
Like YouTube subscriptions - when a channel (subject) uploads video, all subscribers (observers) get notified automatically.

---

**Implementation:**

```java
import java.util.*;

// Observer interface
interface Observer {
    void update(String message);
}

// Subject interface
interface Subject {
    void attach(Observer observer);
    void detach(Observer observer);
    void notifyObservers();
}

// Concrete Subject
class NewsAgency implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String news;
    
    public void attach(Observer observer) {
        observers.add(observer);
    }
    
    public void detach(Observer observer) {
        observers.remove(observer);
    }
    
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(news);
        }
    }
    
    public void setNews(String news) {
        this.news = news;
        notifyObservers();  // Notify all subscribers
    }
}

// Concrete Observers
class NewsChannel implements Observer {
    private String name;
    
    public NewsChannel(String name) {
        this.name = name;
    }
    
    public void update(String news) {
        System.out.println(name + " received news: " + news);
    }
}

// Usage
NewsAgency agency = new NewsAgency();

NewsChannel cnn = new NewsChannel("CNN");
NewsChannel bbc = new NewsChannel("BBC");
NewsChannel fox = new NewsChannel("FOX");

// Subscribe
agency.attach(cnn);
agency.attach(bbc);
agency.attach(fox);

// Publish news - all subscribers notified
agency.setNews("Breaking: New Java version released!");
// CNN received news: Breaking: New Java version released!
// BBC received news: Breaking: New Java version released!
// FOX received news: Breaking: New Java version released!

// Unsubscribe
agency.detach(fox);
agency.setNews("Update: Java 21 features announced");
// Only CNN and BBC receive this
```

**Benefits:**
- ✅ Loose coupling between subject and observers
- ✅ Dynamic subscription/unsubscription
- ✅ Broadcast communication

**Interview Tip:**
> "Observer pattern implements publish-subscribe. Subject maintains list of observers, notifies them on state change. Like YouTube subscriptions - channel notifies all subscribers when new video is uploaded."

---

### 8️⃣ Strategy Pattern

**Purpose:**
> Define family of algorithms, encapsulate each one, and make them interchangeable.

**When to use:**
- Multiple algorithms for same task
- Want to switch algorithms at runtime
- Avoid multiple if-else or switch statements

**Real-life analogy:**
Like choosing transportation to work - you can walk, bike, drive, or take bus. Same goal (reach work), different strategies.

---

**Implementation:**

```java
// Strategy interface
interface PaymentStrategy {
    void pay(double amount);
}

// Concrete strategies
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;
    
    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }
    
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using Credit Card: " + cardNumber);
    }
}

class PayPalPayment implements PaymentStrategy {
    private String email;
    
    public PayPalPayment(String email) {
        this.email = email;
    }
    
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using PayPal: " + email);
    }
}

class CryptoPayment implements PaymentStrategy {
    private String walletAddress;
    
    public CryptoPayment(String walletAddress) {
        this.walletAddress = walletAddress;
    }
    
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using Crypto: " + walletAddress);
    }
}

// Context class
class ShoppingCart {
    private PaymentStrategy paymentStrategy;
    
    public void setPaymentStrategy(PaymentStrategy strategy) {
        this.paymentStrategy = strategy;
    }
    
    public void checkout(double amount) {
        paymentStrategy.pay(amount);
    }
}

// Usage - Switch strategies at runtime
ShoppingCart cart = new ShoppingCart();

cart.setPaymentStrategy(new CreditCardPayment("1234-5678-9012"));
cart.checkout(100.0);  // Paid using Credit Card

cart.setPaymentStrategy(new PayPalPayment("john@example.com"));
cart.checkout(50.0);   // Paid using PayPal

cart.setPaymentStrategy(new CryptoPayment("0x123abc"));
cart.checkout(75.0);   // Paid using Crypto
```

**Benefits:**
- ✅ Eliminates conditional statements
- ✅ Easy to add new strategies
- ✅ Switch algorithms at runtime

**Interview Tip:**
> "Strategy pattern defines family of algorithms and makes them interchangeable. Context uses strategy interface, can switch implementations at runtime. Example: Different payment methods in shopping cart."

---

### 9️⃣ Command Pattern

**Purpose:**
> Encapsulate request as an object. Allows parameterization, queuing, and undo operations.

**When to use:**
- Need to queue operations
- Need undo/redo functionality
- Need to log operations
- Decouple sender from receiver

**Real-life analogy:**
Like a remote control - each button is a command object. Pressing button executes command without knowing how TV works internally.

---

**Implementation:**

```java
// Command interface
interface Command {
    void execute();
    void undo();
}

// Receiver (actual object that performs action)
class Light {
    private boolean isOn = false;
    
    public void turnOn() {
        isOn = true;
        System.out.println("Light is ON");
    }
    
    public void turnOff() {
        isOn = false;
        System.out.println("Light is OFF");
    }
}

// Concrete commands
class LightOnCommand implements Command {
    private Light light;
    
    public LightOnCommand(Light light) {
        this.light = light;
    }
    
    public void execute() {
        light.turnOn();
    }
    
    public void undo() {
        light.turnOff();
    }
}

class LightOffCommand implements Command {
    private Light light;
    
    public LightOffCommand(Light light) {
        this.light = light;
    }
    
    public void execute() {
        light.turnOff();
    }
    
    public void undo() {
        light.turnOn();
    }
}

// Invoker (remote control)
class RemoteControl {
    private Command command;
    private Stack<Command> history = new Stack<>();
    
    public void setCommand(Command command) {
        this.command = command;
    }
    
    public void pressButton() {
        command.execute();
        history.push(command);
    }
    
    public void pressUndo() {
        if (!history.isEmpty()) {
            Command lastCommand = history.pop();
            lastCommand.undo();
        }
    }
}

// Usage
Light livingRoomLight = new Light();

Command lightOn = new LightOnCommand(livingRoomLight);
Command lightOff = new LightOffCommand(livingRoomLight);

RemoteControl remote = new RemoteControl();

remote.setCommand(lightOn);
remote.pressButton();  // Light is ON

remote.setCommand(lightOff);
remote.pressButton();  // Light is OFF

remote.pressUndo();    // Light is ON (undo last command)
```

**Benefits:**
- ✅ Decouples sender from receiver
- ✅ Easy to add new commands
- ✅ Supports undo/redo
- ✅ Can queue/log commands

**Interview Tip:**
> "Command pattern encapsulates request as object. Enables undo/redo, queuing, and logging. Example: Remote control with buttons (commands) controlling devices (receivers)."

---

### 🔟 Template Method Pattern

**Purpose:**
> Define skeleton of algorithm in base class, let subclasses override specific steps.

**When to use:**
- Common algorithm structure with varying steps
- Want to avoid code duplication
- Control extension points

**Real-life analogy:**
Like a recipe template - making tea and coffee follow same steps (boil water, add ingredient, pour in cup), but ingredients differ.

---

**Implementation:**

```java
// Abstract class with template method
abstract class DataProcessor {
    
    // Template method - defines algorithm skeleton
    public final void process() {
        readData();
        processData();
        saveData();
    }
    
    // Common implementation
    private void readData() {
        System.out.println("Reading data from source");
    }
    
    // Abstract - subclasses must implement
    protected abstract void processData();
    
    // Hook method - subclasses can override (optional)
    protected void saveData() {
        System.out.println("Saving data to default location");
    }
}

// Concrete implementations
class CSVProcessor extends DataProcessor {
    @Override
    protected void processData() {
        System.out.println("Processing CSV data");
    }
}

class XMLProcessor extends DataProcessor {
    @Override
    protected void processData() {
        System.out.println("Processing XML data");
    }
    
    @Override
    protected void saveData() {
        System.out.println("Saving XML to database");
    }
}

class JSONProcessor extends DataProcessor {
    @Override
    protected void processData() {
        System.out.println("Processing JSON data");
    }
}

// Usage
DataProcessor csvProcessor = new CSVProcessor();
csvProcessor.process();
// Reading data from source
// Processing CSV data
// Saving data to default location

DataProcessor xmlProcessor = new XMLProcessor();
xmlProcessor.process();
// Reading data from source
// Processing XML data
// Saving XML to database
```

**Benefits:**
- ✅ Code reuse (common steps in base class)
- ✅ Control over algorithm structure
- ✅ Subclasses override only specific steps

**Interview Tip:**
> "Template Method defines algorithm skeleton in base class, subclasses override specific steps. Example: DataProcessor has common steps (read, process, save), subclasses implement process() differently for CSV, XML, JSON."

---

## 📊 Design Patterns Comparison

### Quick Reference Table

| Pattern | Category | Purpose | Example |
|---------|----------|---------|---------|
| **Singleton** | Creational | One instance only | Database connection |
| **Factory** | Creational | Create objects without specifying class | Vehicle factory |
| **Builder** | Creational | Construct complex objects step by step | User with many fields |
| **Adapter** | Structural | Make incompatible interfaces work | Power adapter |
| **Decorator** | Structural | Add functionality dynamically | Coffee with toppings |
| **Facade** | Structural | Simplify complex system | Computer startup |
| **Observer** | Behavioral | Notify dependents of changes | YouTube subscriptions |
| **Strategy** | Behavioral | Interchangeable algorithms | Payment methods |
| **Command** | Behavioral | Encapsulate request as object | Remote control |
| **Template** | Behavioral | Algorithm skeleton with varying steps | Data processors |

---

### When to Use Which Pattern?

**Need to control object creation?**
- One instance → **Singleton**
- Hide creation logic → **Factory**
- Many optional parameters → **Builder**

**Need to work with existing code?**
- Incompatible interfaces → **Adapter**
- Add features without changing code → **Decorator**
- Simplify complex system → **Facade**

**Need flexible behavior?**
- Notify multiple objects → **Observer**
- Switch algorithms at runtime → **Strategy**
- Undo/redo operations → **Command**
- Common algorithm with varying steps → **Template Method**

---

## 🎯 Interview Questions

**1. Explain Singleton pattern and its use cases.**
> "Singleton ensures only one instance of a class exists. Use for database connections, loggers, configuration managers. Implement with private constructor and static getInstance() method. Make thread-safe with eager initialization or double-checked locking."

**2. Difference between Factory and Builder?**
> "Factory creates objects based on type (which class to instantiate). Builder constructs complex objects step by step (how to configure one class). Use Factory for different types, Builder for many optional parameters."

**3. When would you use Adapter pattern?**
> "When integrating incompatible interfaces. Example: Legacy code with old interface needs to work with new system. Adapter wraps old code and implements new interface."

**4. Decorator vs Inheritance?**
> "Decorator adds functionality at runtime without subclassing. More flexible than inheritance - can combine multiple decorators. Example: Coffee with milk, sugar, whip (stack decorators) vs creating subclass for each combination."

**5. Observer pattern real-world example?**
> "Event handling in GUI - button (subject) notifies listeners (observers) when clicked. Or model-view in MVC - model changes, all views get notified and update automatically."

**6. Strategy vs Template Method?**
> "Strategy uses composition (has-a), Template uses inheritance (is-a). Strategy switches entire algorithm, Template changes specific steps. Use Strategy for runtime switching, Template for code reuse with variations."

---

## 💡 Design Patterns Best Practices

**✅ Do:**
- Use patterns to solve actual problems
- Understand the problem before applying pattern
- Combine patterns when needed
- Keep it simple (don't over-engineer)

**❌ Don't:**
- Force patterns where not needed
- Use patterns just to show off
- Apply patterns without understanding trade-offs
- Over-complicate simple problems

**Remember:**
> "Design patterns are tools, not goals. Use them to make code better, not just to use patterns."

---

## 🎓 Pattern Selection Guide

### Problem: Need to create objects

| Scenario | Pattern | Why |
|----------|---------|-----|
| Only one instance needed | Singleton | Shared resource |
| Create different types | Factory | Hide creation logic |
| Many optional parameters | Builder | Readable construction |

### Problem: Need to modify structure

| Scenario | Pattern | Why |
|----------|---------|-----|
| Incompatible interfaces | Adapter | Make them compatible |
| Add features dynamically | Decorator | Flexible extension |
| Simplify complex system | Facade | Easy-to-use interface |

### Problem: Need flexible behavior

| Scenario | Pattern | Why |
|----------|---------|-----|
| Notify multiple objects | Observer | Automatic updates |
| Switch algorithms | Strategy | Runtime flexibility |
| Undo/redo operations | Command | Encapsulate actions |
| Common steps, varying details | Template | Code reuse |

---

|| Common steps, varying details | Template | Code reuse |

---

# 📕 LEVEL 8: SPRING FRAMEWORK

## Spring Core Concepts

### 🎯 What is Spring Framework?

**Definition:**
> Spring is a comprehensive framework for building enterprise Java applications, providing infrastructure support so you can focus on business logic.

**Simple meaning:**
Spring handles the plumbing (object creation, configuration, transactions) so you write business code.

**Core Features:**
- **Dependency Injection (DI)** - Automatic object creation and wiring
- **Aspect-Oriented Programming (AOP)** - Cross-cutting concerns
- **Transaction Management** - Declarative transactions
- **Data Access** - Simplified database operations
- **Security** - Authentication and authorization
- **REST APIs** - Easy REST endpoint creation

**Real-life analogy:**
Spring is like a smart assistant - you tell it what you need (dependencies), and it prepares everything for you automatically.

---

### Dependency Injection (DI)

**Definition:**
> DI is a design pattern where objects receive their dependencies from external source rather than creating them.

**Simple meaning:**
Spring creates and injects objects for you - no need for 'new' keyword.

**Without DI:**
```java
// ❌ Tight coupling
public class UserService {
    private UserRepository repo = new UserRepository();  // Hard-coded
}
```

**With DI:**
```java
// ✅ Loose coupling
@Service
public class UserService {
    private final UserRepository repo;
    
    // Constructor injection (recommended)
    public UserService(UserRepository repo) {
        this.repo = repo;
    }
}
```

---

### Types of Dependency Injection

**1. Constructor Injection (Recommended):**
```java
@Service
public class UserService {
    private final UserRepository repo;
    
    @Autowired  // Optional in Spring 4.3+
    public UserService(UserRepository repo) {
        this.repo = repo;
    }
}
```

**2. Setter Injection:**
```java
@Service
public class UserService {
    private UserRepository repo;
    
    @Autowired
    public void setRepo(UserRepository repo) {
        this.repo = repo;
    }
}
```

**3. Field Injection (Not recommended):**
```java
@Service
public class UserService {
    @Autowired
    private UserRepository repo;  // Hard to test
}
```

**Interview Tip:**
> "DI inverts control - Spring creates and injects dependencies. Three types: constructor (best - immutable, testable), setter (optional dependencies), field (avoid - hard to test). Use @Autowired or rely on constructor."

---

### Spring Bean Lifecycle

**Lifecycle:**
```
Instantiation → Populate Properties → setBeanName → setBeanFactory 
→ setApplicationContext → @PostConstruct → Bean Ready → @PreDestroy → Destroy
```

**Lifecycle Annotations:**
```java
@Component
public class MyBean {
    
    @PostConstruct
    public void init() {
        System.out.println("Bean initialized");
        // Initialization logic
    }
    
    @PreDestroy
    public void cleanup() {
        System.out.println("Bean destroyed");
        // Cleanup logic
    }
}
```

---

### Bean Scopes

| Scope | Description | Use Case |
|-------|-------------|----------|
| **singleton** | One instance per container (default) | Stateless services |
| **prototype** | New instance each time | Stateful objects |
| **request** | One per HTTP request | Web applications |
| **session** | One per HTTP session | User session data |
| **application** | One per ServletContext | Application-wide data |

```java
@Service
@Scope("prototype")  // New instance each time
public class PrototypeService {
}
```

---

## Spring Boot

### 🎯 What is Spring Boot?

**Definition:**
> Spring Boot is an opinionated framework that simplifies Spring application development with auto-configuration and embedded servers.

**Simple meaning:**
Spring Boot = Spring Framework + Auto-configuration + Embedded Server + Production-ready features

**Why Spring Boot:**
- ✅ No XML configuration
- ✅ Embedded server (Tomcat, Jetty)
- ✅ Auto-configuration
- ✅ Production-ready (metrics, health checks)
- ✅ Starter dependencies
- ✅ Fast development

**Real-life analogy:**
Spring Boot is like a meal kit - everything pre-measured and ready to cook, vs Spring Framework which is buying individual ingredients.

---

### Creating Spring Boot Application

**1. Main Application Class:**

```java
@SpringBootApplication  // = @Configuration + @EnableAutoConfiguration + @ComponentScan
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

---

### REST Controller

```java
@RestController
@RequestMapping("/api/users")
public class UserController {
    
    @Autowired
    private UserService userService;
    
    // GET all users
    @GetMapping
    public List<User> getAllUsers() {
        return userService.findAll();
    }
    
    // GET user by ID
    @GetMapping("/{id}")
    public ResponseEntity<User> getUserById(@PathVariable Long id) {
        User user = userService.findById(id);
        if (user == null) {
            return ResponseEntity.notFound().build();
        }
        return ResponseEntity.ok(user);
    }
    
    // POST create user
    @PostMapping
    public ResponseEntity<User> createUser(@RequestBody @Valid User user) {
        User created = userService.save(user);
        return ResponseEntity.status(HttpStatus.CREATED).body(created);
    }
    
    // PUT update user
    @PutMapping("/{id}")
    public ResponseEntity<User> updateUser(
            @PathVariable Long id, 
            @RequestBody @Valid User user) {
        User updated = userService.update(id, user);
        return ResponseEntity.ok(updated);
    }
    
    // DELETE user
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        userService.delete(id);
        return ResponseEntity.noContent().build();
    }
    
    // Query parameters
    @GetMapping("/search")
    public List<User> searchUsers(
            @RequestParam String name,
            @RequestParam(defaultValue = "0") int page) {
        return userService.search(name, page);
    }
}
```

---

### Request/Response Annotations

| Annotation | Purpose | Example |
|------------|---------|---------|
| `@RestController` | Marks class as REST controller | Class level |
| `@RequestMapping` | Base path for all endpoints | `/api/users` |
| `@GetMapping` | Handle GET requests | `@GetMapping("/{id}")` |
| `@PostMapping` | Handle POST requests | `@PostMapping` |
| `@PutMapping` | Handle PUT requests | `@PutMapping("/{id}")` |
| `@DeleteMapping` | Handle DELETE requests | `@DeleteMapping("/{id}")` |
| `@PathVariable` | Extract from URL path | `/users/{id}` |
| `@RequestParam` | Extract query parameter | `/search?name=john` |
| `@RequestBody` | Parse JSON body | POST/PUT requests |
| `@Valid` | Trigger validation | With @RequestBody |

---

### Exception Handling

**Global Exception Handler:**

```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(
            ResourceNotFoundException ex) {
        ErrorResponse error = new ErrorResponse(
            HttpStatus.NOT_FOUND.value(),
            ex.getMessage(),
            System.currentTimeMillis()
        );
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }
    
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErrorResponse> handleValidation(
            MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error -> 
            errors.put(error.getField(), error.getDefaultMessage())
        );
        
        ErrorResponse error = new ErrorResponse(
            HttpStatus.BAD_REQUEST.value(),
            "Validation failed",
            errors
        );
        return ResponseEntity.badRequest().body(error);
    }
    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneral(Exception ex) {
        ErrorResponse error = new ErrorResponse(
            HttpStatus.INTERNAL_SERVER_ERROR.value(),
            "Internal server error",
            System.currentTimeMillis()
        );
        return ResponseEntity.status(500).body(error);
    }
}

// Custom exception
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}

// Error response DTO
@Data
public class ErrorResponse {
    private int status;
    private String message;
    private Object details;
    private long timestamp;
}
```

**Interview Tip:**
> "@RestControllerAdvice handles exceptions globally. @ExceptionHandler specifies which exception to handle. Returns ResponseEntity with status code and error details. Cleaner than try-catch in every controller."

---

## Spring Data JPA

### 🎯 What is Spring Data JPA?

**Definition:**
> Spring Data JPA simplifies database operations by providing repository interfaces with built-in CRUD methods.

**Simple meaning:**
Write interface, Spring generates implementation automatically.

---

### Entity Class

```java
@Entity
@Table(name = "users")
@Data  // Lombok - generates getters, setters, toString
@NoArgsConstructor
@AllArgsConstructor
public class User {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private String name;
    
    @Column(unique = true, nullable = false)
    private String email;
    
    private Integer age;
    
    @CreationTimestamp
    private LocalDateTime createdAt;
    
    @UpdateTimestamp
    private LocalDateTime updatedAt;
    
    // Relationships
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Order> orders;
}
```

---

### JPA Annotations

| Annotation | Purpose |
|------------|---------|
| `@Entity` | Mark class as JPA entity |
| `@Table` | Specify table name |
| `@Id` | Primary key |
| `@GeneratedValue` | Auto-generate ID |
| `@Column` | Column properties |
| `@OneToOne` | One-to-one relationship |
| `@OneToMany` | One-to-many relationship |
| `@ManyToOne` | Many-to-one relationship |
| `@ManyToMany` | Many-to-many relationship |
| `@JoinColumn` | Foreign key column |
| `@Transient` | Don't persist field |

---

### Repository Interface

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    
    // Spring generates implementation automatically!
    
    // Derived query methods (Spring parses method name)
    List<User> findByName(String name);
    List<User> findByEmail(String email);
    List<User> findByAgeGreaterThan(Integer age);
    List<User> findByNameAndEmail(String name, String email);
    List<User> findByNameContaining(String keyword);
    List<User> findByOrderByNameAsc();
    
    // @Query annotation (JPQL)
    @Query("SELECT u FROM User u WHERE u.age > :age")
    List<User> findUsersOlderThan(@Param("age") Integer age);
    
    // Native SQL query
    @Query(value = "SELECT * FROM users WHERE age > ?1", nativeQuery = true)
    List<User> findUsersOlderThanNative(Integer age);
    
    // Update query
    @Modifying
    @Transactional
    @Query("UPDATE User u SET u.age = :age WHERE u.id = :id")
    int updateAge(@Param("id") Long id, @Param("age") Integer age);
    
    // Delete query
    @Modifying
    @Transactional
    @Query("DELETE FROM User u WHERE u.age < :age")
    int deleteUsersYoungerThan(@Param("age") Integer age);
}
```

---

### Service Layer

```java
@Service
@Transactional  // All methods run in transaction
public class UserService {
    
    private final UserRepository userRepository;
    
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    
    public List<User> findAll() {
        return userRepository.findAll();
    }
    
    public User findById(Long id) {
        return userRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("User not found"));
    }
    
    public User save(User user) {
        return userRepository.save(user);
    }
    
    public User update(Long id, User userDetails) {
        User user = findById(id);
        user.setName(userDetails.getName());
        user.setEmail(userDetails.getEmail());
        user.setAge(userDetails.getAge());
        return userRepository.save(user);
    }
    
    public void delete(Long id) {
        User user = findById(id);
        userRepository.delete(user);
    }
    
    // Custom business logic
    public List<User> findAdults() {
        return userRepository.findByAgeGreaterThan(18);
    }
}
```

**Interview Tip:**
> "Spring Data JPA: Create interface extending JpaRepository, Spring generates implementation. Derived queries from method names (findByName). @Query for custom JPQL. @Transactional for transaction management."

---

### JPA Relationships

**One-to-Many:**
```java
// Parent
@Entity
public class User {
    @Id
    @GeneratedValue
    private Long id;
    
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Order> orders = new ArrayList<>();
}

// Child
@Entity
public class Order {
    @Id
    @GeneratedValue
    private Long id;
    
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id")
    private User user;
}
```

**Many-to-Many:**
```java
@Entity
public class Student {
    @Id
    @GeneratedValue
    private Long id;
    
    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses = new HashSet<>();
}

@Entity
public class Course {
    @Id
    @GeneratedValue
    private Long id;
    
    @ManyToMany(mappedBy = "courses")
    private Set<Student> students = new HashSet<>();
}
```

---

### Fetch Types

| Type | Behavior | Use When |
|------|----------|----------|
| **EAGER** | Load immediately | Small related data |
| **LAZY** | Load on access | Large related data |

```java
@ManyToOne(fetch = FetchType.LAZY)  // Default for @ManyToOne
private User user;

@OneToMany(fetch = FetchType.LAZY)  // Default for @OneToMany
private List<Order> orders;
```

**N+1 Problem:**
```java
// ❌ Bad - N+1 queries
List<User> users = userRepository.findAll();  // 1 query
for (User user : users) {
    user.getOrders().size();  // N queries (one per user)
}

// ✅ Good - Single query with JOIN FETCH
@Query("SELECT u FROM User u LEFT JOIN FETCH u.orders")
List<User> findAllWithOrders();
```

---

## Spring AOP (Aspect-Oriented Programming)

### 🎯 What is AOP?

**Definition:**
> AOP separates cross-cutting concerns (logging, security, transactions) from business logic.

**Simple meaning:**
Add functionality to methods without modifying their code.

**Key Concepts:**
- **Aspect** - Module containing cross-cutting concern
- **Join Point** - Point in execution (method call)
- **Advice** - Action taken (before, after, around)
- **Pointcut** - Expression matching join points

**Real-life analogy:**
AOP is like airport security - every passenger (method) goes through security (aspect) without security code in each flight.

---

### AOP Advice Types

**1. @Before - Execute before method:**
```java
@Aspect
@Component
public class LoggingAspect {
    
    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("Executing: " + joinPoint.getSignature().getName());
    }
}
```

**2. @After - Execute after method:**
```java
@After("execution(* com.example.service.*.*(..))")
public void logAfter(JoinPoint joinPoint) {
    System.out.println("Completed: " + joinPoint.getSignature().getName());
}
```

**3. @AfterReturning - Execute after successful return:**
```java
@AfterReturning(
    pointcut = "execution(* com.example.service.*.*(..))",
    returning = "result"
)
public void logAfterReturning(JoinPoint joinPoint, Object result) {
    System.out.println("Method returned: " + result);
}
```

**4. @AfterThrowing - Execute after exception:**
```java
@AfterThrowing(
    pointcut = "execution(* com.example.service.*.*(..))",
    throwing = "error"
)
public void logAfterThrowing(JoinPoint joinPoint, Throwable error) {
    System.out.println("Exception: " + error.getMessage());
}
```

**5. @Around - Execute around method (most powerful):**
```java
@Around("execution(* com.example.service.*.*(..))")
public Object logAround(ProceedingJoinPoint joinPoint) throws Throwable {
    long start = System.currentTimeMillis();
    
    System.out.println("Before method: " + joinPoint.getSignature().getName());
    
    Object result = joinPoint.proceed();  // Execute actual method
    
    long duration = System.currentTimeMillis() - start;
    System.out.println("After method. Duration: " + duration + "ms");
    
    return result;
}
```

---

### Pointcut Expressions

```java
@Aspect
@Component
public class MyAspect {
    
    // All methods in service package
    @Pointcut("execution(* com.example.service.*.*(..))")
    public void serviceMethods() {}
    
    // All methods starting with 'get'
    @Pointcut("execution(* get*(..))")
    public void getterMethods() {}
    
    // Methods with @Transactional annotation
    @Pointcut("@annotation(org.springframework.transaction.annotation.Transactional)")
    public void transactionalMethods() {}
    
    // Combine pointcuts
    @Before("serviceMethods() && getterMethods()")
    public void beforeServiceGetters() {
        // Execute for service getter methods
    }
}
```

**Interview Tip:**
> "AOP separates cross-cutting concerns. Advice types: @Before (before method), @After (after method), @Around (wrap method). Pointcut defines where to apply. Use for logging, security, transactions, performance monitoring."

---

### Practical AOP Examples

**Logging Aspect:**
```java
@Aspect
@Component
@Slf4j
public class LoggingAspect {
    
    @Around("@annotation(com.example.annotation.Loggable)")
    public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        
        Object result = joinPoint.proceed();
        
        long duration = System.currentTimeMillis() - start;
        log.info("{} executed in {}ms", 
            joinPoint.getSignature().getName(), duration);
        
        return result;
    }
}

// Custom annotation
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Loggable {
}

// Usage
@Service
public class UserService {
    @Loggable
    public User findById(Long id) {
        // Method automatically logged
    }
}
```

---

## Spring Security

### 🎯 What is Spring Security?

**Definition:**
> Spring Security provides authentication and authorization for Spring applications.

**Simple meaning:**
Handles who can access what in your application.

**Core Concepts:**
- **Authentication** - Who are you? (Login)
- **Authorization** - What can you do? (Permissions)
- **Principal** - Currently logged-in user
- **GrantedAuthority** - User's permissions/roles

---

### Basic Security Configuration

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf().disable()  // Disable for REST APIs
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/public/**").permitAll()
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated()
            )
            .sessionManagement()
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS);  // For JWT
        
        return http.build();
    }
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

---

### JWT Authentication

**JWT Filter:**

```java
@Component
public class JwtAuthenticationFilter extends OncePerRequestFilter {
    
    @Autowired
    private JwtTokenProvider tokenProvider;
    
    @Autowired
    private UserDetailsService userDetailsService;
    
    @Override
    protected void doFilterInternal(
            HttpServletRequest request,
            HttpServletResponse response,
            FilterChain filterChain) throws ServletException, IOException {
        
        try {
            String jwt = getJwtFromRequest(request);
            
            if (jwt != null && tokenProvider.validateToken(jwt)) {
                String username = tokenProvider.getUsernameFromToken(jwt);
                
                UserDetails userDetails = userDetailsService.loadUserByUsername(username);
                
                UsernamePasswordAuthenticationToken authentication = 
                    new UsernamePasswordAuthenticationToken(
                        userDetails, null, userDetails.getAuthorities()
                    );
                
                SecurityContextHolder.getContext().setAuthentication(authentication);
            }
        } catch (Exception ex) {
            logger.error("Could not set user authentication", ex);
        }
        
        filterChain.doFilter(request, response);
    }
    
    private String getJwtFromRequest(HttpServletRequest request) {
        String bearerToken = request.getHeader("Authorization");
        if (bearerToken != null && bearerToken.startsWith("Bearer ")) {
            return bearerToken.substring(7);
        }
        return null;
    }
}
```

---

### JWT Token Provider

```java
@Component
public class JwtTokenProvider {
    
    @Value("${jwt.secret}")
    private String jwtSecret;
    
    @Value("${jwt.expiration}")
    private long jwtExpiration;
    
    public String generateToken(Authentication authentication) {
        UserDetails userDetails = (UserDetails) authentication.getPrincipal();
        
        Date now = new Date();
        Date expiryDate = new Date(now.getTime() + jwtExpiration);
        
        return Jwts.builder()
            .setSubject(userDetails.getUsername())
            .setIssuedAt(now)
            .setExpiration(expiryDate)
            .signWith(SignatureAlgorithm.HS512, jwtSecret)
            .compact();
    }
    
    public String getUsernameFromToken(String token) {
        Claims claims = Jwts.parser()
            .setSigningKey(jwtSecret)
            .parseClaimsJws(token)
            .getBody();
        
        return claims.getSubject();
    }
    
    public boolean validateToken(String token) {
        try {
            Jwts.parser().setSigningKey(jwtSecret).parseClaimsJws(token);
            return true;
        } catch (Exception ex) {
            return false;
        }
    }
}
```

---

### UserDetailsService Implementation

```java
@Service
public class CustomUserDetailsService implements UserDetailsService {
    
    @Autowired
    private UserRepository userRepository;
    
    @Override
    public UserDetails loadUserByUsername(String username) 
            throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username)
            .orElseThrow(() -> 
                new UsernameNotFoundException("User not found: " + username));
        
        return org.springframework.security.core.userdetails.User
            .builder()
            .username(user.getUsername())
            .password(user.getPassword())
            .roles(user.getRoles().toArray(new String[0]))
            .build();
    }
}
```

---

### Authentication Controller

```java
@RestController
@RequestMapping("/api/auth")
public class AuthController {
    
    @Autowired
    private AuthenticationManager authenticationManager;
    
    @Autowired
    private JwtTokenProvider tokenProvider;
    
    @Autowired
    private UserRepository userRepository;
    
    @Autowired
    private PasswordEncoder passwordEncoder;
    
    @PostMapping("/register")
    public ResponseEntity<?> register(@RequestBody @Valid SignUpRequest request) {
        if (userRepository.existsByUsername(request.getUsername())) {
            return ResponseEntity.badRequest()
                .body("Username already exists");
        }
        
        User user = new User();
        user.setUsername(request.getUsername());
        user.setEmail(request.getEmail());
        user.setPassword(passwordEncoder.encode(request.getPassword()));
        user.setRoles(Set.of("USER"));
        
        userRepository.save(user);
        
        return ResponseEntity.ok("User registered successfully");
    }
    
    @PostMapping("/login")
    public ResponseEntity<?> login(@RequestBody @Valid LoginRequest request) {
        Authentication authentication = authenticationManager.authenticate(
            new UsernamePasswordAuthenticationToken(
                request.getUsername(),
                request.getPassword()
            )
        );
        
        SecurityContextHolder.getContext().setAuthentication(authentication);
        
        String jwt = tokenProvider.generateToken(authentication);
        
        return ResponseEntity.ok(new JwtAuthenticationResponse(jwt));
    }
}
```

**Interview Tip:**
> "Spring Security: Configure with SecurityFilterChain. JWT filter validates token, sets SecurityContext. UserDetailsService loads user. AuthenticationManager authenticates credentials. Use @PreAuthorize for method-level security."

---

## Spring Boot Internals

### 🎯 How Auto-Configuration Works

**Definition:**
> Spring Boot auto-configures beans based on classpath, properties, and existing beans.

**How it works:**
1. `@SpringBootApplication` triggers auto-configuration
2. Scans `META-INF/spring.factories` in JARs
3. Conditional annotations determine what to configure
4. Creates beans automatically

**Conditional Annotations:**

```java
@Configuration
@ConditionalOnClass(DataSource.class)  // Only if DataSource on classpath
public class DataSourceAutoConfiguration {
    
    @Bean
    @ConditionalOnMissingBean  // Only if no DataSource bean exists
    public DataSource dataSource() {
        return new HikariDataSource();
    }
}
```

**Common Conditionals:**
- `@ConditionalOnClass` - If class present
- `@ConditionalOnMissingBean` - If bean not defined
- `@ConditionalOnProperty` - If property set
- `@ConditionalOnWebApplication` - If web app

---

### Application Properties

**application.properties:**
```properties
# Server
server.port=8080
server.servlet.context-path=/api

# Database
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# Logging
logging.level.root=INFO
logging.level.com.example=DEBUG

# JWT
jwt.secret=mySecretKey
jwt.expiration=86400000
```

**application.yml (alternative):**
```yaml
server:
  port: 8080
  servlet:
    context-path: /api

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: password
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
```

---

## Scheduling & Cron Jobs

### 🎯 Task Scheduling

**Enable Scheduling:**
```java
@SpringBootApplication
@EnableScheduling
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

---

### Scheduled Tasks

```java
@Component
public class ScheduledTasks {
    
    private static final Logger log = LoggerFactory.getLogger(ScheduledTasks.class);
    
    // Fixed rate - executes every 5 seconds
    @Scheduled(fixedRate = 5000)
    public void taskWithFixedRate() {
        log.info("Fixed rate task - {}", System.currentTimeMillis());
    }
    
    // Fixed delay - waits 5 seconds after previous execution completes
    @Scheduled(fixedDelay = 5000)
    public void taskWithFixedDelay() {
        log.info("Fixed delay task - {}", System.currentTimeMillis());
    }
    
    // Initial delay - waits 10 seconds before first execution
    @Scheduled(initialDelay = 10000, fixedRate = 5000)
    public void taskWithInitialDelay() {
        log.info("Task with initial delay");
    }
    
    // Cron expression - runs at specific times
    @Scheduled(cron = "0 0 9 * * MON-FRI")  // 9 AM, Monday to Friday
    public void taskWithCronExpression() {
        log.info("Cron task executed");
    }
}
```

---

### Cron Expression Format

```
┌───────────── second (0-59)
│ ┌───────────── minute (0-59)
│ │ ┌───────────── hour (0-23)
│ │ │ ┌───────────── day of month (1-31)
│ │ │ │ ┌───────────── month (1-12 or JAN-DEC)
│ │ │ │ │ ┌───────────── day of week (0-7 or SUN-SAT)
│ │ │ │ │ │
* * * * * *
```

**Common Cron Examples:**

| Expression | Meaning |
|------------|---------|
| `0 0 * * * *` | Every hour |
| `0 */15 * * * *` | Every 15 minutes |
| `0 0 9 * * *` | Every day at 9 AM |
| `0 0 9 * * MON-FRI` | Weekdays at 9 AM |
| `0 0 0 1 * *` | First day of month |
| `0 0 12 * * SUN` | Every Sunday at noon |

---

### Async Scheduling

```java
@Configuration
@EnableAsync
public class AsyncConfig {
    
    @Bean
    public TaskExecutor taskExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(5);
        executor.setMaxPoolSize(10);
        executor.setQueueCapacity(25);
        executor.setThreadNamePrefix("async-");
        executor.initialize();
        return executor;
    }
}

@Service
public class AsyncService {
    
    @Async
    @Scheduled(fixedRate = 10000)
    public void asyncScheduledTask() {
        // Runs asynchronously in separate thread
        log.info("Async task on thread: {}", Thread.currentThread().getName());
    }
    
    @Async
    public CompletableFuture<String> processAsync() {
        // Long-running task
        return CompletableFuture.completedFuture("Result");
    }
}
```

**Interview Tip:**
> "@Scheduled for periodic tasks. fixedRate (every N ms), fixedDelay (N ms after completion), cron (specific times). @EnableScheduling to activate. @Async for async execution with thread pool."

---

## Spring Boot Actuator

### 🎯 Production-Ready Features

**Add dependency:**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

**Configuration:**
```properties
# Expose all endpoints
management.endpoints.web.exposure.include=*

# Or specific endpoints
management.endpoints.web.exposure.include=health,info,metrics

# Custom info
info.app.name=My Application
info.app.version=1.0.0
```

**Useful Endpoints:**

| Endpoint | Purpose |
|----------|---------|
| `/actuator/health` | Application health status |
| `/actuator/info` | Application information |
| `/actuator/metrics` | Application metrics |
| `/actuator/env` | Environment properties |
| `/actuator/loggers` | Logging configuration |
| `/actuator/beans` | All Spring beans |

**Custom Health Indicator:**

```java
@Component
public class CustomHealthIndicator implements HealthIndicator {
    
    @Override
    public Health health() {
        // Check custom health logic
        boolean isHealthy = checkDatabaseConnection();
        
        if (isHealthy) {
            return Health.up()
                .withDetail("database", "Available")
                .build();
        }
        
        return Health.down()
            .withDetail("database", "Unavailable")
            .build();
    }
    
    private boolean checkDatabaseConnection() {
        // Check database
        return true;
    }
}
```

---

## Spring Validation

### 🎯 Bean Validation

**Entity with Validation:**

```java
@Entity
public class User {
    
    @Id
    @GeneratedValue
    private Long id;
    
    @NotBlank(message = "Name is required")
    @Size(min = 2, max = 50, message = "Name must be between 2 and 50 characters")
    private String name;
    
    @NotBlank(message = "Email is required")
    @Email(message = "Email should be valid")
    private String email;
    
    @Min(value = 18, message = "Age must be at least 18")
    @Max(value = 150, message = "Age must be less than 150")
    private Integer age;
    
    @Pattern(regexp = "^\\+?[1-9]\\d{1,14}$", message = "Invalid phone number")
    private String phone;
}
```

**Common Validation Annotations:**

| Annotation | Purpose |
|------------|---------|
| `@NotNull` | Value must not be null |
| `@NotEmpty` | String/Collection not empty |
| `@NotBlank` | String not null/empty/whitespace |
| `@Size` | String/Collection size |
| `@Min` / `@Max` | Number range |
| `@Email` | Valid email format |
| `@Pattern` | Regex pattern |
| `@Past` / `@Future` | Date validation |

**Custom Validator:**

```java
// Custom annotation
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
@Constraint(validatedBy = AgeValidator.class)
public @interface ValidAge {
    String message() default "Invalid age";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}

// Validator implementation
public class AgeValidator implements ConstraintValidator<ValidAge, Integer> {
    
    @Override
    public boolean isValid(Integer age, ConstraintValidatorContext context) {
        return age != null && age >= 18 && age <= 150;
    }
}

// Usage
@ValidAge
private Integer age;
```

---

## Spring Transactions

### 🎯 Transaction Management

**Definition:**
> @Transactional ensures methods execute within a database transaction (all or nothing).

```java
@Service
@Transactional  // Class-level - all methods transactional
public class OrderService {
    
    @Autowired
    private OrderRepository orderRepository;
    
    @Autowired
    private InventoryService inventoryService;
    
    @Autowired
    private PaymentService paymentService;
    
    public Order createOrder(OrderRequest request) {
        // All operations in single transaction
        Order order = new Order();
        order.setItems(request.getItems());
        order.setTotal(calculateTotal(request));
        
        // Save order
        order = orderRepository.save(order);
        
        // Update inventory
        inventoryService.reduceStock(request.getItems());
        
        // Process payment
        paymentService.charge(order.getTotal());
        
        // If any operation fails, entire transaction rolls back
        return order;
    }
    
    @Transactional(readOnly = true)  // Optimization for read-only
    public List<Order> findAll() {
        return orderRepository.findAll();
    }
    
    @Transactional(
        propagation = Propagation.REQUIRES_NEW,  // New transaction
        isolation = Isolation.READ_COMMITTED,
        timeout = 30,  // 30 seconds
        rollbackFor = Exception.class
    )
    public void complexOperation() {
        // Complex transactional logic
    }
}
```

---

### Transaction Propagation

| Type | Behavior |
|------|----------|
| **REQUIRED** | Use existing or create new (default) |
| **REQUIRES_NEW** | Always create new transaction |
| **SUPPORTS** | Use existing if present, non-transactional otherwise |
| **NOT_SUPPORTED** | Execute non-transactionally |
| **MANDATORY** | Must have existing transaction |
| **NEVER** | Must not have transaction |

---

### How @Transactional Works Internally

**Mechanism:**
1. Spring creates proxy around bean
2. Proxy intercepts method calls
3. Begins transaction before method
4. Commits if successful, rolls back if exception
5. Uses AOP under the hood

**Important:**
- Only works on public methods
- Only works when called from outside class
- Self-invocation doesn't trigger transaction

```java
@Service
public class UserService {
    
    @Transactional
    public void method1() {
        method2();  // ❌ Transaction not applied (self-invocation)
    }
    
    @Transactional
    public void method2() {
        // Logic
    }
}
```

**Interview Tip:**
> "@Transactional manages database transactions. Propagation controls transaction behavior (REQUIRED, REQUIRES_NEW). Isolation controls concurrency (READ_COMMITTED). Works via AOP proxy. Self-invocation doesn't trigger transaction."

---

## Spring Profiles

### 🎯 Environment-Specific Configuration

**Definition:**
> Profiles allow different configurations for different environments (dev, test, prod).

**application-dev.properties:**
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb_dev
logging.level.root=DEBUG
```

**application-prod.properties:**
```properties
spring.datasource.url=jdbc:mysql://prod-server:3306/mydb_prod
logging.level.root=WARN
```

**Activate profile:**
```bash
# Command line
java -jar app.jar --spring.profiles.active=prod

# application.properties
spring.profiles.active=dev
```

**Profile-specific beans:**
```java
@Configuration
@Profile("dev")
public class DevConfig {
    @Bean
    public DataSource devDataSource() {
        // Development database
    }
}

@Configuration
@Profile("prod")
public class ProdConfig {
    @Bean
    public DataSource prodDataSource() {
        // Production database
    }
}
```

---

## Spring Boot Testing

### 🎯 Testing REST APIs

```java
@SpringBootTest
@AutoConfigureMockMvc
class UserControllerTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @Autowired
    private ObjectMapper objectMapper;
    
    @MockBean
    private UserService userService;
    
    @Test
    void shouldGetAllUsers() throws Exception {
        List<User> users = Arrays.asList(
            new User(1L, "John", "john@example.com"),
            new User(2L, "Jane", "jane@example.com")
        );
        
        when(userService.findAll()).thenReturn(users);
        
        mockMvc.perform(get("/api/users"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$", hasSize(2)))
            .andExpect(jsonPath("$[0].name").value("John"));
    }
    
    @Test
    void shouldCreateUser() throws Exception {
        User user = new User(null, "John", "john@example.com");
        User saved = new User(1L, "John", "john@example.com");
        
        when(userService.save(any(User.class))).thenReturn(saved);
        
        mockMvc.perform(post("/api/users")
                .contentType(MediaType.APPLICATION_JSON)
                .content(objectMapper.writeValueAsString(user)))
            .andExpect(status().isCreated())
            .andExpect(jsonPath("$.id").value(1))
            .andExpect(jsonPath("$.name").value("John"));
    }
}
```

---

### Repository Testing

```java
@DataJpaTest  // Only loads JPA components
class UserRepositoryTest {
    
    @Autowired
    private UserRepository userRepository;
    
    @Autowired
    private TestEntityManager entityManager;
    
    @Test
    void shouldFindUserByEmail() {
        // Given
        User user = new User();
        user.setName("John");
        user.setEmail("john@example.com");
        entityManager.persist(user);
        entityManager.flush();
        
        // When
        User found = userRepository.findByEmail("john@example.com");
        
        // Then
        assertThat(found.getName()).isEqualTo("John");
    }
}
```

---

## Spring Interview Questions

### Core Spring

**1. What is Spring Framework?**
> "Spring is enterprise Java framework providing DI, AOP, transaction management, data access. Reduces boilerplate, promotes loose coupling. Spring Boot adds auto-configuration and embedded server."

**2. Explain Dependency Injection.**
> "DI is pattern where Spring creates and injects dependencies instead of objects creating them. Three types: constructor (best), setter, field. Promotes loose coupling and testability."

**3. What is Spring Bean?**
> "Bean is object managed by Spring container. Created, configured, and managed by Spring. Defined with @Component, @Service, @Repository, @Controller annotations or @Bean method."

**4. Difference between @Component, @Service, @Repository?**
> "@Component is generic stereotype. @Service for business logic. @Repository for data access (adds exception translation). @Controller for web layer. All are @Component specializations."

**5. What is @SpringBootApplication?**
> "Combines three annotations: @Configuration (Java config), @EnableAutoConfiguration (auto-config), @ComponentScan (scan components). Entry point for Spring Boot application."

---

### Spring Data JPA

**6. What is Spring Data JPA?**
> "Spring Data JPA simplifies data access. Create interface extending JpaRepository, Spring generates implementation. Provides CRUD methods, derived queries, @Query for custom queries."

**7. Explain N+1 problem and solution.**
> "N+1: One query fetches entities, N queries fetch relationships. Solution: Use JOIN FETCH in @Query, @EntityGraph, or set fetch to EAGER (carefully). Example: SELECT u FROM User u JOIN FETCH u.orders."

**8. Difference between EAGER and LAZY loading?**
> "EAGER loads related entities immediately (default for @ManyToOne). LAZY loads on access (default for @OneToMany). Use LAZY for performance, EAGER for small related data. Beware LazyInitializationException."

---

### Spring Security

**9. How does Spring Security work?**
> "Spring Security uses filter chain to intercept requests. Filters check authentication (who you are) and authorization (what you can do). SecurityContext holds authenticated user. Common: JWT filter validates token, sets SecurityContext."

**10. Explain JWT authentication flow.**
> "User logs in → credentials verified → JWT token generated → token sent to client → client includes token in Authorization header → filter validates token → sets SecurityContext → request proceeds."

---

### Spring Boot

**11. How does auto-configuration work?**
> "Spring Boot scans classpath and existing beans, conditionally creates beans. Uses @ConditionalOnClass, @ConditionalOnMissingBean. Configured in META-INF/spring.factories. Can override with custom beans."

**12. What is @Transactional?**
> "@Transactional manages database transactions. Begins transaction before method, commits if successful, rolls back on exception. Propagation controls behavior (REQUIRED, REQUIRES_NEW). Works via AOP proxy."

---

### AOP & Scheduling

**13. What is AOP in Spring?**
> "AOP separates cross-cutting concerns (logging, security, transactions). Aspect contains advice (code to execute). Pointcut defines where to apply. Advice types: @Before, @After, @Around. Uses proxies."

**14. Explain @Scheduled annotation.**
> "@Scheduled for periodic tasks. fixedRate (every N ms), fixedDelay (N ms after completion), cron (specific times). Requires @EnableScheduling. Runs in thread pool."

---

## 🎯 Spring Boot Project Structure

```
src/
├── main/
│   ├── java/
│   │   └── com/
│   │       └── example/
│   │           ├── MyApplication.java
│   │           ├── config/
│   │           │   ├── SecurityConfig.java
│   │           │   └── AsyncConfig.java
│   │           ├── controller/
│   │           │   └── UserController.java
│   │           ├── service/
│   │           │   ├── UserService.java
│   │           │   └── impl/
│   │           │       └── UserServiceImpl.java
│   │           ├── repository/
│   │           │   └── UserRepository.java
│   │           ├── model/
│   │           │   └── User.java
│   │           ├── dto/
│   │           │   ├── UserRequest.java
│   │           │   └── UserResponse.java
│   │           ├── exception/
│   │           │   ├── ResourceNotFoundException.java
│   │           │   └── GlobalExceptionHandler.java
│   │           ├── security/
│   │           │   ├── JwtAuthenticationFilter.java
│   │           │   └── JwtTokenProvider.java
│   │           └── aspect/
│   │               └── LoggingAspect.java
│   └── resources/
│       ├── application.properties
│       ├── application-dev.properties
│       └── application-prod.properties
└── test/
    └── java/
        └── com/
            └── example/
                ├── controller/
                │   └── UserControllerTest.java
                └── service/
                    └── UserServiceTest.java
```

---

## 🚀 Spring Boot Best Practices

### ✅ Do's:

- Use constructor injection (not field injection)
- Use DTOs for API requests/responses (not entities)
- Implement global exception handling
- Use @Transactional on service layer
- Enable validation with @Valid
- Use profiles for different environments
- Implement proper logging
- Use Actuator for monitoring
- Write tests for controllers and services
- Use Lombok to reduce boilerplate

### ❌ Don'ts:

- Don't use field injection (@Autowired on fields)
- Don't expose entities directly in REST APIs
- Don't ignore exception handling
- Don't use @Transactional on repository methods
- Don't hardcode values (use application.properties)
- Don't commit secrets to git
- Don't use synchronous calls for external APIs
- Don't ignore security
- Don't skip input validation

---

## 🎯 Complete REST API Example

```java
// Entity
@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @NotBlank
    private String name;
    
    @Min(0)
    private Double price;
    
    private Integer stock;
}

// Repository
@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    List<Product> findByNameContaining(String name);
    List<Product> findByPriceBetween(Double min, Double max);
}

// Service
@Service
@Transactional
public class ProductService {
    private final ProductRepository repository;
    
    public ProductService(ProductRepository repository) {
        this.repository = repository;
    }
    
    @Transactional(readOnly = true)
    public List<Product> findAll() {
        return repository.findAll();
    }
    
    @Transactional(readOnly = true)
    public Product findById(Long id) {
        return repository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("Product not found"));
    }
    
    public Product save(Product product) {
        return repository.save(product);
    }
    
    public void delete(Long id) {
        Product product = findById(id);
        repository.delete(product);
    }
}

// Controller
@RestController
@RequestMapping("/api/products")
public class ProductController {
    private final ProductService service;
    
    public ProductController(ProductService service) {
        this.service = service;
    }
    
    @GetMapping
    public ResponseEntity<List<Product>> getAll() {
        return ResponseEntity.ok(service.findAll());
    }
    
    @GetMapping("/{id}")
    public ResponseEntity<Product> getById(@PathVariable Long id) {
        return ResponseEntity.ok(service.findById(id));
    }
    
    @PostMapping
    public ResponseEntity<Product> create(@RequestBody @Valid Product product) {
        Product created = service.save(product);
        return ResponseEntity.status(HttpStatus.CREATED).body(created);
    }
    
    @PutMapping("/{id}")
    public ResponseEntity<Product> update(
            @PathVariable Long id,
            @RequestBody @Valid Product product) {
        product.setId(id);
        return ResponseEntity.ok(service.save(product));
    }
    
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> delete(@PathVariable Long id) {
        service.delete(id);
        return ResponseEntity.noContent().build();
    }
}
```

---

## 🎓 Spring Framework Summary

### Key Concepts:

**Spring Core:**
1. **Dependency Injection** - Spring manages object creation
2. **IoC Container** - Creates and manages beans
3. **Bean Scopes** - Singleton (default), prototype, request, session
4. **Lifecycle** - @PostConstruct, @PreDestroy

**Spring Boot:**
1. **Auto-configuration** - Automatic bean creation
2. **Starter Dependencies** - Pre-configured dependencies
3. **Embedded Server** - No external Tomcat needed
4. **Actuator** - Production monitoring

**Spring Data JPA:**
1. **Repository Pattern** - Interface with auto-implementation
2. **Derived Queries** - Method name → SQL
3. **@Query** - Custom JPQL/SQL
4. **Relationships** - @OneToMany, @ManyToOne, @ManyToMany
5. **Fetch Types** - LAZY (default), EAGER

**Spring Security:**
1. **Filter Chain** - Intercepts requests
2. **Authentication** - Verify identity
3. **Authorization** - Check permissions
4. **JWT** - Stateless authentication

**Spring AOP:**
1. **Aspects** - Cross-cutting concerns
2. **Advice** - @Before, @After, @Around
3. **Pointcut** - Where to apply
4. **Use Cases** - Logging, security, transactions

**Scheduling:**
1. **@Scheduled** - Periodic tasks
2. **fixedRate** - Every N ms
3. **fixedDelay** - N ms after completion
4. **cron** - Specific times

**Remember:**
> "Spring simplifies enterprise Java. Master DI, understand auto-configuration, use JPA for data access, secure with Spring Security, schedule tasks with @Scheduled."

---

# 📕 LEVEL 9: ANNOTATIONS

## How Annotations Work

### 🎯 What are Annotations?

**Definition:**
> Annotations are metadata that provide information about code to the compiler, runtime, or frameworks.

**Simple meaning:**
Annotations are like labels or sticky notes on code that give instructions to Java or frameworks.

**Real-life analogy:**
Annotations are like tags on luggage - they tell handlers (compiler/framework) how to process the item (code) without changing the item itself.

---

### Annotation Basics

**Built-in Annotations:**

```java
// 1. @Override - Indicates method overrides parent
@Override
public String toString() {
    return "Custom toString";
}

// 2. @Deprecated - Marks as outdated
@Deprecated
public void oldMethod() {
    // Don't use this anymore
}

// 3. @SuppressWarnings - Suppresses compiler warnings
@SuppressWarnings("unchecked")
public void method() {
    List list = new ArrayList();  // Raw type warning suppressed
}

// 4. @FunctionalInterface - Marks as functional interface
@FunctionalInterface
public interface Calculator {
    int calculate(int a, int b);
}
```

---

### How Annotations Work Internally

**Processing Time:**

| Type | When Processed | Use Case |
|------|----------------|----------|
| **SOURCE** | Compile time only | Code generation, validation |
| **CLASS** | Compile time + class file | Bytecode manipulation |
| **RUNTIME** | Runtime via reflection | Frameworks (Spring, JPA) |

**Retention Policy:**

```java
@Retention(RetentionPolicy.SOURCE)    // Discarded after compilation
@Retention(RetentionPolicy.CLASS)     // In .class file, not at runtime
@Retention(RetentionPolicy.RUNTIME)   // Available at runtime (most common)
```

**Target:**

```java
@Target(ElementType.TYPE)          // Class, interface, enum
@Target(ElementType.FIELD)         // Field
@Target(ElementType.METHOD)        // Method
@Target(ElementType.PARAMETER)     // Method parameter
@Target(ElementType.CONSTRUCTOR)   // Constructor
@Target(ElementType.LOCAL_VARIABLE)  // Local variable
@Target({ElementType.METHOD, ElementType.FIELD})  // Multiple targets
```

---

### Creating Custom Annotations

**Step 1: Define Annotation**

```java
import java.lang.annotation.*;

@Target(ElementType.METHOD)  // Can be applied to methods
@Retention(RetentionPolicy.RUNTIME)  // Available at runtime
public @interface LogExecutionTime {
    String value() default "";  // Optional parameter
}
```

**Step 2: Process Annotation (Using Reflection)**

```java
public class AnnotationProcessor {
    
    public static void processAnnotations(Object obj) {
        Class<?> clazz = obj.getClass();
        
        // Get all methods
        for (Method method : clazz.getDeclaredMethods()) {
            // Check if method has our annotation
            if (method.isAnnotationPresent(LogExecutionTime.class)) {
                LogExecutionTime annotation = method.getAnnotation(LogExecutionTime.class);
                
                System.out.println("Found @LogExecutionTime on: " + method.getName());
                System.out.println("Value: " + annotation.value());
                
                // Can invoke method, measure time, etc.
                try {
                    long start = System.currentTimeMillis();
                    method.invoke(obj);
                    long duration = System.currentTimeMillis() - start;
                    System.out.println("Execution time: " + duration + "ms");
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

**Step 3: Use Annotation**

```java
public class MyService {
    
    @LogExecutionTime("Processing data")
    public void processData() {
        try {
            Thread.sleep(1000);  // Simulate work
            System.out.println("Data processed");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
    
    public void normalMethod() {
        System.out.println("Normal method");
    }
}

// Test
public class Main {
    public static void main(String[] args) {
        MyService service = new MyService();
        AnnotationProcessor.processAnnotations(service);
    }
}

// Output:
// Found @LogExecutionTime on: processData
// Value: Processing data
// Data processed
// Execution time: 1002ms
```

---

### Complete Custom Annotation Example

**Validation Annotation:**

```java
// 1. Define annotation
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface ValidEmail {
    String message() default "Invalid email format";
    boolean required() default true;
}

// 2. Validator class
public class EmailValidator {
    
    public static boolean validate(Object obj) {
        Class<?> clazz = obj.getClass();
        
        for (Field field : clazz.getDeclaredFields()) {
            if (field.isAnnotationPresent(ValidEmail.class)) {
                ValidEmail annotation = field.getAnnotation(ValidEmail.class);
                
                field.setAccessible(true);
                try {
                    String value = (String) field.get(obj);
                    
                    // Check if required
                    if (annotation.required() && (value == null || value.isEmpty())) {
                        System.out.println(annotation.message() + ": Field is required");
                        return false;
                    }
                    
                    // Validate email format
                    if (value != null && !value.matches("^[A-Za-z0-9+_.-]+@(.+)$")) {
                        System.out.println(annotation.message());
                        return false;
                    }
                } catch (IllegalAccessException e) {
                    e.printStackTrace();
                    return false;
                }
            }
        }
        return true;
    }
}

// 3. Use annotation
public class User {
    private String name;
    
    @ValidEmail(message = "Please provide valid email", required = true)
    private String email;
    
    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }
}

// 4. Test
public class Main {
    public static void main(String[] args) {
        User user1 = new User("John", "john@example.com");
        System.out.println("Valid: " + EmailValidator.validate(user1));  // true
        
        User user2 = new User("Jane", "invalid-email");
        System.out.println("Valid: " + EmailValidator.validate(user2));  // false
        
        User user3 = new User("Bob", null);
        System.out.println("Valid: " + EmailValidator.validate(user3));  // false
    }
}
```

---

### How Spring Processes Annotations

**Spring's Annotation Processing:**

1. **Component Scanning** - Spring scans packages for @Component, @Service, etc.
2. **Bean Creation** - Creates instances of annotated classes
3. **Dependency Injection** - Resolves @Autowired dependencies
4. **Proxy Creation** - For @Transactional, @Async, AOP
5. **Post-Processing** - Calls @PostConstruct methods

**Example: How @Autowired Works**

```
1. Spring scans classes
2. Finds @Service, @Repository annotations
3. Creates beans and stores in ApplicationContext
4. When creating bean with @Autowired:
   - Looks up dependency by type in ApplicationContext
   - Injects dependency via constructor/setter/field
5. Bean is ready to use
```

**Example: How @Transactional Works**

```
1. Spring creates proxy around @Transactional bean
2. Proxy intercepts method calls
3. Before method: Begin transaction
4. Execute actual method
5. After method: Commit (success) or Rollback (exception)
```

**Interview Tip:**
> "Annotations are metadata processed at compile time or runtime. Custom annotations use @interface. Retention defines lifetime (SOURCE, CLASS, RUNTIME). Target defines where to apply. Process with reflection. Spring uses annotations for component scanning, DI, AOP."

---

### Advanced Custom Annotation

**Method Timing Annotation with AOP:**

```java
// 1. Define annotation
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Timed {
    String operation() default "";
}

// 2. Aspect to process annotation
@Aspect
@Component
@Slf4j
public class TimingAspect {
    
    @Around("@annotation(timed)")
    public Object measureExecutionTime(ProceedingJoinPoint joinPoint, Timed timed) 
            throws Throwable {
        long start = System.currentTimeMillis();
        
        Object result = joinPoint.proceed();
        
        long duration = System.currentTimeMillis() - start;
        
        log.info("Operation '{}' - Method '{}' executed in {}ms",
            timed.operation(),
            joinPoint.getSignature().getName(),
            duration);
        
        return result;
    }
}

// 3. Use annotation
@Service
public class UserService {
    
    @Timed(operation = "Find User")
    public User findById(Long id) {
        // Method automatically timed
        return userRepository.findById(id).orElse(null);
    }
    
    @Timed(operation = "Create User")
    public User save(User user) {
        return userRepository.save(user);
    }
}
```

---

## 🎯 Complete Spring Boot Project

### Project: Task Management API

**Complete working project demonstrating all concepts:**

#### 1. pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project>
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.1.0</version>
    </parent>
    
    <groupId>com.example</groupId>
    <artifactId>task-api</artifactId>
    <version>1.0.0</version>
    
    <dependencies>
        <!-- Spring Boot Web -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <!-- Spring Data JPA -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        
        <!-- Spring Security -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
        
        <!-- Spring Validation -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>
        
        <!-- MySQL Driver -->
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
        </dependency>
        
        <!-- JWT -->
        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt</artifactId>
            <version>0.9.1</version>
        </dependency>
        
        <!-- Lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
        
        <!-- Actuator -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        
        <!-- Testing -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

---

#### 2. Main Application

```java
package com.example.taskapi;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.scheduling.annotation.EnableScheduling;

@SpringBootApplication
@EnableScheduling
public class TaskApiApplication {
    public static void main(String[] args) {
        SpringApplication.run(TaskApiApplication.class, args);
    }
}
```

---

#### 3. Entity Classes

```java
// User.java
@Entity
@Table(name = "users")
@Data
@NoArgsConstructor
@AllArgsConstructor
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(unique = true, nullable = false)
    @NotBlank(message = "Username is required")
    private String username;
    
    @Column(unique = true, nullable = false)
    @Email(message = "Invalid email")
    private String email;
    
    @Column(nullable = false)
    private String password;
    
    @ElementCollection(fetch = FetchType.EAGER)
    private Set<String> roles = new HashSet<>();
    
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Task> tasks = new ArrayList<>();
    
    @CreationTimestamp
    private LocalDateTime createdAt;
}

// Task.java
@Entity
@Table(name = "tasks")
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Task {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @NotBlank(message = "Title is required")
    private String title;
    
    private String description;
    
    @Enumerated(EnumType.STRING)
    private TaskStatus status = TaskStatus.TODO;
    
    @Enumerated(EnumType.STRING)
    private TaskPriority priority = TaskPriority.MEDIUM;
    
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id")
    private User user;
    
    private LocalDateTime dueDate;
    
    @CreationTimestamp
    private LocalDateTime createdAt;
    
    @UpdateTimestamp
    private LocalDateTime updatedAt;
}

// Enums
public enum TaskStatus {
    TODO, IN_PROGRESS, DONE
}

public enum TaskPriority {
    LOW, MEDIUM, HIGH
}
```

---

#### 4. Repository Layer

```java
// UserRepository.java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByUsername(String username);
    Optional<User> findByEmail(String email);
    boolean existsByUsername(String username);
    boolean existsByEmail(String email);
}

// TaskRepository.java
@Repository
public interface TaskRepository extends JpaRepository<Task, Long> {
    List<Task> findByUserId(Long userId);
    List<Task> findByStatus(TaskStatus status);
    List<Task> findByUserIdAndStatus(Long userId, TaskStatus status);
    
    @Query("SELECT t FROM Task t WHERE t.user.id = :userId AND t.dueDate < :date")
    List<Task> findOverdueTasks(@Param("userId") Long userId, @Param("date") LocalDateTime date);
    
    @Query("SELECT t FROM Task t WHERE t.user.id = :userId ORDER BY t.priority DESC, t.dueDate ASC")
    List<Task> findTasksSortedByPriority(@Param("userId") Long userId);
}
```

---

#### 5. Service Layer

```java
// UserService.java
@Service
@Transactional
@Slf4j
public class UserService {
    
    private final UserRepository userRepository;
    private final PasswordEncoder passwordEncoder;
    
    public UserService(UserRepository userRepository, PasswordEncoder passwordEncoder) {
        this.userRepository = userRepository;
        this.passwordEncoder = passwordEncoder;
    }
    
    public User register(SignUpRequest request) {
        if (userRepository.existsByUsername(request.getUsername())) {
            throw new DuplicateResourceException("Username already exists");
        }
        
        if (userRepository.existsByEmail(request.getEmail())) {
            throw new DuplicateResourceException("Email already exists");
        }
        
        User user = new User();
        user.setUsername(request.getUsername());
        user.setEmail(request.getEmail());
        user.setPassword(passwordEncoder.encode(request.getPassword()));
        user.setRoles(Set.of("ROLE_USER"));
        
        return userRepository.save(user);
    }
    
    @Transactional(readOnly = true)
    public User findById(Long id) {
        return userRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("User not found"));
    }
}

// TaskService.java
@Service
@Transactional
@Slf4j
public class TaskService {
    
    private final TaskRepository taskRepository;
    private final UserRepository userRepository;
    
    public TaskService(TaskRepository taskRepository, UserRepository userRepository) {
        this.taskRepository = taskRepository;
        this.userRepository = userRepository;
    }
    
    public Task createTask(Long userId, TaskRequest request) {
        User user = userRepository.findById(userId)
            .orElseThrow(() -> new ResourceNotFoundException("User not found"));
        
        Task task = new Task();
        task.setTitle(request.getTitle());
        task.setDescription(request.getDescription());
        task.setPriority(request.getPriority());
        task.setDueDate(request.getDueDate());
        task.setUser(user);
        
        return taskRepository.save(task);
    }
    
    @Transactional(readOnly = true)
    public List<Task> getUserTasks(Long userId) {
        return taskRepository.findByUserId(userId);
    }
    
    public Task updateTaskStatus(Long taskId, TaskStatus status) {
        Task task = taskRepository.findById(taskId)
            .orElseThrow(() -> new ResourceNotFoundException("Task not found"));
        
        task.setStatus(status);
        return taskRepository.save(task);
    }
    
    public void deleteTask(Long taskId) {
        Task task = taskRepository.findById(taskId)
            .orElseThrow(() -> new ResourceNotFoundException("Task not found"));
        
        taskRepository.delete(task);
    }
    
    @Scheduled(cron = "0 0 9 * * *")  // Every day at 9 AM
    public void sendDueDateReminders() {
        LocalDateTime tomorrow = LocalDateTime.now().plusDays(1);
        List<Task> tasks = taskRepository.findOverdueTasks(null, tomorrow);
        
        log.info("Sending reminders for {} tasks", tasks.size());
        // Send email notifications
    }
}
```

---

#### 6. Controller Layer

```java
// AuthController.java
@RestController
@RequestMapping("/api/auth")
@Slf4j
public class AuthController {
    
    private final UserService userService;
    private final AuthenticationManager authenticationManager;
    private final JwtTokenProvider tokenProvider;
    
    @PostMapping("/register")
    public ResponseEntity<?> register(@RequestBody @Valid SignUpRequest request) {
        User user = userService.register(request);
        return ResponseEntity.status(HttpStatus.CREATED)
            .body(Map.of("message", "User registered successfully"));
    }
    
    @PostMapping("/login")
    public ResponseEntity<?> login(@RequestBody @Valid LoginRequest request) {
        Authentication authentication = authenticationManager.authenticate(
            new UsernamePasswordAuthenticationToken(
                request.getUsername(),
                request.getPassword()
            )
        );
        
        SecurityContextHolder.getContext().setAuthentication(authentication);
        String jwt = tokenProvider.generateToken(authentication);
        
        return ResponseEntity.ok(new JwtResponse(jwt));
    }
}

// TaskController.java
@RestController
@RequestMapping("/api/tasks")
@Slf4j
public class TaskController {
    
    private final TaskService taskService;
    
    public TaskController(TaskService taskService) {
        this.taskService = taskService;
    }
    
    @GetMapping
    public ResponseEntity<List<Task>> getUserTasks(@AuthenticationPrincipal UserDetails userDetails) {
        // Get current user's tasks
        List<Task> tasks = taskService.getUserTasks(getCurrentUserId(userDetails));
        return ResponseEntity.ok(tasks);
    }
    
    @GetMapping("/{id}")
    public ResponseEntity<Task> getTaskById(@PathVariable Long id) {
        Task task = taskService.findById(id);
        return ResponseEntity.ok(task);
    }
    
    @PostMapping
    public ResponseEntity<Task> createTask(
            @AuthenticationPrincipal UserDetails userDetails,
            @RequestBody @Valid TaskRequest request) {
        Long userId = getCurrentUserId(userDetails);
        Task task = taskService.createTask(userId, request);
        return ResponseEntity.status(HttpStatus.CREATED).body(task);
    }
    
    @PatchMapping("/{id}/status")
    public ResponseEntity<Task> updateStatus(
            @PathVariable Long id,
            @RequestParam TaskStatus status) {
        Task task = taskService.updateTaskStatus(id, status);
        return ResponseEntity.ok(task);
    }
    
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteTask(@PathVariable Long id) {
        taskService.deleteTask(id);
        return ResponseEntity.noContent().build();
    }
    
    private Long getCurrentUserId(UserDetails userDetails) {
        // Extract user ID from UserDetails
        return 1L;  // Simplified
    }
}
```

---

#### 7. DTOs (Data Transfer Objects)

```java
// SignUpRequest.java
@Data
public class SignUpRequest {
    @NotBlank
    @Size(min = 3, max = 20)
    private String username;
    
    @NotBlank
    @Email
    private String email;
    
    @NotBlank
    @Size(min = 6, max = 40)
    private String password;
}

// LoginRequest.java
@Data
public class LoginRequest {
    @NotBlank
    private String username;
    
    @NotBlank
    private String password;
}

// TaskRequest.java
@Data
public class TaskRequest {
    @NotBlank
    private String title;
    
    private String description;
    
    private TaskPriority priority = TaskPriority.MEDIUM;
    
    @Future(message = "Due date must be in future")
    private LocalDateTime dueDate;
}

// JwtResponse.java
@Data
@AllArgsConstructor
public class JwtResponse {
    private String token;
    private String type = "Bearer";
    
    public JwtResponse(String token) {
        this.token = token;
    }
}
```

---

#### 8. Exception Handling

```java
// Custom Exceptions
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}

public class DuplicateResourceException extends RuntimeException {
    public DuplicateResourceException(String message) {
        super(message);
    }
}

// Global Exception Handler
@RestControllerAdvice
@Slf4j
public class GlobalExceptionHandler {
    
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
        log.error("Resource not found: {}", ex.getMessage());
        ErrorResponse error = new ErrorResponse(
            HttpStatus.NOT_FOUND.value(),
            ex.getMessage(),
            LocalDateTime.now()
        );
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }
    
    @ExceptionHandler(DuplicateResourceException.class)
    public ResponseEntity<ErrorResponse> handleDuplicate(DuplicateResourceException ex) {
        ErrorResponse error = new ErrorResponse(
            HttpStatus.CONFLICT.value(),
            ex.getMessage(),
            LocalDateTime.now()
        );
        return ResponseEntity.status(HttpStatus.CONFLICT).body(error);
    }
    
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErrorResponse> handleValidation(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error ->
            errors.put(error.getField(), error.getDefaultMessage())
        );
        
        ErrorResponse error = new ErrorResponse(
            HttpStatus.BAD_REQUEST.value(),
            "Validation failed",
            errors,
            LocalDateTime.now()
        );
        return ResponseEntity.badRequest().body(error);
    }
    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneral(Exception ex) {
        log.error("Unexpected error", ex);
        ErrorResponse error = new ErrorResponse(
            HttpStatus.INTERNAL_SERVER_ERROR.value(),
            "Internal server error",
            LocalDateTime.now()
        );
        return ResponseEntity.status(500).body(error);
    }
}

@Data
@AllArgsConstructor
public class ErrorResponse {
    private int status;
    private String message;
    private Object details;
    private LocalDateTime timestamp;
    
    public ErrorResponse(int status, String message, LocalDateTime timestamp) {
        this.status = status;
        this.message = message;
        this.timestamp = timestamp;
    }
}
```

---

#### 9. Logging Aspect

```java
@Aspect
@Component
@Slf4j
public class LoggingAspect {
    
    @Around("execution(* com.example.taskapi.service.*.*(..))")
    public Object logServiceMethods(ProceedingJoinPoint joinPoint) throws Throwable {
        String methodName = joinPoint.getSignature().getName();
        String className = joinPoint.getTarget().getClass().getSimpleName();
        
        log.info("Executing {}.{}", className, methodName);
        
        long start = System.currentTimeMillis();
        Object result = joinPoint.proceed();
        long duration = System.currentTimeMillis() - start;
        
        log.info("Completed {}.{} in {}ms", className, methodName, duration);
        
        return result;
    }
    
    @AfterThrowing(
        pointcut = "execution(* com.example.taskapi.service.*.*(..))",
        throwing = "error"
    )
    public void logErrors(JoinPoint joinPoint, Throwable error) {
        log.error("Error in {}: {}", 
            joinPoint.getSignature().getName(), 
            error.getMessage());
    }
}
```

---

#### 10. Scheduled Tasks

```java
@Component
@Slf4j
public class TaskScheduler {
    
    private final TaskRepository taskRepository;
    
    public TaskScheduler(TaskRepository taskRepository) {
        this.taskRepository = taskRepository;
    }
    
    // Check for overdue tasks every hour
    @Scheduled(cron = "0 0 * * * *")
    public void checkOverdueTasks() {
        LocalDateTime now = LocalDateTime.now();
        List<Task> overdueTasks = taskRepository.findOverdueTasks(null, now);
        
        log.info("Found {} overdue tasks", overdueTasks.size());
        
        // Send notifications
        overdueTasks.forEach(task -> {
            log.warn("Task '{}' is overdue for user {}", 
                task.getTitle(), 
                task.getUser().getUsername());
        });
    }
    
    // Daily summary at 9 AM
    @Scheduled(cron = "0 0 9 * * *")
    public void sendDailySummary() {
        log.info("Sending daily task summary to all users");
        // Implementation
    }
    
    // Cleanup completed tasks older than 30 days (monthly)
    @Scheduled(cron = "0 0 0 1 * *")
    public void cleanupOldTasks() {
        LocalDateTime thirtyDaysAgo = LocalDateTime.now().minusDays(30);
        log.info("Cleaning up tasks completed before {}", thirtyDaysAgo);
        // Implementation
    }
}
```

---

#### 11. Configuration

```java
// SecurityConfig.java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    
    @Autowired
    private JwtAuthenticationFilter jwtAuthenticationFilter;
    
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf().disable()
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/auth/**").permitAll()
                .requestMatchers("/actuator/**").permitAll()
                .anyRequest().authenticated()
            )
            .sessionManagement()
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            .and()
            .addFilterBefore(jwtAuthenticationFilter, 
                UsernamePasswordAuthenticationFilter.class);
        
        return http.build();
    }
    
    @Bean
    public AuthenticationManager authenticationManager(
            AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();
    }
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}

// AsyncConfig.java
@Configuration
@EnableAsync
public class AsyncConfig {
    
    @Bean(name = "taskExecutor")
    public Executor taskExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(5);
        executor.setMaxPoolSize(10);
        executor.setQueueCapacity(100);
        executor.setThreadNamePrefix("async-");
        executor.initialize();
        return executor;
    }
}
```

---

#### 12. application.properties

```properties
# Application
spring.application.name=Task Management API
server.port=8080

# Database
spring.datasource.url=jdbc:mysql://localhost:3306/taskdb
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

# JWT
jwt.secret=mySecretKeyForJWTTokenGeneration
jwt.expiration=86400000

# Logging
logging.level.root=INFO
logging.level.com.example.taskapi=DEBUG
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} - %msg%n

# Actuator
management.endpoints.web.exposure.include=health,info,metrics
info.app.name=Task Management API
info.app.version=1.0.0
```

---

### Project Features Demonstrated:

**✅ Spring Core:**
- Dependency Injection (constructor injection)
- Bean management
- Component scanning

**✅ Spring Boot:**
- Auto-configuration
- Embedded server
- Starter dependencies
- Profiles

**✅ Spring Data JPA:**
- Entity relationships (@OneToMany, @ManyToOne)
- Repository pattern
- Derived queries
- Custom @Query
- Fetch types (LAZY, EAGER)

**✅ Spring Security:**
- JWT authentication
- Password hashing (BCrypt)
- Security filter chain
- Role-based access

**✅ Spring AOP:**
- Logging aspect
- Method execution timing
- Error logging

**✅ Scheduling:**
- Cron jobs
- Fixed rate/delay tasks
- Scheduled notifications

**✅ Validation:**
- Bean validation
- Custom validators
- Error handling

**✅ Exception Handling:**
- Custom exceptions
- Global exception handler
- Proper HTTP status codes

**✅ Testing:**
- Unit tests
- Integration tests
- MockMvc for controllers

**✅ Production-Ready:**
- Actuator endpoints
- Logging
- Environment configuration
- Error handling

---

## 🎯 Key Takeaways

### Spring Framework:
1. **DI/IoC** - Spring manages object lifecycle
2. **AOP** - Separate cross-cutting concerns
3. **Declarative** - Annotations over configuration
4. **Layered** - Controller → Service → Repository
5. **Transaction Management** - @Transactional for ACID

### Spring Boot:
1. **Auto-configuration** - Minimal setup
2. **Starter Dependencies** - Pre-configured packages
3. **Embedded Server** - No external Tomcat
4. **Production-Ready** - Actuator, metrics, health checks
5. **Convention over Configuration** - Sensible defaults

### Annotations:
1. **Metadata** - Information about code
2. **Retention** - SOURCE, CLASS, RUNTIME
3. **Target** - Where to apply
4. **Processing** - Reflection or compile-time
5. **Spring Uses** - Component scanning, DI, AOP, validation

**Remember:**
> "Spring Boot simplifies enterprise Java. Master DI, understand annotations, use JPA for data, secure with Spring Security, schedule with @Scheduled. Annotations are processed via reflection or AOP proxies."

Good luck with your Spring Framework journey and interviews! 🚀
