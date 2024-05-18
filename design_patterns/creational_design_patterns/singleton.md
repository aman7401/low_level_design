Singleton
Intent : Singleton is a creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.

Use of Singleton Class Object 

Global Access Point: Provides a single, well-known point of access to a shared resource.Just like a global variable, the Singleton pattern lets you access some object from anywhere in the program. However, it also protects that instance from being overwritten by other code.

Configuration Manager: A singleton can hold configuration settings loaded from a file or database, ensuring all parts of the application access the same configuration data.

The Singleton design pattern is used to ensure that a class has only one instance and provides a global point of access to it. Here are several ways to implement the Singleton pattern in various programming languages, particularly focusing on common methods in Java:

```java

Eager Initialization
This approach initializes the singleton instance at the time of class loading. It is simple but might lead to resource wastage if the instance is not used.

public class Singleton {
    // Private static variable to hold the single instance
    private static final Singleton INSTANCE = new Singleton();
    
    // Private constructor to prevent instantiation
    private Singleton() {
        // private constructor
    }
    
    public static Singleton getInstance() {
        return INSTANCE;
    }
}


Lazy Initialization
In this method, the instance is created only when it is needed. It can be problematic in a multi-threaded environment.


public class Singleton {
    private static Singleton instance;
    
    private Singleton() {
        // private constructor
    }
    
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

Thread-Safe Singleton (Synchronized Method)
To make the lazy initialization method thread-safe, synchronization is added to the getInstance method.


public class Singleton {
    private static Singleton instance;
    
    private Singleton() {
        // private constructor
    }
    
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

Double-Checked Locking
This method reduces the overhead of acquiring a lock by first checking the instance without synchronization.

public class Singleton {
    private static volatile Singleton instance;
    
    private Singleton() {
        // private constructor
    }
    
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}

Notes

In a singleton class, the constructor is made private to enforce the creation of only one instance of the class throughout the program. Here's why this is important:

Guarantees a Single Instance: By making the constructor private, you prevent any other part of your code from directly creating a new instance using the new keyword. This ensures that there's only one object ever created for that class.

Controlled Access:  Since the constructor is private, you control how the instance is created. Typically, a static method is provided within the class to retrieve the single instance. This allows you to manage the object's lifecycle and initialization process.

Here's an analogy: Imagine a singleton class represents a global configuration manager. You only want one configuration to exist, and making the constructor private ensures you have a single point of access and control over it.

Overall, a private constructor is a key aspect of the singleton design pattern. It enforces the core principle of having just one instance and provides a controlled way to access it.