#dart 
Dart follows four main OOP principles:

1. **Encapsulation**

2. **Abstraction**

3. **[[Inheritance]]**

4. **Polymorphism**


**1. Encapsulation (Data Hiding)**
Encapsulation means restricting direct access to the internal state of an object and requiring all interactions to happen through methods. In Dart, we use **private variables** (prefix with _) and public methods to control access.

```dart
class BankAccount {
  String _accountHolder; // Private variable
  double _balance; // Private variable

  BankAccount(this._accountHolder, this._balance);

  // Public method to access balance
  double get balance => _balance;

  // Public method to deposit money
  void deposit(double amount) {
    if (amount > 0) {
      _balance += amount;
      print("Deposited \$${amount}. New balance: \$$_balance");
    }
  }

  // Public method to withdraw money
  void withdraw(double amount) {
    if (amount > 0 && amount <= _balance) {
      _balance -= amount;
      print("Withdrew \$${amount}. Remaining balance: \$$_balance");
    } else {
      print("Insufficient balance.");
    }
  }
}

void main() {
  var account = BankAccount("John Doe", 1000);
  account.deposit(500);
  account.withdraw(200);
  print("Balance: ${account.balance}"); // Accessing balance through getter
}
```
**Encapsulation prevents direct modification of** _balance, ensuring controlled access.

2.**Abstraction (Hiding Complexity)**
Abstraction allows us to hide complex implementation details and show only the necessary parts. In Dart, we use **abstract classes** to enforce abstraction.

```dart
abstract class Vehicle {
  void start(); // Abstract method (must be implemented by subclasses)
  void stop();
}

class Car extends Vehicle {
  @override
  void start() => print("Car is starting...");

  @override
  void stop() => print("Car is stopping...");
}

void main() {
  Car myCar = Car();
  myCar.start();
  myCar.stop();
}
```
The **abstract class** Vehicle defines the structure, and the **concrete class** Car **implements it**.

**3. Inheritance (Code Reusability)**
Inheritance allows a class to inherit properties and behaviors from another class, promoting **code reuse**.

```dart
class Animal {
  void eat() => print("Animal is eating...");
}

class Dog extends Animal {
  void bark() => print("Dog is barking...");
}

void main() {
  Dog myDog = Dog();
  myDog.eat(); // Inherited from Animal
  myDog.bark(); // Defined in Dog
}
```
Dog **inherits** the eat() method from Animal but also has its own bark() method.

**4. Polymorphism (Multiple Forms)**
Polymorphism allows a subclass to provide its own implementation of a method that is already defined in its superclass.

```dart
class Animal {
  void makeSound() => print("Animal makes a sound...");
}

class Dog extends Animal {
  @override
  void makeSound() => print("Dog barks...");
}

class Cat extends Animal {
  @override
  void makeSound() => print("Cat meows...");
}

void main() {
  Animal myDog = Dog();
  Animal myCat = Cat();

  myDog.makeSound(); // Dog barks...
  myCat.makeSound(); // Cat meows...
}
```
The same method makeSound() behaves **differently for different subclasses**.

**Principle** **Description** **Example**

**Encapsulation** Hides internal data and provides controlled access. Private variables _balance, public getters/setters.

**Abstraction** Hides complexity and exposes only essential details. abstract class Vehicle forces subclasses to implement methods.

**Inheritance** Enables code reuse by inheriting methods and properties. Dog extends Animal and inherits eat().

**Polymorphism** Allows the same method to have different behaviours. makeSound() behaves differently in Dog and Cat.
