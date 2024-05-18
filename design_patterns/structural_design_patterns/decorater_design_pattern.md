The Decorator Design Pattern is a structural design pattern that allows behavior to be added to individual objects dynamically, without affecting the behavior of other objects from the same class. It involves creating a set of decorator classes that are used to wrap concrete components.

Real-World Example of Decorator Design Pattern

Consider a video streaming platform where users can watch movies and TV shows. Each video content may have additional features or options available, such as subtitles, language preferences, video quality options, and audio enhancements.

Use Cases for the Decorator Pattern
Below are some of the use cases of Decorator Design Pattern:

Extending Functionality: When you have a base component with basic functionality, but you need to add additional features or behaviors to it dynamically without altering its structure. Decorators allow you to add new responsibilities to objects at runtime.

Multiple Combinations of Features: When you want to provide multiple combinations of features or options to an object. Decorators can be stacked and combined in different ways to create customized variations of objects, providing flexibility to users.

Legacy Code Integration: When working with legacy code or third-party libraries where modifying the existing codebase is not feasible or desirable, decorators can be used to extend the functionality of existing objects without altering their implementation.

GUI Components: In graphical user interface (GUI) development, decorators can be used to add additional visual effects, such as borders, shadows, or animations, to GUI components like buttons, panels, or windows.

Input/Output Streams: Decorators are commonly used in input/output stream classes in languages like Java. They allow you to wrap streams with additional functionality such as buffering, compression, encryption, or logging without modifying the original stream classes.

Example of Decorator Design Pattern
Below is the problem statement to understand the Decorator Design Pattern:

Suppose we are building a coffee shop application where customers can order different types of coffee. Each coffee can have various optional add-ons such as milk, sugar, whipped cream, etc. We want to implement a system where we can dynamically add these add-ons to a coffee order without modifying the coffee classes themselves.


```java

// Coffee.java
public interface Coffee {
    String getDescription();
    double getCost();
}

// PlainCoffee.java
public class PlainCoffee implements Coffee {
    @Override
    public String getDescription() {
        return "Plain Coffee";
    }

    @Override
    public double getCost() {
        return 2.0;
    }
}

// CoffeeDecorator.java
public abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;

    public CoffeeDecorator(Coffee decoratedCoffee) {
        this.decoratedCoffee = decoratedCoffee;
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription();
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost();
    }
}

// MilkDecorator.java
public class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee decoratedCoffee) {
        super(decoratedCoffee);
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription() + ", Milk";
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost() + 0.5;
    }
}

// SugarDecorator.java
public class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee decoratedCoffee) {
        super(decoratedCoffee);
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription() + ", Sugar";
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost() + 0.2;
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        // Plain Coffee
        Coffee coffee = new PlainCoffee();
        System.out.println("Description: " + coffee.getDescription());
        System.out.println("Cost: $" + coffee.getCost());

        // Coffee with Milk
        Coffee milkCoffee = new MilkDecorator(new PlainCoffee());
        System.out.println("\nDescription: " + milkCoffee.getDescription());
        System.out.println("Cost: $" + milkCoffee.getCost());

        // Coffee with Sugar and Milk
        Coffee sugarMilkCoffee = new SugarDecorator(new MilkDecorator(new PlainCoffee()));
        System.out.println("\nDescription: " + sugarMilkCoffee.getDescription());
        System.out.println("Cost: $" + sugarMilkCoffee.getCost());
    }
}

```
Advantages of the Decorator Design Pattern
Here are some of the advantages of the decorator pattern:

Open-Closed Principle: The decorator pattern follows the open-closed principle, which states that classes should be open for extension but closed for modification. This means you can introduce new functionality to an existing class without changing its source code.

Flexibility: It allows you to add or remove responsibilities (i.e., behaviors) from objects at runtime. This flexibility makes it easy to create complex object structures with varying combinations of behaviors.


Disadvantages of the Decorator Design Pattern
Here are some of the disadvantages of the Decorator pattern:

Complexity: As you add more decorators to an object, the code can become more complex and harder to understand. The nesting of decorators can make the codebase difficult to navigate and debug, especially when there are many decorators involved.

Increased Number of Classes: When using the Decorator pattern, you often end up with a large number of small, specialized decorator classes. This can lead to a proliferation of classes in your codebase, which may increase maintenance overhead.

Order of Decoration: The order in which decorators are applied can affect the final behavior of the object. If decorators are not applied in the correct order, it can lead to unexpected results. Managing the order of decorators can be challenging, especially in complex scenarios.
Reusable Code: Decorators are reusable components. You can create a library of decorator classes and apply them to different objects and classes as needed, reducing code duplication


The Decorator and Bridge design patterns are both structural patterns, but they serve different purposes and address different concerns:

Focus:

Decorator pattern focuses on enhancing individual objects' functionality dynamically.
Bridge pattern focuses on decoupling abstraction from implementation, allowing them to vary independently.

In summary, the Decorator pattern is about adding functionality to individual objects, while the Bridge pattern is about separating abstraction from implementation to allow independent evolution.
