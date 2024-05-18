The Builder Design Pattern is a creational pattern used in software design to construct a complex object step by step. It allows the construction of a product in a step-by-step fashion, where the construction process can vary based on the type of product being built. The pattern separates the construction of a complex object from its representation, allowing the same construction process to create different representations.

```java

// Product
class Computer {
    private String cpu;
    private String ram;
    private String storage;

    public void setCPU(String cpu) {
        this.cpu = cpu;
    }

    public void setRAM(String ram) {
        this.ram = ram;
    }

    public void setStorage(String storage) {
        this.storage = storage;
    }

    public void displayInfo() {
        System.out.println("Computer Configuration:");
        System.out.println("CPU: " + cpu);
        System.out.println("RAM: " + ram);
        System.out.println("Storage: " + storage);
        System.out.println();
    }
}

// Builder interface
interface Builder {
    void buildCPU();
    void buildRAM();
    void buildStorage();
    Computer getResult();
}

// ConcreteBuilder for Gaming Computers
class GamingComputerBuilder implements Builder {
    private Computer computer = new Computer();

    @Override
    public void buildCPU() {
        computer.setCPU("High-Performance Gaming CPU");
    }

    @Override
    public void buildRAM() {
        computer.setRAM("16GB DDR4");
    }

    @Override
    public void buildStorage() {
        computer.setStorage("1TB SSD");
    }

    @Override
    public Computer getResult() {
        return computer;
    }
}

// ConcreteBuilder for Workstation Computers
class WorkstationComputerBuilder implements Builder {
    private Computer computer = new Computer();

    @Override
    public void buildCPU() {
        computer.setCPU("Multi-Core Workstation CPU");
    }

    @Override
    public void buildRAM() {
        computer.setRAM("32GB ECC RAM");
    }

    @Override
    public void buildStorage() {
        computer.setStorage("2TB SSD");
    }

    @Override
    public Computer getResult() {
        return computer;
    }
}

// Director
class ComputerDirector {
    public void construct(Builder builder) {
        builder.buildCPU();
        builder.buildRAM();
        builder.buildStorage();
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        ComputerDirector director = new ComputerDirector();

        // Building a Gaming Computer
        GamingComputerBuilder gamingBuilder = new GamingComputerBuilder();
        director.construct(gamingBuilder);
        Computer gamingComputer = gamingBuilder.getResult();
        gamingComputer.displayInfo();

        // Building a Workstation Computer
        WorkstationComputerBuilder workstationBuilder = new WorkstationComputerBuilder();
        director.construct(workstationBuilder);
        Computer workstationComputer = workstationBuilder.getResult();
        workstationComputer.displayInfo();
    }
}



Advantages:

Readability: Improved code readability by separating object construction steps.

Immutability: Builders often create immutable objects (unchangeable after creation), promoting 
thread safety and immutability benefits.

Flexibility: Allows specifying only the necessary parameters for object creation.

Telescoping Constructors: Avoids the "Telescoping Constructor" anti-pattern, where a constructor with many parameters becomes unwieldy.

Disadvantages:

Complexity: Introduces an additional builder class, potentially increasing code size.

Verbosity: Can lead to more verbose code compared to simple constructors, especially for simple objects.

Dependency Injection: May complicate dependency injection if you need to inject dependencies into the object being built.

Difference between Builder Design Pattern and Decorator design pattern
Focus	
Construction of complex objects	(Builder)
Dynamically adding/removing behavior to objects(Decorater)

So Decorater design pattern provide you the dynamic nature you can add/remove the behavior without creating  a differnt class

