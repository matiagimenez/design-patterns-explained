# Builder

The **builder** pattern separates the construction of a complex object from its representation, allowing to use the same construction process to create objects with different representations.

It provides an elegant solution to the problem of creating complex objects with multiple components.

### Introduction

Imagine you have a class that includes in its behaviour the creation of a complex object, with various configurations.

#### How this class can be _simplified_?

The **builder** pattern solves this problem by abstracting the construction process into separate classes, resulting in cleaner and more maintainable code. In other words, applying the pattern means following the _separation of concerns_ principle, separating the construction process from the products internal structure.

Without the **builder** pattern, you might end up with a constructor that takes numerous parameters, leading to confusing and complex code.

Another benefit is that now, adding new components or variations of the product, is straightforward by extending the builder classes.

### Key components

The **builder** pattern typically involves the following components.

-   **Product**. This is the complex object that you want to create. It contains various parts or components, so several representations of this object exists.

-   **Builder**. An abstract interface that defines the methods for building each part of the product.

-   **Concrete builders**. Concrete classes that implement the builder interface. Each concrete builder is responsible for constructing a specific representation of the product.

-   **Director**. Coordinates the construction process using the builder interface. It knows the specific order and combination of steps required to build the product. Is common that this class has a `construct()` or `create()` method that creates the customized object.

### How to recognize a builder pattern implementation?

The **builder** pattern can be recognized in a class, which has a _single creation method_ and _several methods to configure_ the resulting object. Builder methods often support chaining.

The **builder** and factory patterns are very similar in the fact they both instantiate new objects at runtime. The difference is when the process of creating the object is more complex, so rather that the factory returning a new instance of object, it calls the builders director constructor method that goes through a more complex construction process involving several steps. In the end, both return an object instance.

## References

-   📚 [Design Patterns in Python: Builder](https://medium.com/@amirm.lavasani/design-patterns-in-python-builder-0732552324b1)
-   📚 [Builder in Python](https://refactoring.guru/design-patterns/builder/python/example)
-   📼 [Builder: Design Patterns in Python](https://youtu.be/pMadA6F4zGU)
-   📼 [Builder Design Pattern Explained in 10 Minutes](https://youtu.be/oP76NM4qZhw)
