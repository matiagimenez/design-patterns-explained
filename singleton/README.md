# Singleton

The **Singleton** pattern ensures that only one object of its kind exists and provides a single point of access to it for any other code. For achieving this, you have to restrict the instantiation of a class.

![singleton](https://github.com/user-attachments/assets/fe89cab8-db18-4276-b10a-c8bbe9db0c7a)

## Introduction

#### Why would anyone want to control how many instances a class has?

The most common reason for this is to control access to some shared resource — for example, a database or a file.

Just like a global variable, the **Singleton** pattern lets you access some object from anywhere in the program. However, it also protects that instance from being overwritten by other code.

## How to recognize a singleton pattern implementation?
The **Singleton** pattern can be implemented following different approaches, but all of them have the following common concepts.

-   _Private constructor_ to restrict instantiation of the class from other classes.
-   _Private variable of the same class_ that is the only instance of the class.
-   _Public static method that returns the instance of the class_. Under the hood, this method calls the private constructor to create an object and saves it in a static field. All following calls to this method return the cached object working as a global access point

### Real world analogy

A great real-world analogy is a central bank. Every country has only one central bank responsible for controlling monetary policy, regulating the financial system, and issuing currency. No matter how many financial institutions exist, they all rely on this single entity for economic stability. If someone attempted to create another central bank, it wouldn’t be allowed, as the system is designed to have only one official authority.

Similarly, in software design, the **Singleton** pattern ensures that a class has only one instance and provides a single, global point of access to it, preventing the creation of multiple instances that could disrupt system consistency.

## How to know if you can apply the pattern in your project?

## Key components

## Benefits and Trade-offs

-   ✅
-   ❌

## References

-   📚 [Singleton in Python](https://refactoring.guru/design-patterns/singleton/python/example)
-   📼 [Mastering the Singleton Design Pattern in Python](https://youtu.be/Awoh5-Yr6SE)
-   📼 [Making singletons in Python](https://youtu.be/sppHANksoG4)
