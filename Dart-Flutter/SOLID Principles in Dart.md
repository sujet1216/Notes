#dart 
**SOLID** is a set of five design principles that make code more **maintainable, scalable, and testable**. It stands for:

1. **S** - Single Responsibility Principle (SRP)

2. **O** - Open/Closed Principle (OCP)

3. **L** - Liskov Substitution Principle (LSP)

4. **I** - Interface Segregation Principle (ISP)

5. **D** - Dependency Inversion Principle (DIP)

**1. Single Responsibility Principle (SRP)**
💡 **Each class should have only one reason to change.**

A class should only have **one responsibility** (i.e., handle a single task).
**❌ Bad Example (Violating SRP)**
```dart
class Order {
  void placeOrder() => print("Order placed");
  void saveToDatabase() => print("Order saved to database"); // ❌ Handles database logic
  void sendEmail() => print("Email sent to customer"); // ❌ Handles email logic
}
```

Here, Order does too many things:
• Placing an order

• Saving to the database

• Sending an email

**✅ Good Example (Following SRP)**
We **split responsibilities** into separate classes:
```dart
class Order {
  void placeOrder() => print("Order placed");
}

class OrderRepository {
  void saveToDatabase() => print("Order saved to database");
}

class EmailService {
  void sendEmail() => print("Email sent to customer");
}

void main() {
  var order = Order();
  var repository = OrderRepository();
  var emailService = EmailService();

  order.placeOrder();
  repository.saveToDatabase();
  emailService.sendEmail();
}
```
🔹 **Now, each class has a single responsibility.**

**2. Open/Closed Principle (OCP)**

💡 **A class should be open for extension but closed for modification.**
Instead of modifying existing code, we should extend it.

**❌ Bad Example (Violating OCP)**

```dart
class Discount {
  double applyDiscount(double price, String type) {
    if (type == "percentage") return price * 0.9;
    if (type == "fixed") return price - 10; // ❌ Adding more types requires modifying this class
    return price;
  }
}
```
Every time we add a new discount type, we **modify** the class.

**✅ Good Example (Following OCP)**
We use **inheritance and polymorphism**:

```dart
abstract class Discount {
  double applyDiscount(double price);
}

class PercentageDiscount extends Discount {
  @override
  double applyDiscount(double price) => price * 0.9;
}

class FixedDiscount extends Discount {
  @override
  double applyDiscount(double price) => price - 10;
}

void main() {
  Discount discount = PercentageDiscount();
  print("Final price: ${discount.applyDiscount(100)}");
}
```
🔹 **New discount types can be added without modifying existing code.**

**3. Liskov Substitution Principle (LSP)**

💡 **Subclasses should be able to replace the parent class without breaking the system.**
**❌ Bad Example (Violating LSP)**
```dart
class Bird {
  void fly() => print("Bird is flying");
}

class Penguin extends Bird {
  @override
  void fly() => throw Exception("Penguins can't fly!"); // ❌ Violates LSP
}
```
**Problem:**

• Penguin **inherits** fly() **but cannot fly**.
• This breaks the principle, as Penguin **can’t fully replace** Bird.

**✅ Good Example (Following LSP)**

We create a more specific hierarchy:
```dart
abstract class Bird {}

class FlyingBird extends Bird {
  void fly() => print("Bird is flying");
}

class NonFlyingBird extends Bird {
  void walk() => print("Bird is walking");
}

class Sparrow extends FlyingBird {}

class Penguin extends NonFlyingBird {}

void main() {
  Sparrow().fly();
  Penguin().walk();
}
```
🔹 Now, **each bird behaves correctly** without breaking substitution.

**4. Interface Segregation Principle (ISP)**

💡 **A class should not be forced to implement interfaces it does not use.**
  
**❌ Bad Example (Violating ISP)**
```dart
abstract class Worker {
  void work();
  void eat(); // ❌ Not all workers need this
}

class Developer implements Worker {
  @override
  void work() => print("Coding...");

  @override
  void eat() => print("Taking a break..."); // ❌ Unnecessary
}

class Robot implements Worker {
  @override
  void work() => print("Robot is working...");

  @override
  void eat() => throw Exception("Robots don't eat!"); // ❌ Problem
}
```
**Problem:**

• Robot **is forced** to implement eat(), which doesn’t make sense.

**✅ Good Example (Following ISP)**

We split interfaces into **smaller ones**:

```dart
abstract class Workable {
  void work();
}

abstract class Eatable {
  void eat();
}

class Developer implements Workable, Eatable {
  @override
  void work() => print("Coding...");

  @override
  void eat() => print("Taking a break...");
}

class Robot implements Workable {
  @override
  void work() => print("Robot is working...");
}
```
🔹 Now, Robot **doesn’t have to implement** eat(), following ISP.

**5. Dependency Inversion Principle (DIP)**

💡 **High-level modules should not depend on low-level modules. Both should depend on abstractions.**

**❌ Bad Example (Violating DIP)**

```dart
class MySQLDatabase {
  void saveData() => print("Data saved to MySQL");
}

class DataService {
  MySQLDatabase db = MySQLDatabase(); // ❌ Direct dependency

  void save() => db.saveData();
}
```

**Problem:**

• DataService is **tightly coupled** with MySQLDatabase.
• If we want to switch to another database (e.g., PostgreSQL), we must modify DataService.

**✅ Good Example (Following DIP)**

We use **abstraction (interfaces)**:

```dart
abstract class Database {
  void saveData();
}

class MySQLDatabase implements Database {
  @override
  void saveData() => print("Data saved to MySQL");
}

class PostgreSQLDatabase implements Database {
  @override
  void saveData() => print("Data saved to PostgreSQL");
}

class DataService {
  final Database db;
  DataService(this.db); // ✅ Dependency is injected

  void save() => db.saveData();
}

void main() {
  var service = DataService(MySQLDatabase());
  service.save();

  var newService = DataService(PostgreSQLDatabase());
  newService.save();
}
```
🔹 **Now, we can switch databases without modifying** DataService**.**

**S** - Single Responsibility A class should have only **one reason to change** Split responsibilities into separate classes

**O** - Open/Closed A class should be **open for extension but closed for modification** Use **inheritance & polymorphism**

**L** - Liskov Substitution Subclasses should **replace** base class without breaking behavior Use **proper hierarchy**

**I** - Interface Segregation No class should be forced to implement methods it **does not use** Use **multiple smaller interfaces**

**D** - Dependency Inversion High-level modules should **not depend on low-level modules** Use **abstraction & dependency injection**

Applying SOLID principles makes your Dart code **cleaner, more maintainable, and scalable**.