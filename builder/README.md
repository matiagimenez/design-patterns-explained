# Builder

The **builder** pattern separates the construction of a complex object from its representation so that the same construction process can create different representations of the object.

It provides an elegant solution to the problem of creating complex objects with multiple components.

![image](https://github.com/user-attachments/assets/3906e7a5-642d-444e-ad13-69bd4633ea44)

## Introduction

Imagine you have a class that includes in its behaviour the creation of a complex object, with various configurations.

#### How this class can be _simplified_?

The **builder** pattern solves this problem by abstracting the construction process into separate classes, resulting in cleaner and more maintainable code. In other words, applying the pattern means following the _separation of concerns_ principle, separating the construction process from the products internal structure.

Without the **builder** pattern, you might end up with a constructor that takes numerous parameters, leading to confusing and complex code.

Implementating the **builder** pattern, keeps encapsulated the code for construction, allowing you to vary a product's internal representation.

The main drawback of the **builder** pattern is that requires creating a concrete builder for each unique configuration of the "product".

## How to recognize a builder pattern implementation?

The **builder** pattern can be recognized in a class, which has a _single creation method_ and _several methods to configure_ the resulting object. **Builder class methods often support chaining**.

The **builder** and factory patterns are very similar in the fact they both instantiate new objects at runtime. The difference is when the process of creating the object is more complex, so rather that the factory returning a new instance of object, it calls the builders director constructor method that goes through a more complex construction process involving several steps. In the end, both return an object instance.

### Real world analogy

Consider a restaurant. The creation of "today's meal" is a factory pattern, because you tell the kitchen "get me today's meal" and the kitchen (factory) decides what object to generate, based on hidden criteria.

The **builder** appears if you order a custom pizza. In this case, the waiter tells the chef (builder) "I need a pizza; add cheese, onions and bacon to it!" Thus, the builder exposes the attributes the generated object should have, but hides how to set them.

## How to know if you can apply the pattern in your project?

A **builder** is useful when constructing an object requires multiple steps, especially when many parameters are involved, some of which may be optional.

In such cases, using a class constructor can become confusing, as handling numerous optional arguments makes it harder to validate the object's state. This increases the risk of creating an instance with an invalid combination of parameters.

The builder pattern addresses this by allowing parameters to be set step by step before returning a fully constructed object. While this approach requires a *concrete builder* implementation for each parameter combination, it ensures a consistent and valid object representation.

Another advantage of builders is handling complex object initialization, where method calls must follow a specific sequence and intermediate objects need to be generated. Attempting to manage this within a constructor can be a real pain, and relying on a separate initialization method that one must remember to call is error-prone. Delegating construction to a **builder** simplifies this process by ensuring the object transitions through the necessary states in a controlled manner.

## Key components

The **builder** pattern typically involves the following components.

-   **Product**. This is the complex object that you want to create. It contains various parts or components, so several representations of this object exists.

-   **Builder**. An abstract interface that defines the methods for building each part of the product.

-   **Concrete builders**. Concrete classes that implement the builder interface. Each concrete builder is responsible for constructing a specific representation of the product.

-   **Director**. Coordinates the construction process using the builder interface. It knows the specific order and combination of steps required to build the product. The Director is only responsible for executing the building steps in a particular sequence. The Director works with any builder instance that the client code passes to it.

#### Strictly speaking, the director class is optional, since the client can control builders directly.

## Conceptual example

```python
from abc import ABC, abstractmethod

class Builder(ABC):
    """
    The Builder interface specifies methods for creating the different parts of
    the Product objects.
    """

    @property
    @abstractmethod
    def product(self) -> None:
        pass

    @abstractmethod
    def produce_part_a(self) -> None:
        pass

    @abstractmethod
    def produce_part_b(self) -> None:
        pass

    @abstractmethod
    def produce_part_c(self) -> None:
        pass


class ConcreteBuilder(Builder):
    """
    The Concrete Builder classes follow the Builder interface and provide
    specific implementations of the building steps. Your program may have
    several variations of Builders, implemented differently.
    """
    product: Product

    def __init__(self) -> None:
        """
        A fresh builder instance should contain a blank product object, which is
        used in further assembly.
        """
        self.reset()


    def reset(self) -> None:
        """
        A fresh builder instance should contain a blank product object, which is
        used in further assembly.
        """
        self._product = Product()

    @property
    def product(self) -> Product:
        """
        Concrete Builders are supposed to provide their own methods for
        retrieving results. That's because various types of builders may create
        entirely different products that don't follow the same interface.

        Usually, after returning the end result to the client, a builder
        instance is expected to be ready to start producing another product.
        That's why it's a usual practice to call the reset method at the end of
        the `getProduct` method body. However, this behavior is not mandatory,
        and you can make your builders wait for an explicit reset call from the
        client code before disposing of the previous result.
        """
        product = self._product
        self.reset()
        return product

    def produce_part_a(self) -> None:
        self._product.add("Part A1")

    def produce_part_b(self) -> None:
        self._product.add("Part B1")

    def produce_part_c(self) -> None:
        self._product.add("Part C1")


class Product():
    """
    It makes sense to use the Builder pattern only when your products are quite
    complex and require extensive configuration.

    Unlike in other creational patterns, different concrete builders can produce
    unrelated products. In other words, results of various builders may not
    always follow the same interface.
    """
    parts: list[str]

    def __init__(self) -> None:
        self.parts = []

    def add(self, part: str) -> None:
        self.parts.append(part)

class Director:
    """
    The Director is only responsible for executing the building steps in a
    particular sequence. It is helpful when producing products according to a
    specific order or configuration. Strictly speaking, the Director class is
    optional, since the client can control builders directly.
    """

    def __init__(self) -> None:
        self._builder = None

    @property
    def builder(self) -> Builder:
        return self._builder

    @builder.setter
    def builder(self, builder: Builder) -> None:
        """
        The Director works with any builder instance that the client code passes
        to it. This way, the client code may alter the final type of the newly
        assembled product.
        """
        self._builder = builder

    """
    The Director can construct several product variations using the same
    building steps.
    """

    def build_minimal_viable_product(self) -> None:
        self.builder.produce_part_a()

    def build_full_featured_product(self) -> None:
        self.builder.produce_part_a()
        self.builder.produce_part_b()
        self.builder.produce_part_c()


if __name__ == "__main__":
    """
    The client code creates a builder object, passes it to the director and then
    initiates the construction process. The end result is retrieved from the
    builder object.
    """

    builder = ConcreteBuilder()
    director = Director()
    director.builder = builder

    print("Standard basic product: ")
    director.build_minimal_viable_product()
    print(f"Product: {builder.product}") # Product(parts=["Part A1"])

    print("Standard full featured product: ")
    director.build_full_featured_product()
    print(f"Product: {builder.product}") # Product(parts=["Part A1", "Part B1", "Part C1"])

    # Remember, the Builder pattern can be used without a Director class.
    print("Custom product: ")
    builder.produce_part_a()
    builder.produce_part_b()
    print(f"Product: {builder.product}") # Product(parts=["Part A1", "Part B1"])

```

## References

-   📚 [Design Patterns in Python: Builder](https://medium.com/@amirm.lavasani/design-patterns-in-python-builder-0732552324b1)
-   📚 [Builder in Python](https://refactoring.guru/design-patterns/builder/python/example)
-   📼 [Builder: Design Patterns in Python](https://youtu.be/pMadA6F4zGU)
-   📼 [Builder Design Pattern Explained in 10 Minutes](https://youtu.be/oP76NM4qZhw)
