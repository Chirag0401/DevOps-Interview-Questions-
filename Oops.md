Interviewer: “You have 2 minutes. Explain all 7 of OOPS concepts to me.”

My answer: Challenge accepted, Let’s go!

 1️⃣ Encapsulation
- Bundles data and methods in a single unit.
- Protects data from outside interference and misuse.

Example: A class `Car` with private attributes like `speed` and `fuel`, and public methods like `accelerate` and `brake`.

 2️⃣ Abstraction
- Hides complex implementation details, exposing only the necessary information.
- Simplifies code interaction and reduces complexity.

Example: A `Database` interface with methods `connect` and `query`, hiding the details of SQL or NoSQL operations.

 3️⃣ Inheritance
- Allows a class to inherit properties and behaviors from another class.
- Promotes code reuse and reduces redundancy.

Example: A `Vehicle` class inherited by `Car` and `Bike` classes, sharing common properties like `engine` and methods like `start`.

 4️⃣ Polymorphism
- Objects of different types can be treated as the same type.
- Enables flexible and modular code.

Example: A method `draw` that can work with objects of `Circle`, `Square`, and `Triangle` classes.

 5️⃣ Composition
- Combines simpler objects to create complex ones.
- Enhances code maintainability and flexibility.

Example: A `House` class composed of `Room` objects like `Kitchen`, `Bedroom`, and `Bathroom`.

 6️⃣ Association
- Relationship between two objects where one uses or depends on the other.
- Defines how objects interact with each other.

Example: A `Library` class is associated with `Book` class where the library contains books.

 7️⃣ Dependency Inversion
- High-level modules should not depend on low-level modules; 
- both should depend on abstractions.
- Reduces coupling between code and enhances flexibility.

Example: A `PaymentProcessor` class depends on an `IPaymentGateway` interface instead of concrete implementations like `Paypal` or `Stripe`.
