Facade Method Design Pattern is a part of the Gang of Four design patterns and it is categorized under Structural design patterns. Before we dive deep into the details of it, imagine a building, the facade is the outer wall that people see, but behind it is a complex network of wires, pipes, and other systems that make the building function. The facade pattern is like that outer wall. It hides the complexity of the underlying system and provides a simple interface that clients can use to interact with the system.

When to use Facade Method Design Pattern

A Facade provide a simple default view of the subsystem that is good enough for most clients. Only clients needing more customizability will need to look beyond the facade.

There are many dependencies between clients and the implementation classes of an abstraction.

A Facade to decouple the subsystem from clients and other subsystems, thereby promoting subsystem independence and portability.

Facade define an entry point to each subsystem level. If subsystem are dependent, then you can simplify the dependencies between them by making them communicate with each other solely through their facades.

Real Life Example of Facade Design Pattern 

Let’s consider a hotel. This hotel has a hotel keeper. There are a lot of restaurants inside the hotel e.g. Veg restaurants, Non-Veg restaurants, and Veg/Non Both restaurants. You, as a client want access to different menus of different restaurants. You do not know what are the different menus they have. You just have access to a hotel keeper who knows his hotel well. Whichever menu you want, you tell the hotel keeper and he takes it out of the respective restaurants and hands it over to you.


```java 

//Interface of Hotel

package structural.facade;

public interface Hotel {
	public Menus getMenus();
}

//NonVeg Restaurant 

package structural.facade;

public class NonVegRestaurant implements Hotel {

	public Menus getMenus()
	{
		NonVegMenu nv = new NonVegMenu();
		return nv;
	}
}

//VegRestaurant 

package structural.facade;

public class VegRestaurant implements Hotel {

	public Menus getMenus()
	{
		VegMenu v = new VegMenu();
		return v;
	}
}

// VegNonBothRestaurant

package structural.facade;

public class VegNonBothRestaurant implements Hotel {

	public Menus getMenus()
	{
		Both b = new Both();
		return b;
	}
}

/*package whatever //do not write package name here */
// HotelKeeper Takes care of all the 

package structural.facade;

public interface HotelKeeper {


public VegMenu getVegMenu();
public NonVegMenu getNonVegMenu();
public Both getVegNonMenu();

}


package structural.facade;

public class HotelKeeperImplementation implements HotelKeeper {

	public VegMenu getVegMenu()
	{
		VegRestaurant v = new VegRestaurant();
		VegMenu vegMenu = (VegMenu)v.getMenus();
		return vegMenu;
	}

	public NonVegMenu getNonVegMenu()
	{
		NonVegRestaurant v = new NonVegRestaurant();
		NonVegMenu NonvegMenu = (NonVegMenu)v.getMenus();
		return NonvegMenu;
	}

	public Both getVegNonMenu()
	{
		VegNonBothRestaurant v = new VegNonBothRestaurant();
		Both bothMenu = (Both)v.getMenus();
		return bothMenu;
	}
}


package structural.facade;

public class Client
{
	public static void main (String[] args)
	{
		HotelKeeper keeper = new HotelKeeperImplementation();
		
		VegMenu v = keeper.getVegMenu();
		NonVegMenu nv = keeper.getNonVegMenu();
		Both = keeper.getVegNonMenu();

	}
}

```
Conclusion

The facade pattern is appropriate when you have a complex system that you want to expose to clients in a simplified way, or you want to make an external communication layer over an existing system that is incompatible with the system. Facade deals with interfaces, not implementation. Its purpose is to hide internal complexity behind a single interface that appears simple on the outside.   


Use Cases of Facade Method Design Pattern

Simplifying Complex External Systems:

A facade encapsulates database connection, query execution, and result processing, offering a clean interface to the application.
A facade simplifies the usage of external APIs by hiding the complexities of authentication, request formatting, and response parsing.
A facade can create a more user-friendly interface for complex or poorly documented libraries.

Layering Subsystems:

Decoupling subsystems: Facades define clear boundaries between subsystems, reducing dependencies and promoting modularity.
Providing high-level views: Facades offer simplified interfaces to lower-level subsystems, making them easier to understand and use.

Providing a Unified Interface to Diverse Systems:

Integrating multiple APIs: A facade can combine multiple APIs into a single interface, streamlining interactions and reducing code duplication.
Bridging legacy systems: A facade can create a modern interface for older, less accessible systems, facilitating their integration with newer components.

Protecting Clients from Unstable Systems:

Isolating clients from changes: Facades minimize the impact of changes to underlying systems by maintaining a stable interface.
Managing third-party dependencies: Facades can protect clients from changes or issues in external libraries or services.


Disadvantages of Facade Method Design Pattern
Increased Complexity:

Introducing a facade layer adds an extra abstraction level, potentially increasing the overall complexity of the system.
This can make the code harder to understand and debug, especially for developers unfamiliar with the pattern.

Reduced Flexibility:
The facade acts as a single point of access to the underlying system.
This can limit the flexibility for clients who need to bypass the facade or access specific functionalities hidden within the subsystem.
