The SOLID Principles
S — Single Responsibility
A class should have a single responsibility
This principle aims to separate behaviours so that if bugs arise as a result of your change, it won’t affect other unrelated behaviours.

O — Open-Closed
Classes should be open for extension, but closed for modification
This principle aims to extend a Class’s behaviour without changing the existing behaviour of that Class. This is to avoid causing bugs wherever the Class is being used.

L — Liskov Substitution
If S is a subtype of T, then objects of type T in a program may be replaced with objects of type S without altering any of the desirable properties of that program.
The child Class should be able to process the same requests and deliver the same result as the parent Class or it could deliver a result that is of the same type.
This principle aims to enforce consistency so that the parent Class or its child Class can be used in the same way without any errors.

I — Interface Segregation
Clients should not be forced to depend on methods that they do not use.
When a Class is required to perform actions that are not useful, it is wasteful and may produce unexpected bugs if the Class does not have the ability to perform those actions.
This principle aims at splitting a set of actions into smaller sets so that a Class executes ONLY the set of actions it requires.

D — Dependency Inversion(Class should Depend on Interface rather than concrete class)
- High-level modules should not depend on low-level modules. Both should depend on the abstraction.
- Abstractions should not depend on details. Details should depend on abstractions.

High-level Module(or Class): Class that executes an action with a tool.

Low-level Module (or Class): The tool that is needed to execute the action

Abstraction: Represents an interface that connects the two Classes.

Details: How the tool works

This principle says a Class should not be fused with the tool it uses to execute an action. Rather, it should be fused to the interface that will allow the tool to connect to the Class.
It also says that both the Class and the interface should not know how the tool works. However, the tool needs to meet the specification of the interface.

Goal
This principle aims at reducing the dependency of a high-level Class on the low-level Class by introducing an interface.

class Mackbook{
    private final Keyboard keyboard;
    private final Mouse mouse ;    // Object type interface

    public Macbook(Keyboard keyboard , Mouse mouse){
        this.keyboard = keyboard;
        this.mouse = mosue;
    }
}

 In the above code we are using Interface object Type which will assign the type of Mouse or Keyboard at the runtime via constructor injection . And the Mackbook class is only dependent on the Keyboard , Mpuse Interface on the concrete class object which implies (High-level modules should not depend on low-level modules. Both should depend on the abstraction.)

 
