![image](https://github.com/user-attachments/assets/2be2588a-8348-4f07-9505-1d22e3ae41ae)


# SOLID Principles in Angular

## What is SOLID means in Angular?

SOLID principles are a set of guidelines for writing clean, maintainable, and reusable code. These principles were introduced by Robert C. Martin in his book “Agile Software Development, Principles, Patterns, and Practices.”

The acronym SOLID stands for:

S: Single Responsibility Principle

O: Open/Closed Principle

L: Liskov Substitution Principle

I: Interface Segregation Principle

D: Dependency Inversion Principle

In this article, we will delve into each of these principles and examine how they can enhance code organization, promote reusability, and ensure easier maintenance within Angular applications.

## Single Responsibility Principle (SRP)
The Single Responsibility Principle (SRP) is a fundamental principle of software engineering which states that a class or module should have only one reason to change. In other words, it should have only one responsibility. Violating this principle can lead to code that is difficult to maintain and understand.

## Violation of SRP
Consider a component that displays a list of products and allows the user to filter them by category. Here’s an example of what the code might look like:

![image](https://github.com/user-attachments/assets/32dde38d-94ce-46ca-a138-0667028a0fc1)

This component violates the SRP because it has two responsibilities: displaying the list of products and filtering them by category. This violates the “one reason to change” principle, as changes to the filtering behavior may affect the component’s rendering logic and vice versa.

To fix this violation, we can refactor the component into two separate components, each with its own responsibility.

## Fixing the Violation
First, we’ll create a new component that displays the list of products:

![image](https://github.com/user-attachments/assets/15b4626c-cbca-40ee-9835-a58e5750f8f7)

This component is now responsible only for displaying the list of products. We’ve removed the category filtering logic to a new component.

Next, we’ll create a new component that handles the category filtering:

![image](https://github.com/user-attachments/assets/c37c7791-2d27-4efe-99fd-d5f318ba046c)





