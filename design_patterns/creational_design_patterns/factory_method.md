The Factory Method Design Pattern is a creational design pattern that provides an interface for creating objects in a superclass, allowing subclasses to alter the type of objects that will be created. It encapsulates object creation logic in a separate method, promoting loose coupling between the creator and the created objects


```java

// Library classes
abstract class Vehicle {
    public abstract void printVehicle();
}

class TwoWheeler extends Vehicle {
    public void printVehicle() {
        System.out.println("I am two wheeler");
    }
}

class FourWheeler extends Vehicle {
    public void printVehicle() {
        System.out.println("I am four wheeler");
    }
}

// Factory Interface
interface VehicleFactory {
    Vehicle createVehicle();
}

// Concrete Factory for TwoWheeler
class TwoWheelerFactory implements VehicleFactory {
    public Vehicle createVehicle() {
        return new TwoWheeler();
    }
}

// Concrete Factory for FourWheeler
class FourWheelerFactory implements VehicleFactory {
    public Vehicle createVehicle() {
        return new FourWheeler();
    }
}

// Client class
class Client {
    private Vehicle pVehicle;

    public Client(VehicleFactory factory) {
        pVehicle = factory.createVehicle();
    }

    public Vehicle getVehicle() {
        return pVehicle;
    }
}

// Driver program
public class GFG {
    public static void main(String[] args) {
        VehicleFactory twoWheelerFactory = new TwoWheelerFactory();
        Client twoWheelerClient = a Client(twoWheelerFactory);
        Vehicle twoWheeler = twoWheelerClient.getVehicle();
        twoWheeler.printVehicle();

        VehicleFactory fourWheelerFactory = new FourWheelerFactory();
        Client fourWheelerClient = a Client(fourWheelerFactory);
        Vehicle fourWheeler = fourWheelerClient.getVehicle();
        fourWheeler.printVehicle();
    }
}



Output : 
I am two wheeler
I am four wheeler



Pros:
Flexibility: Easy to add new product types without changing client code.
Loose Coupling: Client code doesn't depend on specific products.
Encapsulation: Hides object creation logic.
Testability: Simplifies unit testing.


Cons:
Complexity: Introduces more classes, potentially increasing overhead.
Performance: Might have slight overhead compared to simpler approaches.
Overuse: Not always necessary for simple scenarios.


