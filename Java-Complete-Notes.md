# ☕ Java Complete Notes — Beginner to Pro
* AUTHOR ~ JAY GUPTA---
> **Version:** 1.0  
> **Level:** Beginner → Intermediate → Advanced  
> **Goal:** One-stop reference for Java mastery

---

## 📑 Table of Contents

1. [Introduction & Setup](#1-introduction--setup)
2. [Java Basics](#2-java-basics)
3. [Object-Oriented Programming (OOP)](#3-object-oriented-programming-oop)
4. [Exception Handling](#4-exception-handling)
5. [Java Collections Framework](#5-java-collections-framework)
6. [Multithreading & Concurrency](#6-multithreading--concurrency)
7. [File I/O & NIO](#7-file-io--nio)
8. [Generics](#8-generics)
9. [Lambda Expressions & Stream API](#9-lambda-expressions--stream-api)
10. [JVM Internals](#10-jvm-internals)
11. [Java 8+ Features](#11-java-8-features)
12. [Master Cheatsheet](#12-master-cheatsheet)
13. [Memory Hooks & Interview Tricks](#13-memory-hooks--interview-tricks)

---

## 1. Introduction & Setup

### What is Java?
- **High-level**, **object-oriented**, **platform-independent** language
- Follows **WORA** — *Write Once, Run Anywhere*
- Compiled to **bytecode** (`.class`), executed by **JVM**

### JDK vs JRE vs JVM
| Component | Purpose |
|-----------|---------|
| **JDK** | Development kit (JRE + compilers + tools) |
| **JRE** | Runtime environment (JVM + libraries) |
| **JVM** | Executes bytecode — the heart of Java |

🔑 **Remember:** `JDK ⊃ JRE ⊃ JVM` (like nested boxes)

### First Program
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```
🔑 **Why `public static void main(String[] args)`?**
- `public` — JVM can access it from anywhere
- `static` — no object needed to call it
- `void` — returns nothing
- `main` — entry point name (fixed by JVM)
- `String[] args` — command-line arguments

---

## 2. Java Basics

### Data Types

#### Primitive Types (8 total)
| Type | Size | Default | Range |
|------|------|---------|-------|
| `byte` | 1 byte | 0 | -128 to 127 |
| `short` | 2 bytes | 0 | -32,768 to 32,767 |
| `int` | 4 bytes | 0 | ~-2B to ~2B |
| `long` | 8 bytes | 0L | Huge numbers |
| `float` | 4 bytes | 0.0f | 6-7 decimal digits |
| `double` | 8 bytes | 0.0d | 15-16 decimal digits |
| `char` | 2 bytes | `'\u0000'` | 0 to 65,535 (Unicode) |
| `boolean` | 1 bit* | `false` | `true` or `false` |

🔑 **Memory Trick:** `Byte → Short → Int → Long` (sizes: 1, 2, 4, 8 — doubles each time)

#### Wrapper Classes
```java
int x = 10;
Integer obj = Integer.valueOf(x);      // Boxing
int y = obj.intValue();                // Unboxing
Integer auto = x;                      // Autoboxing (Java 5+)
int z = auto;                          // Auto-unboxing
```

⚠️ **Trap:** `==` compares reference for wrappers, `.equals()` compares value. Always use `.equals()` for wrapper comparison!

### Variables
```java
int age = 25;                    // Local variable
static double PI = 3.14;         // Class/static variable
String name;                     // Instance variable (default: null)
```

### Type Casting
```java
// Implicit (Widening) — automatic, safe
int a = 100;
long b = a;

// Explicit (Narrowing) — manual, risky
double c = 100.99;
int d = (int) c;    // d = 100 (data loss!)
```

🔑 **Widening is automatic; Narrowing needs a cast!**

### Operators
| Category | Operators |
|----------|-----------|
| Arithmetic | `+ - * / %` |
| Relational | `== != > < >= <=` |
| Logical | `&& \|\| !` |
| Bitwise | `& \| ^ ~ << >> >>>` |
| Ternary | `condition ? value1 : value2` |

⚠️ `&` vs `&&`: `&&` short-circuits; `&` always evaluates both sides

### Control Flow

```java
// If-Else-If Ladder
if (score >= 90) grade = 'A';
else if (score >= 80) grade = 'B';
else grade = 'F';

// Switch (Enhanced since Java 14)
switch (day) {
    case MONDAY, FRIDAY -> System.out.println("Meeting day");
    case TUESDAY -> System.out.println("Work day");
    default -> System.out.println("Other");
}

// Loops
for (int i = 0; i < 10; i++) { }     // For loop
while (condition) { }                 // While loop
do { } while (condition);             // Do-while (runs at least once)

// Enhanced For (For-each)
for (String name : names) {
    System.out.println(name);
}
```

### Arrays
```java
// Declaration & Initialization
int[] numbers = new int[5];
int[] values = {1, 2, 3, 4, 5};

// 2D Array
int[][] matrix = new int[3][3];

// Key Methods (Arrays class)
Arrays.sort(arr);
Arrays.binarySearch(arr, key);
Arrays.fill(arr, value);
Arrays.copyOf(arr, newLength);
```

🔑 **Arrays have fixed size! For dynamic size, use ArrayList.**

### Strings (Immutable!)
```java
String s1 = "Hello";           // String literal (pool)
String s2 = new String("Hello"); // Heap object

// Important Methods
s1.length();
s1.charAt(0);
s1.substring(0, 3);            // "Hel"
s1.equals(s2);                 // true (content)
s1 == s2;                      // false (reference for new String())
s1.concat(" World");           // Returns NEW string (original unchanged)
```

⚠️ **String is IMMUTABLE.** Every "modification" creates a new object!

**StringBuilder** (mutable, not thread-safe) vs **StringBuffer** (mutable, thread-safe):
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");           // Modifies existing object — faster!
```

🔑 **Rule of Thumb:**
- `String` — constant/unchanging text
- `StringBuilder` — single-threaded, frequent modifications
- `StringBuffer` — multi-threaded, frequent modifications (rarely needed now)

---

## 3. Object-Oriented Programming (OOP)

### Class & Object
```java
public class Student {
    // Fields (Instance Variables)
    private String name;
    private int rollNo;
    
    // Constructor
    public Student(String name, int rollNo) {
        this.name = name;
        this.rollNo = rollNo;
    }
    
    // Methods
    public void study() {
        System.out.println(name + " is studying");
    }
    
    // Getters & Setters
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}

// Creating Object
Student s = new Student("Jay", 101);
```

### The 4 Pillars of OOP

#### 1. Encapsulation (Data Hiding)
```java
// Wrap data + methods together; control access via getters/setters
private int age;              // Hide the data
public int getAge() {         // Controlled access
    return age;
}
```
🔑 **Think of a capsule — medicine is hidden inside, you only consume through the shell.**

#### 2. Inheritance (IS-A Relationship)
```java
class Animal {
    void eat() { System.out.println("Eating..."); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking..."); }
}

Dog d = new Dog();
d.eat();    // Inherited from Animal
d.bark();   // Own method
```

🔑 **Types of Inheritance in Java:**
- Single: `B extends A`
- Multilevel: `C extends B extends A`
- Hierarchical: `B extends A`, `C extends A`
- ⚠️ **Java does NOT support Multiple Inheritance with classes** (Diamond Problem). Use **Interfaces** instead.

**`super` Keyword:**
```java
class Dog extends Animal {
    Dog() {
        super();           // Calls parent constructor (must be first line)
    }
    void eat() {
        super.eat();       // Calls parent's eat()
        System.out.println("Dog eating");
    }
}
```

#### 3. Polymorphism (Many Forms)

**Compile-time (Method Overloading):**
```java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
}
```
🔑 **Same name, different parameters. Decision at compile time.**

**Runtime (Method Overriding):**
```java
class Animal {
    void sound() { System.out.println("Animal sound"); }
}
class Cat extends Animal {
    @Override
    void sound() { System.out.println("Meow"); }
}

Animal a = new Cat();
a.sound();    // Output: "Meow" — JVM decides at runtime!
```
🔑 **Same signature, different body in child. Decision at runtime.**

**Rules for Overriding:**
- Same method name & parameter list
- Return type must be same or covariant
- Access modifier cannot be more restrictive
- `static` methods cannot be overridden (they are hidden)

#### 4. Abstraction (Hiding Implementation)

**Abstract Class** (0-100% abstraction):
```java
abstract class Shape {
    abstract void draw();          // No body — MUST implement in child
    void print() {                 // Can have concrete methods too
        System.out.println("Printing...");
    }
}
```

**Interface** (100% abstraction before Java 8):
```java
interface Drawable {
    void draw();                   // Implicitly public abstract
    default void print() {         // Java 8+: default method with body
        System.out.println("Default print");
    }
    static void info() {           // Java 8+: static method
        System.out.println("Info");
    }
}
```

🔑 **When to use what?**
- **Abstract Class:** IS-A relationship + shared code + state (fields)
- **Interface:** CAN-DO relationship + multiple behaviors + no state

### Important Keywords

| Keyword | Purpose |
|---------|---------|
| `this` | Refers to current object |
| `super` | Refers to parent class |
| `static` | Belongs to class, not instance |
| `final` | Variable = constant, Method = cannot override, Class = cannot extend |
| `abstract` | No implementation — must be completed by child |
| `synchronized` | Thread-safe access |
| `volatile` | Variable always read from main memory |
| `transient` | Field not serialized |
| `instanceof` | Checks object type |

### Object Class (Mother of All Classes)
Every class implicitly extends `Object`. Key methods:
- `toString()` — String representation
- `equals(Object obj)` — Content equality (override for custom logic)
- `hashCode()` — Integer hash (contract: equal objects → equal hashcodes)
- `clone()` — Creates copy (class must implement `Cloneable`)
- `finalize()` — Called before garbage collection (deprecated in Java 9+)

⚠️ **Always override `equals()` and `hashCode()` together!**

```java
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Student student = (Student) o;
    return rollNo == student.rollNo && Objects.equals(name, student.name);
}

@Override
public int hashCode() {
    return Objects.hash(name, rollNo);
}
```

---

## 4. Exception Handling

### Exception Hierarchy
```
Throwable
├── Error (Unchecked — system-level, don't catch)
│     └── OutOfMemoryError, StackOverflowError
└── Exception
      ├── RuntimeException (Unchecked — programming errors)
      │     └── NullPointerException, ArrayIndexOutOfBoundsException, IllegalArgumentException
      └── Checked (Must handle or declare)
            └── IOException, SQLException, ClassNotFoundException
```

🔑 **Unchecked = Runtime = Your fault. Checked = Compile-time = You MUST handle.**

### Try-Catch-Finally
```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero!");
} catch (Exception e) {
    System.out.println("General error");
} finally {
    System.out.println("Always executes!");   // Cleanup code here
}
```

**Try-with-resources (Java 7+):**
```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line = br.readLine();
} catch (IOException e) {
    e.printStackTrace();
}
// br is automatically closed!
```

### Throw & Throws
```java
public void withdraw(double amount) throws InsufficientFundsException {
    if (amount > balance) {
        throw new InsufficientFundsException("Not enough money");
    }
}
```

**Custom Exception:**
```java
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}
```

🔑 **Best Practices:**
- Catch most specific exception first
- Never catch `Throwable` or `Exception` broadly unless logging/rethrowing
- Use try-with-resources for AutoCloseable resources
- Create meaningful custom exceptions for business logic errors

---

## 5. Java Collections Framework

### Hierarchy
```
Collection (Interface)
├── List (Ordered, allows duplicates)
│     ├── ArrayList
│     ├── LinkedList
│     └── Vector → Stack
├── Set (No duplicates)
│     ├── HashSet (Unordered)
│     ├── LinkedHashSet (Insertion order)
│     └── TreeSet (Sorted)
└── Queue (FIFO)
      ├── PriorityQueue
      └── Deque → ArrayDeque

Map (Interface — key-value pairs)
├── HashMap
├── LinkedHashMap
├── TreeMap (Sorted by key)
└── Hashtable (Thread-safe, legacy)
```

### List Implementations
```java
List<String> arrayList = new ArrayList<>();      // Dynamic array, fast random access
List<String> linkedList = new LinkedList<>();    // Doubly-linked, fast insertion/deletion
```

| Operation | ArrayList | LinkedList |
|-----------|-----------|------------|
| get(index) | O(1) | O(n) |
| add(end) | O(1)* | O(1) |
| add(middle) | O(n) | O(1) |
| remove(middle) | O(n) | O(1) |
| Memory | Less | More (node overhead) |

### Set Implementations
```java
Set<Integer> hashSet = new HashSet<>();               // Fastest, no order
Set<Integer> linkedHashSet = new LinkedHashSet<>();   // Maintains insertion order
Set<Integer> treeSet = new TreeSet<>();               // Sorted ascending, O(log n) ops
```

### Map Implementations
```java
Map<String, Integer> hashMap = new HashMap<>();           // Fastest, null key allowed
Map<String, Integer> linkedHashMap = new LinkedHashMap<>(); // Maintains insertion order
Map<String, Integer> treeMap = new TreeMap<>();           // Sorted by key
Map<String, Integer> hashtable = new Hashtable<>();       // Thread-safe, no null
```

🔑 **HashMap Internals (Crucial for Interviews):**
- Array of **buckets** (Node<K,V>[] table)
- Uses `hashCode()` to find bucket index: `(n - 1) & hash`
- Collision resolution: **Separate chaining** (Linked List → Tree if > 8 nodes)
- Default: Capacity = 16, Load Factor = 0.75
- When size > capacity × load factor → **Rehashing** (doubles capacity)

### Collections Class Utility Methods
```java
Collections.sort(list);
Collections.reverse(list);
Collections.shuffle(list);
Collections.binarySearch(list, key);
Collections.max(list);
Collections.min(list);
Collections.synchronizedList(new ArrayList<>());
Collections.unmodifiableList(list);
```

### Comparable vs Comparator
```java
// Comparable — Natural ordering (class implements it)
class Student implements Comparable<Student> {
    public int compareTo(Student other) {
        return this.age - other.age;    // Ascending by age
    }
}

// Comparator — Custom/multiple sorting strategies
Comparator<Student> byName = Comparator.comparing(s -> s.name);
Comparator<Student> byAgeDesc = (s1, s2) -> s2.age - s1.age;
Collections.sort(students, byName);
```

🔑 **Comparable = `compareTo()` = One natural order. Comparator = `compare()` = Multiple custom orders.**

---

## 6. Multithreading & Concurrency

### Creating Threads
```java
// Method 1: Extend Thread
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running");
    }
}
MyThread t = new MyThread();
t.start();    // NEVER call t.run() directly!

// Method 2: Implement Runnable (Preferred — better OOP)
Runnable r = () -> System.out.println("Runnable running");
new Thread(r).start();

// Method 3: Implement Callable (Returns value)
Callable<Integer> c = () -> 42;
FutureTask<Integer> ft = new FutureTask<>(c);
new Thread(ft).start();
Integer result = ft.get();    // Blocks until done
```

### Thread Lifecycle
```
NEW → RUNNABLE → (RUNNING) → BLOCKED/WAITING/TIMED_WAITING → TERMINATED
```

### Thread Methods
```java
thread.start();       // Begins execution
thread.join();        // Wait for this thread to die
thread.sleep(1000);   // Pause for milliseconds (static method)
thread.yield();       // Hint to scheduler (static method)
thread.interrupt();   // Interrupt sleeping/waiting thread
```

### Synchronization
```java
// Synchronized method
public synchronized void increment() { count++; }

// Synchronized block
public void increment() {
    synchronized(this) { count++; }
}

// Static synchronization
public static synchronized void method() { }
```

### Inter-Thread Communication
```java
// wait() — releases lock, goes to waiting state
// notify() — wakes one waiting thread
// notifyAll() — wakes all waiting threads

synchronized(lock) {
    while (!condition) {
        lock.wait();     // Must be inside synchronized block
    }
    // do work
    lock.notifyAll();
}
```

🔑 **wait()/notify() are on Object, not Thread!** Every object has a monitor/lock.

### Executor Framework (Preferred over raw threads)
```java
ExecutorService executor = Executors.newFixedThreadPool(5);
Future<Integer> future = executor.submit(() -> 42);
executor.shutdown();    // Always shutdown!
```

| Executor Type | Use Case |
|---------------|----------|
| `newFixedThreadPool(n)` | Limited concurrent threads |
| `newCachedThreadPool()` | Many short-lived tasks |
| `newSingleThreadExecutor()` | Sequential execution |
| `newScheduledThreadPool(n)` | Delayed/periodic tasks |

### Concurrent Collections
```java
ConcurrentHashMap<K, V>        // Thread-safe Map, better than Hashtable
CopyOnWriteArrayList<E>        // Thread-safe List (copy-on-write)
BlockingQueue<E>               // Producer-consumer pattern
```

---

## 7. File I/O & NIO

### Classic I/O (java.io)
```java
// Reading file
BufferedReader br = new BufferedReader(new FileReader("file.txt"));
String line;
while ((line = br.readLine()) != null) {
    System.out.println(line);
}
br.close();

// Writing file
BufferedWriter bw = new BufferedWriter(new FileWriter("file.txt"));
bw.write("Hello");
bw.close();

// Serialization
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("obj.ser"));
oos.writeObject(object);

// Deserialization
ObjectInputStream ois = new ObjectInputStream(new FileInputStream("obj.ser"));
MyClass obj = (MyClass) ois.readObject();
```

🔑 **For Serialization:** Class must implement `Serializable` (marker interface). Use `transient` to skip fields.

### NIO.2 (java.nio — Java 7+)
```java
Path path = Paths.get("data", "file.txt");

// Read all lines
List<String> lines = Files.readAllLines(path);

// Read as String
String content = Files.readString(path);

// Write String
Files.writeString(path, "content");

// Check existence
if (Files.exists(path)) { }

// Stream of lines
try (Stream<String> stream = Files.lines(path)) {
    stream.forEach(System.out::println);
}
```

---

## 8. Generics

### Basics
```java
List<String> names = new ArrayList<>();    // Type-safe list
Map<String, Integer> ages = new HashMap<>();
```

### Generic Class
```java
class Box<T> {
    private T content;
    public void set(T content) { this.content = content; }
    public T get() { return content; }
}
Box<String> stringBox = new Box<>();
Box<Integer> intBox = new Box<>();
```

### Bounded Types
```java
// Upper bound — T must be Number or subclass
class Calculator<T extends Number> { }

// Multiple bounds
class Example<T extends Number & Comparable<T>> { }

// Wildcards
List<?> anyList;                    // Unbounded
List<? extends Number> numList;     // Upper bound — can read Number, cannot add
List<? super Integer> intParent;    // Lower bound — can add Integer, read as Object
```

🔑 **PECS Principle:**
- **P**roducer → **E**xtends (read from collection)
- **C**onsumer → **S**uper (write to collection)

```java
// Producer — we read Animals from it
void printAnimals(List<? extends Animal> animals) { }

// Consumer — we add Integers to it
void addNumbers(List<? super Integer> list) { list.add(10); }
```

---

## 9. Lambda Expressions & Stream API

### Lambda Syntax
```java
// (parameters) -> { body }
Runnable r = () -> System.out.println("Running");
Comparator<String> c = (a, b) -> a.length() - b.length();
Function<Integer, String> f = num -> "Number: " + num;
```

### Functional Interfaces (java.util.function)
| Interface | Method | Use |
|-----------|--------|-----|
| `Predicate<T>` | `test(T)` → boolean | Filter condition |
| `Function<T,R>` | `apply(T)` → R | Transform |
| `Consumer<T>` | `accept(T)` → void | Side effect |
| `Supplier<T>` | `get()` → T | Provide value |
| `UnaryOperator<T>` | `apply(T)` → T | Transform same type |
| `BinaryOperator<T>` | `apply(T,T)` → T | Reduce two to one |

### Stream API
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

List<Integer> result = numbers.stream()
    .filter(n -> n % 2 == 0)        // Intermediate: keep evens
    .map(n -> n * n)                // Intermediate: square them
    .sorted(Comparator.reverseOrder()) // Intermediate: sort desc
    .limit(3)                       // Intermediate: take top 3
    .collect(Collectors.toList());  // Terminal: collect to list

// Common Terminal Operations
.forEach(System.out::println);
.count();
.reduce(0, Integer::sum);
.anyMatch(n -> n > 5);
.allMatch(n -> n > 0);
.findFirst();
.collect(Collectors.toMap(k -> k, v -> v * 2));
```

🔑 **Stream Characteristics:**
- **Intermediate ops** return Stream (lazy — not executed until terminal op)
- **Terminal ops** produce result or side-effect (trigger execution)
- Once consumed, stream cannot be reused!

### Method References
```java
list.forEach(System.out::println);           // object::method
list.stream().map(String::toUpperCase);      // Class::instanceMethod
list.stream().map(Integer::valueOf);         // Class::staticMethod
Supplier<List<String>> s = ArrayList::new;   // Class::new
```

---

## 10. JVM Internals

### Memory Areas
| Area | Purpose |
|------|---------|
| **Method Area** | Class metadata, static variables, method code |
| **Heap** | All objects and arrays live here |
| **Stack** | Method frames, local variables (each thread gets one) |
| **PC Register** | Address of current instruction (per thread) |
| **Native Method Stack** | Native (C/C++) method execution |

### Garbage Collection
```
Heap Structure:
┌─────────────┬─────────────┬─────────────────────────────┐
│   Young     │             │          Old                 │
│  Generation │   Survivor  │       Generation             │
│  (Eden)     │   (S0, S1)  │                              │
└─────────────┴─────────────┴─────────────────────────────┘
```

**GC Process:**
1. New objects → **Eden**
2. Minor GC → Live objects → **Survivor** (S0 or S1)
3. After several survivals → **Old Generation**
4. Old Gen full → **Major GC / Full GC** (slower!)

**GC Algorithms:**
- **Serial GC:** Single thread, stop-the-world
- **Parallel GC:** Multi-threaded throughput
- **CMS:** Concurrent mark-sweep (low latency)
- **G1 GC:** Default since Java 9 — divides heap into regions
- **ZGC / Shenandoah:** Ultra-low latency (Java 11+)

🔑 **Important Flags:**
```bash
-Xms512m          # Initial heap size
-Xmx2g            # Maximum heap size
-XX:+UseG1GC      # Use G1 garbage collector
-XX:+PrintGCDetails
```

### Class Loading
```
Loading → Verification → Preparation → Resolution → Initialization
```

**Classloaders:**
1. **Bootstrap** — Loads core Java classes (`rt.jar`)
2. **Extension** — Loads extension libraries
3. **Application** — Loads classpath classes

🔑 **Delegation Model:** Before loading a class, a classloader delegates to its parent first.

---

## 11. Java 8+ Features

### Java 8
- Lambda expressions
- Stream API
- Default & static methods in interfaces
- Method references
- Optional class
- New Date/Time API (`java.time`)

### Optional (Null Safety)
```java
Optional<String> opt = Optional.ofNullable(getString());
opt.ifPresent(System.out::println);
String value = opt.orElse("default");
String result = opt.orElseThrow(() -> new RuntimeException("Missing!"));
```

🔑 **Never use `Optional.get()` without `isPresent()` check!** Use `orElse` or `orElseThrow`.

### New Date/Time API
```java
LocalDate date = LocalDate.now();                    // 2024-01-15
LocalTime time = LocalTime.now();                    // 14:30:00
LocalDateTime dt = LocalDateTime.now();
ZonedDateTime zdt = ZonedDateTime.now(ZoneId.of("Asia/Kolkata"));

// Formatting
DateTimeFormatter fmt = DateTimeFormatter.ofPattern("dd-MM-yyyy");
String formatted = date.format(fmt);

// Period & Duration
Period p = Period.between(startDate, endDate);
Duration d = Duration.between(startTime, endTime);
```

### Other Version Highlights
| Version | Key Features |
|---------|-------------|
| **9** | Jigsaw (modules), JShell, private interface methods |
| **10** | `var` local variable type inference |
| **11** | New HTTP Client, ZGC, `String` methods (`isBlank`, `lines`, `strip`) |
| **14** | Switch expressions (standard), records (preview) |
| **15** | Text blocks, sealed classes (preview) |
| **16** | Records finalized, pattern matching for instanceof |
| **17** (LTS) | Sealed classes finalized, new macOS rendering |
| **21** (LTS) | Virtual threads (Project Loom), sequenced collections |

### Records (Java 16+)
```java
public record Person(String name, int age) { }
// Automatically generates: constructor, getters, equals, hashCode, toString

Person p = new Person("Jay", 25);
System.out.println(p.name());    // Note: method-style access, not field
```

### Sealed Classes (Java 17)
```java
public sealed class Shape permits Circle, Square, Rectangle { }
public final class Circle extends Shape { }
```

### Virtual Threads (Java 21)
```java
Thread.startVirtualThread(() -> {
    System.out.println("Running in virtual thread");
});

// Or with ExecutorService
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    executor.submit(() -> "task");
}
```
🔑 **Virtual threads are lightweight — you can create millions!** OS threads are heavy, virtual threads are JVM-managed.

---

## 12. Master Cheatsheet

### Quick Reference Table

| Concept | Quick Recall |
|---------|-------------|
| `==` vs `.equals()` | `==` → reference (primitives: value); `.equals()` → content |
| `String` immutable | Every change creates new object |
| `final` | Variable=const, Method=not override, Class=not extend |
| `static` | Belongs to class, shared across objects |
| Abstract vs Interface | Abstract=IS-A + state; Interface=CAN-DO + behavior |
| `ArrayList` vs `LinkedList` | Random access vs Insert/Delete |
| `HashMap` vs `TreeMap` | Fast/O(1) vs Sorted/O(log n) |
| `HashSet` internal | Backed by `HashMap` (dummy value) |
| `synchronized` | Lock on object/monitor |
| `volatile` | Visibility, NOT atomicity |
| `wait/notify` | Object methods, need synchronized |
| `throw` vs `throws` | `throw` = actually throw; `throws` = declaration |
| Checked vs Unchecked | Checked=handle/declare; Unchecked=Runtime |
| Stream lazy | Intermediate ops lazy; terminal triggers |
| `var` (Java 10) | Local var only; compiler infers type |

### Modifier Access Table
```
                    Same Class   Same Package   Subclass   Anywhere
public                 ✓            ✓            ✓           ✓
protected              ✓            ✓            ✓           ✗
default (package)      ✓            ✓            ✗           ✗
private                ✓            ✗            ✗           ✗
```

### Collection Time Complexity
```
                    |  Add  | Remove |  Get  | Contains | Next
ArrayList           | O(1)* |  O(n)  | O(1)  |   O(n)   | O(1)
LinkedList          | O(1)  |  O(1)  | O(n)  |   O(n)   | O(1)
HashSet/Map         | O(1)* |  O(1)* | O(1)  |   O(1)   | O(h/n)
TreeSet/Map         |O(log n)|O(log n)|O(log n)| O(log n)| O(log n)
PriorityQueue       | O(log n)| O(log n)| O(1) |   —     | O(log n)
```
*Amortized / depends on hash distribution

### Object Methods Contract
```java
equals() and hashCode() MUST be consistent:
  If a.equals(b) → a.hashCode() == b.hashCode()
  (Reverse is NOT required)

compareTo() contract:
  Negative → this < other
  Zero     → this == other
  Positive → this > other
```

---

## 13. Memory Hooks & Interview Tricks

### 🧠 Easy Memory Techniques

1. **`String` Pool:**
   > *Imagine a swimming pool — once a "Hello" float is there, everyone shares it. New String() builds a private pool in your backyard.*

2. **Heap vs Stack:**
   > *Heap = Heap of objects (shared, managed by GC). Stack = Stack of plates (LIFO, per thread, method frames).*

3. **`final` vs `finally` vs `finalize`:**
   > *`final` = FINALLY decided (can't change). `finally` = FINALLY executes (always runs). `finalize` = garbage collector's final call (deprecated!).*

4. **`throw` vs `throws`:**
   > *`throw` = THROW the ball (action). `throws` = "This method THROWS responsibility to caller" (warning label).*

5. **Abstract vs Interface:**
   > *Abstract class = half-built house (some walls up). Interface = blueprint only (contract, no walls).*

6. **`Comparable` vs `Comparator`:**
   > *`Comparable` = "I compare MYSELF to others" (natural). `Comparator` = "I compare TWO OTHERS" (external judge).*

7. **HashMap Collision:**
   > *Think of a shared apartment mailbox. Same address? Chain them (linked list). Too many at one address? Convert to a tree (apartment complex with floor numbers).*

8. **`synchronized`:**
   > *Bathroom lock. One person at a time. Others wait outside.*

9. **`volatile`:**
   > *A whiteboard everyone reads from directly. But writing still needs care — it's visible, not atomic!*

10. **Stream Pipeline:**
    > *Assembly line. Intermediate steps set up the factory. Terminal step hits the ON button and products roll out.*

### 🎯 Common Interview Questions

**Q: Why is String immutable?**
- String pool can safely reuse references
- Hashcodes can be cached (used in HashMap keys)
- Thread-safe by default
- Security (network, file paths can't be altered)

**Q: Why no multiple inheritance in Java classes?**
- Diamond Problem: If B and C extend A, and D extends both B and C — which method does D inherit?
- Interfaces solve this (methods are abstract until Java 8)

**Q: `ArrayList` vs `Vector`?**
- `ArrayList` — unsynchronized, faster
- `Vector` — synchronized (thread-safe), slower, legacy

**Q: `fail-fast` vs `fail-safe` iterators?**
- `fail-fast` — throws ConcurrentModificationException (ArrayList, HashMap)
- `fail-safe` — works on clone/copy (ConcurrentHashMap, CopyOnWriteArrayList)

**Q: How does `HashMap` work internally?**
1. Compute `hash = hashCode()`
2. Index = `(n - 1) & hash`
3. If empty → insert Node
4. If collision → append to linked list
5. If list > 8 AND table > 64 → convert to Red-Black Tree
6. If load factor exceeded → resize (double capacity, rehash)

**Q: What happens if `hashCode()` always returns 1?**
- All objects land in same bucket → O(n) degradation → worst-case linked list

### 📝 Code Patterns to Remember

**Singleton Pattern (Thread-safe):**
```java
public class Singleton {
    private static volatile Singleton instance;
    private Singleton() { }
    
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

**Try-with-resources:**
```java
try (Connection conn = DriverManager.getConnection(url);
     Statement stmt = conn.createStatement();
     ResultSet rs = stmt.executeQuery(query)) {
    while (rs.next()) { /* process */ }
} // All closed automatically!
```

**Builder Pattern:**
```java
Computer comp = new Computer.Builder("Intel i7", "16GB")
    .setSSD("512GB")
    .setGPU("RTX 4060")
    .build();
```

---

## ✅ Checklist: Java Mastery Path

| Level | Topics |
|-------|--------|
| **Beginner** | Syntax, OOP, Arrays, Strings, Basic Collections |
| **Intermediate** | Exception handling, Generics, I/O, Multithreading basics |
| **Advanced** | JVM internals, Concurrency utilities, Stream API, Design Patterns |
| **Expert** | GC tuning, Performance optimization, Custom frameworks, Virtual threads |

---

> **"Write code that is easy to delete, not easy to extend."** — Java Philosophy

> *Keep this guide handy. Revisit the cheatsheet section before interviews. Practice coding every concept — reading alone won't make it stick!*

---

**End of Notes — Happy Coding! ☕**
