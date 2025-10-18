# Chapter 2: Object Oriented Design with Java Basic
**Name:** Daymian Snowden
**Assignment:** Midterm
---
## Chapter covers:
- OOD terminology and philosophy
- Introduction to class
- Basic class design 
- Constructors
- Getters/setters
- The *this* pointer
- OOD pros and cons
- Example problems showing the difference between an OOD approach vs procedural approach
---
### Object-Oriented Design (OOD)
We talked a little bit about OOD in chapter 1, but let's discuss it in detail.
Rather than approach problems as independent problems, OOD seeks to build a cohesive system of objects.
These objects contain states, behaviors, and identities. 
In Java, these are represented by fields (state), methods (behavior), and a unique memory reference (identity).
As such, OOD treats objects as representations of real or abstract entities, and us programmers use their interactions and relationships to achieve our aims.
Instead of using separate entities to represent either data or functions, OOD uses objects to represent and manipulate data simultaneously.
Much like Dr. Alan Kay explained earlier, objects work like cells; each contains their own internal data, methods, relationships, and independence.
Rather than asking ourselves "what steps do I need to perform to complete a task", we ask ourselves "what objects exist and how can their interactions meet our requirements".

Let's go over some terminology, principles, and design that will further explain the OOD paradigm.

**Important OOD Terminology**

- **Class**: A blueprint or template that defines the structure and behavior of objects. 
  - It specifies what fields (data) and methods (behavior) objects created from this class will have. 
  - They are basically plans — it defines a resulting object without being an object itself.

- **Object (or Instance)**: A concrete realization of a class created in memory. 
  - If a class is the blueprint, an object is the resulting item. 
  - Each object has its own copy of the class's fields, but also shares the class's methods.

- **Method**: Any function defined within a class that describes what objects (of that class) can do.
  - Methods represent the behavior of objects
  - Methods can also access and modify the object's fields

- **Field (Attribute/Property)**: A variable defined within a class that holds data.
    - Fields represent the state of objects and define what information each object stores.

- **Constructor**: This is a special method that is called when creating a new object using the `new` keyword.
    - Constructors initialize an object's fields and prepare it for use.
    - A constructor has the same name as its class and has no return type.

- **Encapsulation**: The practice of bundling data (fields) and the methods that operate on that data together within a class, which also can hide the internal implementation details. 
  - In Java, access modifiers (`private`, `public`, `protected`) that control what parts of a class are visible to other classes. 
  - Encapsulation protects object integrity by preventing external code from directly manipulating internal state.

- **Inheritance**: A mechanism where a new class (subclass/child) is created based on an existing class (superclass/parent), inheriting its fields and methods. 
  - This establishes an "is-a" relationship and promotes code reuse.
  - For example, if `Dog` inherits from `Animal`, a dog becomes an animal and automatically has all the properties and behaviors of its class (animal).

- **Polymorphism**: The ability for objects of different classes to respond to the same method call in different ways.
  - Fun fact! Polymorphism literally means "many forms".
  - Polymorphism allows you to write general code that works with multiple specific types.
    For instance, `animal.makeSound()` could be programmed to produce different results on the `animal`, such as a dog, cat, or goose.

- **Abstraction**: The practice of hiding complex implementation details and exposing only essential features.
  - Abstraction lets you focus on **what** an object does, not **how** it does it.
  - We focus on using classes to simplify otherwise complex systems.
  - It's like driving a car; while driving, we are (hopefully) not concerned about the nuance of fuel injection or electrical wiring, and instead focusing on steering, braking, etc.
  - In Java, we primarily use abstract classes and interfaces as abstractions.

- **Composition**: Build complex objects by combining simpler objects, establishing "has-a" relationships between classes.
  - Promotes code reuse and creates flexible designs that are easier to modify when compared to inheritance hierarchies.
  - Objects contain instances of other objects as fields and delegate responsibilities to them
  - Example: A `Car` *has an* `Engine`, *has a* `Transmission`, and *has* `Wheel` objects; the car contains these objects and uses their methods, but is itself a distinct object.

- **Message Passing**: The process by which objects communicate with each other through method calls.
  - For example, if we call `student.calculateGPA()`, we are actually sending a message to the student object and requesting it to perform that action (calculate student GPA).
  
- **Contract**: A promise or agreement about what methods a class must provide.
  - Any class that implements or extends an interface or abstract class must provide a set of specific methods with these signatures
  - Here is an example contract below:
```java
// This interface is a CONTRACT
public interface Flyable {
void fly();      // Contract: You MUST have a fly() method
void land();     // Contract: You MUST have a land() method
}

// Bird must fulfill the contract
public class Bird implements Flyable {
    @Override
    public void fly() {
        System.out.println("Flapping wings");
    }

    @Override
    public void land() {
        System.out.println("Landing on branch");
    }
}
``` 

