- In the **Single Responsibility Principle (SRP)**, each class should be responsible for a single part or functionality of the system.
- In the **Open Closed principle (OCP)**, software components should be open for extension but closed for modification.
- In the **Liskov Substitution Principle (LSP)**, objects of a superclass should be replaceable with objects of its subclasses without breaking the system.
- The **Interface Segregation Principle (ISP)** makes fine-grained interfaces that are client specific.
- The **Dependency Inversion Principle (DIP)**, ensures that the high-level modules are not dependent on low-level modules. In other words, one should depend upon abstraction and not concretion.

#### Single Responsibility

![[Screenshot 2025-04-15 at 8.48.24 PM.png]]

#### Open Closed Principle

![[Screenshot 2025-04-15 at 8.47.36 PM.png]]

#### Liskov Substitution Principle

- `Car` is substitutable with its superclass, `Motorized`, and `Bicycle` is substitutable with its superclass, `Manual`, without breaking the functionality.

![[Screenshot 2025-04-15 at 8.50.14 PM.png]]

#### Interface Segregation Principle

By organizing interfaces based on the dimensions of shapes, we avoid forcing 2D shape implementations to provide methods irrelevant to them.

![[Screenshot 2025-04-15 at 8.55.22 PM.png]]

#### Dependency Inversion

if any other kind of faculty is employed, they can just be easily added to the `Headmaster` without the need to explicitly inform the headmaster of it.

![[Screenshot 2025-04-15 at 8.57.11 PM.png]]