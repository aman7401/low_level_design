The Prototype Design Pattern is a creational pattern that enables the creation of new objects by copying an existing object. Prototype allows us to hide the complexity of making new instances from the client. The concept is to copy an existing object rather than create a new instance from scratch, something that may include costly operations. The existing object acts as a prototype and contains the state of the object.

The Prototype interface declares the cloning methods. In most cases, it’s a single clone method.

The Concrete Prototype class implements the cloning method. In addition to copying the original object’s data to the clone, this method may also handle some edge cases of the cloning process related to cloning linked objects, untangling recursive dependencies, etc.

The Client can produce a copy of any object that follows the prototype interface.

```java
// Prototype interface
interface Shape {
	Shape clone(); // Make a copy of itself
	void draw(); // Draw the shape
}

// Concrete prototype
class Circle implements Shape {
	private String color;

	// When you create a circle, you give it a color.
	public Circle(String color) {
		this.color = color;
	}

	// This creates a copy of the circle.
	@Override
	public Shape clone() {
		return new Circle(this.color);
	}

	// This is how a circle draws itself.
	@Override
	public void draw() {
		System.out.println("Drawing a " + color + " circle.");
	}
}

// Client code
class ShapeClient {
	private Shape shapePrototype;

	// When you create a client, you give it a prototype (a shape).
	public ShapeClient(Shape shapePrototype) {
		this.shapePrototype = shapePrototype;
	}

	// This method creates a new shape using the prototype.
	public Shape createShape() {
		return shapePrototype.clone();
	}
}

// Main class
public class PrototypeExample {
	public static void main(String[] args) {
		// Create a concrete prototype (a red circle).
		Shape circlePrototype = new Circle("red");

		// Create a client and give it the prototype.
		ShapeClient client = new ShapeClient(circlePrototype);

		// Use the prototype to create a new shape (a red circle).
		Shape redCircle = client.createShape();

		// Draw the newly created red circle.
		redCircle.draw();
	}
}

When to use the Prototype Design Pattern 

Creating Objects is Costly:
Use the Prototype pattern when creating objects is more expensive or complex than copying existing ones.
If object creation involves significant resources, such as database or network calls, and you have a similar object available, cloning can be more efficient.

Variations of Objects:
Use the Prototype pattern when your system needs to support a variety of objects with slight variations.
Instead of creating multiple classes for each variation, you can create prototypes and clone them with modifications.


Pros:

Faster creation: Clone existing objects for improved performance, especially for complex ones.
Flexible object variation: Create variations without subclassing. Clone and modify properties.
Less subclassing: Prototype offers an alternative to subclassing for variations.
Lazy initialization: Defer object creation until needed, potentially saving memory.

Cons:

Overkill for simple objects: Unnecessary complexity for simple object creation.
Hidden concrete products: Client code might not know specific object types being used.
Deep cloning complexity: Deep copying all parts can be tricky, especially with circular references.
Memory overhead: Cloning creates copies, potentially increasing memory usage for large objects.

Use Prototype when:

Object creation is expensive.
You need variations without subclassing.
Lazy initialization is beneficial.



The main difference between shallow cloning and deep cloning lies in how they handle references to other objects within the object being cloned:

Shallow Cloning:

Creates a new object of the same type.
Copies the values of primitive data fields from the original object.
Crucially, for reference type fields (objects within the object), it simply copies the memory addresses of those referenced objects. This means both the original and the clone point to the same objects in memory.
Deep Cloning:

Creates a completely independent copy of the original object.
Copies the values of primitive data fields.
For reference type fields, it also creates new copies of the referenced objects and assigns them to the corresponding fields in the cloned object. This ensures that changes made to the clone's references don't affect the original object's references (and vice versa) because they are separate objects in memory.
