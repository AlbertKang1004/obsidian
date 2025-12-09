### \[M0] Java and Git

- [ ] Which git commands did we discuss during lecture or use in a lab assignment?
- [ ] What are the parts of a Java class? (class declaration, fields, constructor, etc.)
- [ ] What are the Java naming conventions?
- [ ] How do you declare a class, a method, a variable? (including accessibility modifiers, `static`, etc.)
- [ ] What does a constructor do?
    - [ ] When is the default constructor provided?
    - [ ] What does "super();" do?

### \[M1] More Java and Git

- [ ] What are keywords that we have seen in the Java quizzes and the lecture and lab activities? (including `this`, `new`, `throw`, `throws`, etc.)
- [ ] How do overloading, overriding, and shadowing work?
- [ ] How does inheritance work in Java?
- [ ] What is the difference between an abstract class and an interface?
    - [ ] When would you want to use each?
- [ ] What are the java.swing classes we used during lecture and lab?
    - [ ] What do they correspond to visually when you look at the GUI?
- [ ] How do you translate a UML diagram into code or code into a UML diagram using the symbols on [this slide](https://q.utoronto.ca/courses/394773/files/40549821 "Link")?
- [ ] How do we use git branches?
- [ ] What is a pull request, and what are the steps to creating one?

### \[M2] SOLID and Design

- [ ] What do we mean by "high cohesion, low coupling"?
- [ ] What does it mean for class A to depend on class B?
- [ ] What are each of the SOLID principles and how can you summarize each one?
    - [ ] How do you identify code that violates each principle?
    - [ ] Why is it useful to follow each of the SOLID principles?
- [ ] What is a user story and who is the target audience?
- [ ] How can we identify stakeholders in our program?
- [ ] What is an API and how do you use one in Java?
- [ ] What is JSON and how is it relevant to an API?

### \[M3] Clean Architecture

- [x] What is a use case and who is the target audience?
- [x] How do you translate a user story to a set of 1 or more use cases?
- [ ] What are the layers of Clean Architecture?
    - [ ] Which layer contains the Enterprise Business Rules and what are they?
    - [ ] Which layer contains the Application Business Rules and what are they?
    - [ ] Which layer adapts elements outside of the program so that they can interact with the main part of the program?
- [x] What are the roles of and interfaces implemented by each kind of class in Clean Architecture?
    - [x] Which layer contains each class?
    - [x] How can you identify the role of a class by looking at the code?
- [x] What is the Clean Architecture Dependency Rule?
    - [x] How is it related to the "D" in SOLID?
- [x] Which of the SOLID principles are necessarily followed by any program that adheres to Clean Architecture?
- [x] How do you test a Use Case Interactor?
- [x] Which classes are "mocked" by a unit test in order to test a Use Case Interactor?
- [x] How can we determine which use cases are required in a program based on its user stories?
- [x] What is the flow of information through the Clean Architecture — how does information get from the user at the keyboard/mouse into the program, get modified, get stored within and outside of the program, and cause the appropriate changes to the User Interface?
### \[M4\] Design Patterns

- [x] What is a design pattern?
- [x] Each pattern solves a problem. What problem is solved by each of these patterns and how is it solved? 
    - [x] Creational patterns: Builder, Factory
    - [x] Behavioural patterns: Strategy, Observer
    - [x] Structural patterns: Façade, Adapter
- [x] What are the classes involved in each of the above design patterns and what (if any) is their relationship?
- [x] What is an anti-pattern? What might the anti-pattern of each design pattern above look like?
- [x] What is the difference between a "refactoring technique" and any other modification to a class or program?
- [x] Explain how each refactoring technique works (note that most of these are simple edits):
    - [ ] Extract Method
    - [ ] Change Method Declaration
    - [ ] Encapsulate Fields
    - [ ] Split Loop
    - [ ] Slide Statements
    - [x] Replace Constructor with Builder
    - [x] Replace Constructor with Factory Method
- [ ] Which design patterns are built into Clean Architecture? In other words, if you implement Clean Architecture, which design patterns will necessarily appear in your code?
### [M5] Ethics and Regex

- [ ] What is a speech act?
- [ ] What is the difference between material and relational harm?
    - [ ] How can you identify each?
- [x] What are the similarities and differences between the medical and social models of disability?
- [ ] Why and how can we use the Principles of Universal Design when designing software?
- [ ] What are the basic regular expression (regex) symbols that we covered in the reading and/or in lecture?
- [ ] How can we write a regular expression that matches a set of Strings?
- [ ] How can we find a String that conforms to a given regular expression?
- [ ] What do we have to do to a regular expression to use it in a Java program?
- [ ] What are three ways of checking if a String conforms to a regular expression in Java?