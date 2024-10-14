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