**Key Principles (SOLID)**

The SOLID principles are five design guidelines that help create maintainable, flexible, and understandable object-oriented code. The acronym stands for:

- **Single Responsibility Principle (SRP)**: A class should have only one reason to change, meaning it should have only one job or responsibility.
  - If a class tries to do too many things, changes to one responsibility can break functionality related to another.
  - For example, a `Student` class should handle student data and behavior; it should not be used for database connections or file I/O.

- **Open/Closed Principle (OCP)**: Classes should be open for extension but closed for modification.
  - You should be able to add new functionality by creating new classes (through inheritance or composition) without changing existing, working code.
  - This principle reduces the risk of breaking existing functionality when adding features.

- **Liskov Substitution Principle (LSP)**: Objects of a subclass should be able to replace objects of the superclass without breaking the program. 
  - For example, if `Dog` extends `Animal`, you should be able to use a `Dog` object anywhere an `Animal` object is expected.
  - In this way, we say that subclasses must honor the contracts established by their parent classes.

- **Interface Segregation Principle (ISP)**: Clients should not be forced to depend on interfaces they don't use.
  - Rather than creating one large, general-purpose interface, we should create smaller, specific interfaces.
  - For example, instead of a giant `Animal` interface with methods for all the locomotion types, we should instead create separate `Flys`, `Swims`, and `Runs` interfaces.

- **Dependency Inversion Principle (DIP)**: High-level modules should not depend on low-level modules; instead, both should depend on abstractions.
  - Quiz time! What's an abstraction? An abstraction is simplified representation of something more complicated.
  - Additionally, abstractions should not depend on details!
  - Details should depend on abstractions, which should encourage interfaces over concrete implementations, resulting in more flexible and testable code.

**System Design**

System design in OOD involves identifying the major components (classes and objects) of your program, then determining how they interact in relation to one's goals.
Key considerations include:

- **Identifying Objects and Classes**: Analyze the problem domain to determine what entities exist.
  - Look at nouns in the problem description—these often become classes and objects.
  - Define classes based on the objects in the system.
  - For a university system, we would identify students, courses, professors, etc.

- **Defining Relationships**: Determine how objects relate to each other.
  - Common relationships include "has-a" (composition), "is-a" (inheritance), and "uses-a" (dependency).
  - For example, a University *has an* HR department, a professor *is an* employee, and a course *uses a* classroom.

- **Establishing Responsibilities**: Decide what each class is responsible for.
  - Apply SRP to keep classes focused.
  - Define methods for each class.
  - A `Course` class should manage enrollment and grading, while a separate `Transcript` class manages a student's academic history.

- **Planning for Change**: Design systems that can accommodate future requirements without major rewrites.
  - Implement the classes and objects, preferably using a test based framework when appropriate.
  - Use interfaces and abstract classes to define contracts
  - Concrete classes implement contracts in different ways.

**Object Design**

Object design focuses on the internal structure of individual classes—what fields they contain, what methods they provide, and how they maintain their invariants (rules that must always be true).
Key aspects include:

- **Choosing Fields**: Determine what data each object needs to store to represent its state.
  - Fields should be directly related to the class's responsibilities.
  - A `BankAccount` needs a `balance` and `accountNumber`; we don't need to know the account holder's favorite color.

- **Defining Methods**: Create methods that allow objects to perform their responsibilities and interact with other objects.
  - Methods should have clear, single purposes and descriptive names.
  - It is better to use many small methods over a few large methods, as this reduces the scale of errors and helps during debugging.

- **Access Control**: Use access modifiers appropriately.
  - Make fields `private` by default to enforce encapsulation, and provide `public` methods (getters/setters) only when external access is necessary.
  - Protect internal implementation details, in accordance with abstraction and encapsulation.

- **Maintaining Invariants**: Ensure objects can never enter an invalid state.
  - If a `Rectangle` must always have positive dimensions, the constructor and setter methods should not allow for negative values.

- **Designing Constructors**: Provide constructors that initialize objects in valid states.
  - Consider offering multiple constructors for different initialization scenarios.
  - Ensure all constructors result in properly configured objects.

**Common Object Design Patterns**

While we've covered general principles concerning object design, there are recurring problems in OOD that experience developers have identified (to the benefit of all). 
These observations eventually resulted in design patterns as proven solutions to common design challenges.
Using these design patterns will often make code more maintainable, flexible, and understandable. 
Here are some fundamental patterns, although this list is definitely not exhaustive:

