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

#

### Single Responsibility Principle (SRP)
The Single Responsibility Principle (SRP) is a fundamental principle of software engineering which states that a class or module should have only one reason to change. In other words, it should have only one responsibility. Violating this principle can lead to code that is difficult to maintain and understand.

### Violation of SRP
Consider a component that displays a list of products and allows the user to filter them by category. Here’s an example of what the code might look like:

![image](https://github.com/user-attachments/assets/32dde38d-94ce-46ca-a138-0667028a0fc1)

This component violates the SRP because it has two responsibilities: displaying the list of products and filtering them by category. This violates the “one reason to change” principle, as changes to the filtering behavior may affect the component’s rendering logic and vice versa.

To fix this violation, we can refactor the component into two separate components, each with its own responsibility.

### Fixing the Violation
First, we’ll create a new component that displays the list of products:

![image](https://github.com/user-attachments/assets/15b4626c-cbca-40ee-9835-a58e5750f8f7)

This component is now responsible only for displaying the list of products. We’ve removed the category filtering logic to a new component.

Next, we’ll create a new component that handles the category filtering:

![image](https://github.com/user-attachments/assets/c37c7791-2d27-4efe-99fd-d5f318ba046c)

This component is now responsible only for handling the category filtering. It updates the selected category and calls the getProductsByCategory() method of the ProductService to update the list of products.

Finally, we’ll update the app.component.html file to include both components:

![image](https://github.com/user-attachments/assets/99edeaba-42a2-4fb3-9559-10f52fda63dd)

The app-product-filter component emits a categorySelected event when a new category is selected. This event is handled by the app-product-list component, which calls its filterByCategory() method with the selected category.

By splitting the responsibilities into two separate components, we’ve successfully refactored our code to comply with the Single Responsibility Principle. Each component now has a single responsibility, making our code more modular and easier to maintain.

In addition to complying with the SRP, this refactoring also follows the Separation of Concerns principle, which advocates for dividing a software system into separate modules, each addressing a separate concern.

Adhering to the SRP is crucial for writing maintainable, extensible, and reusable code. By keeping each module’s responsibilities separated, we can avoid coupling and ensure that any changes to one module do not affect others unnecessarily.

Real-World Example: Email Sending Service

Suppose you have an Invoice class that calculates the total, formats the invoice, and sends it via email. This class violates SRP since it's handling multiple responsibilities (calculation, formatting, sending email).

Solution: Split the class into three separate classes:

InvoiceCalculator for calculating the invoice total.

InvoiceFormatter for formatting the invoice.

EmailService for sending the email.

Application: SRP ensures that each class has one reason to change, making the system more maintainable and easier to test.

#

### Open/Closed Principle (OCP)

The Open/Closed Principle states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, we should be able to add new functionality without modifying existing code. This principle helps in reducing code coupling, improving code scalability, and making the code more reusable.

OCP can be applied using inheritance and interfaces. For example, we can create a base component or service that contains common functionality and then create child components or services that inherit from the base component or service. We can also create interfaces for components or services that define a set of methods or properties that must be implemented.

### Violating the Open/Closed Principle

Consider, we have a component that displays a list of users. The users are retrieved and displayed in a table. The table has three columns: name, email, and phone number. We have created a UserListComponent to display this list. Initially, the component looks like this:

![image](https://github.com/user-attachments/assets/014c479f-6355-418a-b279-b8bc52a801a1)

In the template file user-list.component.html, we have the following code:

![image](https://github.com/user-attachments/assets/06acf844-6a97-430d-9d98-52c9c0334f53)

Everything works fine, and we can see the list of users displayed in a table with three columns.

Now, suppose we want to add a new feature to the application, which is to allow users to view additional details for each user. We want to display the user’s address, city, and state. We can simply modify the UserListComponent to add these columns to the table. Here’s how we can do it:

![image](https://github.com/user-attachments/assets/68309a66-1c90-433c-ac71-a171d4c7791b)

![image](https://github.com/user-attachments/assets/1ffe097b-32fd-4368-848b-1e849d0225d3)

This code violates the OCP because we have modified the existing component to add new functionality. If we want to add more features to the application, we will have to keep modifying the UserListComponent, which makes it difficult to maintain and scale.

### Fixing the violation

To fix the violation of the OCP, we need to separate the concerns of displaying the list of users and displaying the details of each user. We can create a new component called UserDetailComponent to display the additional details for each user. Here’s how we can do it:

![image](https://github.com/user-attachments/assets/7963832c-5950-4ee1-81a1-948cd4755a01)

In the UserListComponent, we can now use the UserDetailComponent to display the additional details for each user. Here’s how we can do it:

![image](https://github.com/user-attachments/assets/1d35b0c8-7da1-423d-a9af-5c66b51b6f92)

![image](https://github.com/user-attachments/assets/4dc37c31-6574-44d5-800d-4f82eabeddc2)

In this new implementation, the UserListComponent is responsible for displaying the list of users, while the UserDetailComponent is responsible for displaying the details of each user. The UserListComponent doesn’t need to be modified to add new functionality because the UserDetailComponent can be easily extended to display additional details.

Real-World Example: Payment Processing System

You have a PaymentProcessor class that handles different payment methods (credit card, PayPal, bank transfer). If you add a new payment method, you'd need to modify the class, violating OCP.

Solution: Use an interface like IPaymentMethod and let each payment method (e.g., CreditCardPayment, PaypalPayment) implement it.

Application: The PaymentProcessor class remains open for extension (adding new payment methods) but closed for modification (no need to change the existing class). This prevents breaking existing functionality when adding new features.

#

### Liskov Substitution Principle (LSP)

The Liskov Substitution Principle (LSP) is a fundamental concept in software engineering that is essential for designing and implementing maintainable and extensible systems. LSP states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. Violating the LSP can lead to unexpected behavior and bugs.

### Violating LSP

![image](https://github.com/user-attachments/assets/f9784c6e-0651-49f6-a782-4ff0fb00d410)

In this example, Ostrich is a subclass of Animal that overrides the move() method to reflect the fact that ostriches cannot fly. However, when we pass an instance of Ostrich to the moveAnimal() function, we get unexpected behavior because the move() method of Ostrich does not behave the same way as the move() method of Animal. This violates the LSP because Ostrich is not a true substitute for Animal.

To fix the violation, we can modify the Ostrich class to behave more like Animal:

![image](https://github.com/user-attachments/assets/9690ded8-964a-4966-9f07-9cbf4a4b8e8d)

In this updated implementation, we have added a fly() method to the Ostrich class that throws an error because ostriches cannot fly. This ensures that Ostrich behaves like Animal and can be used as a substitute for it without affecting the correctness of the program.

The Liskov Substitution Principle is an important principle in software engineering that helps us design maintainable and extensible systems. Violating the LSP can lead to unexpected behavior and bugs, but these violations can be fixed by ensuring that subclasses behave like their superclasses.

Real-World Example: User Authentication System

You have a User class for normal users and an AdminUser class for administrators. If you replace a User object with an AdminUser object, the system should still function correctly without changing the behavior.

Violation: If AdminUser has extra methods (e.g., deleteUser()) that are not applicable to normal User objects, it violates LSP.

Solution: Ensure that both User and AdminUser conform to the same interface (e.g., IUser) and only add additional methods where necessary. The base class functionality should be consistent across subclasses.

Application: LSP ensures that derived classes can replace base classes without altering the expected behavior, improving code reliability.

#

### Interface Segregation Principle (ISP)

The Interface Segregation Principle (ISP) is a software development principle that states that a software component should not be forced to depend on interfaces that it does not use. In other words, clients should not be forced to depend on methods they do not use. This principle helps to reduce coupling between components and makes code more modular, flexible, and maintainable.

ISP can be violated when a component has a dependency on a service that provides more methods than the component needs. This can lead to unnecessary coupling between the component and the service, making it difficult to modify either component without affecting the other. Additionally, it can cause performance issues as the component may be forced to load unnecessary methods from the service.

To demonstrate this, let’s consider an example where a component needs to retrieve data from a service. The service provides several methods, including ones that are not required by the component.

![image](https://github.com/user-attachments/assets/365dea48-2666-4b2c-9a95-170e0080f4c9)

The component only needs to retrieve items from the service, so it should only depend on the getItems method. However, if the component is written as follows:

![image](https://github.com/user-attachments/assets/4a10fe7f-cb65-4c36-8793-def1c6e4e1c9)







