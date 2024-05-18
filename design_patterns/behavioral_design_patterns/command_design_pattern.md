Real-Life Analogy: Smart Home System
Imagine you have a smart home system with various devices such as lights, air conditioners, and speakers. You can control these devices using a central remote control. Here’s how the Command Design Pattern fits into this scenario:


Components in the Smart Home System:
Command Interface: Represents the command to be executed (e.g., turn on/off a device, set temperature).
Concrete Commands: Implement the command interface for specific devices and actions (e.g., LightOnCommand, LightOffCommand, SetTemperatureCommand).
Invoker: The remote control that triggers commands.
Receiver: The actual devices in the smart home system (e.g., Light, AirConditioner).

```java

// Command Interface
interface Command {
    void execute();
    void undo();
}

// Receiver: Light
class Light {
    public void on() {
        System.out.println("The light is on.");
    }

    public void off() {
        System.out.println("The light is off.");
    }
}

// Concrete Command for turning on the light
class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.on();
    }

    @Override
    public void undo() {
        light.off();
    }
}

// Concrete Command for turning off the light
class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.off();
    }

    @Override
    public void undo() {
        light.on();
    }
}

// Receiver: AirConditioner
class AirConditioner {
    private int temperature;

    public void setTemperature(int temperature) {
        this.temperature = temperature;
        System.out.println("The air conditioner temperature is set to " + temperature + " degrees.");
    }
}

// Concrete Command for setting the temperature of the air conditioner
class SetTemperatureCommand implements Command {
    private AirConditioner airConditioner;
    private int temperature;
    private int previousTemperature;

    public SetTemperatureCommand(AirConditioner airConditioner, int temperature) {
        this.airConditioner = airConditioner;
        this.temperature = temperature;
    }

    @Override
    public void execute() {
        previousTemperature = airConditioner.temperature;
        airConditioner.setTemperature(temperature);
    }

    @Override
    public void undo() {
        airConditioner.setTemperature(previousTemperature);
    }
}

// Invoker: RemoteControl
class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }

    public void pressUndo() {
        command.undo();
    }
}

// Client Code
public class SmartHomeDemo {
    public static void main(String[] args) {
        // Creating receivers
        Light livingRoomLight = new Light();
        AirConditioner airConditioner = new AirConditioner();

        // Creating commands
        Command lightOn = new LightOnCommand(livingRoomLight);
        Command lightOff = new LightOffCommand(livingRoomLight);
        Command setTemperature = new SetTemperatureCommand(airConditioner, 24);

        // Creating invoker
        RemoteControl remote = new RemoteControl();

        // Turn on the light
        remote.setCommand(lightOn);
        remote.pressButton();

        // Set the air conditioner temperature
        remote.setCommand(setTemperature);
        remote.pressButton();

        // Turn off the light
        remote.setCommand(lightOff);
        remote.pressButton();

        // Undo the last command (turn off)
        remote.pressUndo();
    }
}

Expected Clinet Output 

The light is on.
The air conditioner temperature is set to 24 degrees.
The light is off.
The light is on.

When to use the Command Design Pattern 
Decoupling is Needed:
Use the Command Pattern when you want to decouple the sender (requester) of a request from the object that performs the request.
This helps in making your code more flexible and extensible.

Undo/Redo Functionality is Required:
If you need to support undo and redo operations in your application, the Command Pattern is a good fit.
Each command can encapsulate an operation and its inverse, making it easy to undo or redo actions.

Support for Queues and Logging:
If you want to maintain a history of commands, log them, or even put them in a queue for execution, the Command Pattern provides a structured way to achieve this.

Dynamic Configuration:
When you need the ability to dynamically configure and assemble commands at runtime, the Command Pattern allows for flexible composition of commands.