- **Creational patterns:** deals with object creation mechanisms; provides flexible ways to create objects appropriate to the situation.
  - **Singleton**: Ensures a class has only one instance throughout the program and provides a global point of access to it.
  Useful for managing shared resources like database connections or configuration settings.
  - **Factory Method**: Defines an interface for creating objects but allows subclasses to decide which class to instantiate.
  This pattern delegates the instantiation logic to subclasses, which makes code more flexible and easier to extend.

- **Structural Patterns**: deals with object composition and relationships between classes; provides ways to change a portion of code without requiring changes to the entire structure.
  - **Adapter**: Converts the interface of one class into an interface that clients expect, allowing incompatible classes to work together.
  Imagine a power adapter that lets you plug a US device into a European outlet; same concept.
  - **Composite**: Composes objects into tree structures to represent part-whole hierarchies (like folders containing files and other folders).
  This allows clients to treat individual objects and compositions uniformly, where we can perform the same operations on a single file, or even an entire folder structure.

- **Behavioral Patterns**: deals with communication between objects and the assignment of responsibilities; provides ways to make interactions more flexible and easier to understand.
  - **Observer**: Defines a one-to-many dependency between objects where changes to one object automatically notify and update all dependent objects.
  This pattern is commonly found in event-driven systems, such that multiple users can respond to events.
  - **Strategy**: Defines a family of interchangeable algorithms and encapsulates each one, allowing the algorithm to vary independently. 
  For example, a sorting system could swap between quicksort, mergesort, or bubblesort without changing the code that calls the sort method.

These patterns represent a lot of collective failures between years of programmers. 
We don't have to memorize them all, but it is extremely helpful to apply these patterns to save time and develop robust solutions.
At the end of the day, why do the work that's already been done, right?
As it is, computer science is a vast field, and one can barely scratch the surface without revealing an overwhelming amount of content.

### Introduction to class

### Basic class design

### Constructors

### Getters/setters

### The *this* pointer
Huh? What is a pointer? More specifically, what is a *this* pointer?

### OOD pros and cons
**OOD Pros**
- Modularity: OOD simplifies development and maintenance by decomposing complicated structures into smaller, more manageable components. 
- Reusability: Objects and classes can be reused across different projects, reducing redundancy and saving time. 
- Scalability: OOD facilitates system growth by making it simple to incorporate new objects without interfering with already-existing functionality. 
- Maintainability: Encapsulation of data and behavior within objects simplifies troubleshooting and updates, enhancing system reliability. 
- Clear Mapping to Real-World Problems: By modeling software after real-world entities and their interactions, OOD makes systems more intuitive and easier to understand. 
- Flexibility and Extensibility: Through inheritance and polymorphism, OOD allows for extending and adapting systems with minimal changes, accommodating future requirements efficiently.

**OOD Cons**
- fads
- 
### Example Problem: Distance Between Two Points
When would it be better to take a more procedural approach rather than OOD?

### Example Problem: Managing A Zoo
Now, there are cases where we clearly see that an OOD approach makes more sense than a procedural approach.

![My Image](null.jpg)
*Figure 1:  pending-  *


---
### Academic Integrity Statement
I understand that my learning is dependent on individual effort and struggle, 
and I acknowledge that this assignment is a 100% original work and that I received no other assistance other than what is listed here.

**Acknowledgements and assistance received:**
- Course Content, primarily modules and lecture content
- Object-oriented programming - https://en.wikipedia.org/wiki/Object-oriented_programming
- Object-Oriented Design (OOD) - System Design - https://www.geeksforgeeks.org/system-design/oops-object-oriented-design/
- Object-Oriented Design (OOD) - https://science.jrank.org/programming/ObjectOriented_Design_OOD.html
- Object (computer science) - https://en.wikipedia.org/wiki/Object_(computer_science)
- Object-oriented design: Designing low-level design - https://medium.com/@kumar.atul.2122/object-oriented-design-designing-low-level-design-1b5ff9f3d0be
- 
I did not use generative AI in any form to create this content and the final content was not adapted from generative AI created content.

I did not view content from anyone else’s submission including submissions from previous semesters nor am I submitting someone else’s previous work in part or in whole.

I am the only creator for this content. All sections are my work and no one else’s with the exception being any starter content provided by the instructor.
If asked to explain any part of this content, I will be able to.

By putting your name and date here, you acknowledge that all of the above is true and you acknowledge that lying on this form is a violation of academic integrity and will result in no credit on this assignment and possible further repercussions as determined by the Khoury Academic Integrity Committee.

#### Signed: Daymian Snowden
#### Date: 10/15/2025

---