The Bridge design pattern allows you to separate the abstraction from the implementation. It is a structural design pattern. 

There are 2 parts in Bridge design pattern : 

Abstraction
Implementation
This is a design mechanism that encapsulates an implementation class inside of an interface class.  

The bridge pattern allows the Abstraction and the Implementation to be developed independently and the client code can access only the Abstraction part without being concerned about the Implementation part.

The abstraction is an interface or abstract class and the implementer is also an interface or abstract class.

The abstraction contains a reference to the implementer. Children of the abstraction are referred to as refined abstractions, and children of the implementer are concrete implementers. Since we can change the reference to the implementer in the abstraction, we are able to change the abstraction’s implementer at run-time. Changes to the implementer do not affect client code.

It increases the loose coupling between class abstraction and it’s implementation.


```java

// The below code is using abstraction so that that why it have to call the super of parent to intilize the Render type object 


// Implementor
public interface Renderer {
    void renderCircle(float radius);
    void renderSquare(float side);
}

// Concrete Implementor A
public class VectorRenderer implements Renderer {
    @Override
    public void renderCircle(float radius) {
        System.out.println("Drawing a circle with radius " + radius + " using vector renderer.");
    }

    @Override
    public void renderSquare(float side) {
        System.out.println("Drawing a square with side " + side + " using vector renderer.");
    }
}

// Concrete Implementor B
public class RasterRenderer implements Renderer {
    @Override
    public void renderCircle(float radius) {
        System.out.println("Drawing a circle with radius " + radius + " using raster renderer.");
    }

    @Override
    public void renderSquare(float side) {
        System.out.println("Drawing a square with side " + side + " using raster renderer.");
    }
}

// Abstraction
public abstract class Shape {
    protected Renderer renderer;

    public Shape(Renderer renderer) {
        this.renderer = renderer;
    }

    public abstract void draw();
    public abstract void resize(float factor);
}

// Refined Abstraction A
public class Circle extends Shape {
    private float radius;

    public Circle(Renderer renderer, float radius) {
        super(renderer);
        this.radius = radius;
    }

    @Override
    public void draw() {
        renderer.renderCircle(radius);
    }

    @Override
    public void resize(float factor) {
        radius *= factor;
    }
}

// Refined Abstraction B
public class Square extends Shape {
    private float side;

    public Square(Renderer renderer, float side) {
        super(renderer);
        this.side = side;
    }

    @Override
    public void draw() {
        renderer.renderSquare(side);
    }

    @Override
    public void resize(float factor) {
        side *= factor;
    }
}

// Client Code
public class Client {
    public static void main(String[] args) {
        Renderer vectorRenderer = new VectorRenderer();
        Renderer rasterRenderer = new RasterRenderer();

        Shape circle = new Circle(vectorRenderer, 5);
        circle.draw();
        circle.resize(2);
        circle.draw();

        Shape square = new Square(rasterRenderer, 3);
        square.draw();
        square.resize(2);
        square.draw();
    }
}

```
Note

In Java, super(renderer) is used to call the constructor of the superclass of the current class (Circle in this case) with the specified argument(s).

When you call super(renderer) within a constructor of a subclass (Circle), you're essentially invoking a constructor of the superclass (Shape or any class from which Circle directly or indirectly inherits) that matches the signature Renderer.


If Circle directly extends a class (not an interface), then super(renderer) should match the signature of one of the constructors in the superclass. If Circle extends an abstract class or a concrete class, this constructor call should match one of the constructors in that superclass.

If Circle implements an interface (Shape), then this call doesn't directly invoke a constructor of Shape, but rather ensures that the renderer instance is stored in the Circle object as part of the initialization process.

```java 

// Interface Implementation below  No need to call the supar 

// Implementor
public interface Renderer {
    void renderCircle(float radius);
    void renderSquare(float side);
}

// Concrete Implementor A
public class VectorRenderer implements Renderer {
    @Override
    public void renderCircle(float radius) {
        System.out.println("Drawing a circle with radius " + radius + " using vector renderer.");
    }

    @Override
    public void renderSquare(float side) {
        System.out.println("Drawing a square with side " + side + " using vector renderer.");
    }
}

// Concrete Implementor B
public class RasterRenderer implements Renderer {
    @Override
    public void renderCircle(float radius) {
        System.out.println("Drawing a circle with radius " + radius + " using raster renderer.");
    }

    @Override
    public void renderSquare(float side) {
        System.out.println("Drawing a square with side " + side + " using raster renderer.");
    }
}

// Abstraction
public interface Shape {
    void draw();
    void resize(float factor);
}

// Refined Abstraction A
public class Circle implements Shape {
    private float radius;
    private Renderer renderer;

    public Circle(Renderer renderer, float radius) {
        this.renderer = renderer;
        this.radius = radius;
    }

    @Override
    public void draw() {
        renderer.renderCircle(radius);
    }

    @Override
    public void resize(float factor) {
        radius *= factor;
    }
}

// Refined Abstraction B
public class Square implements Shape {
    private float side;
    private Renderer renderer;

    public Square(Renderer renderer, float side) {
        this.renderer = renderer;
        this.side = side;
    }

    @Override
    public void draw() {
        renderer.renderSquare(side);
    }

    @Override
    public void resize(float factor) {
        side *= factor;
    }
}

// Client Code
public class Client {
    public static void main(String[] args) {
        Renderer vectorRenderer = new VectorRenderer();
        Renderer rasterRenderer = new RasterRenderer();

        Shape circle = new Circle(vectorRenderer, 5);
        circle.draw();
        circle.resize(2);
        circle.draw();

        Shape square = new Square(rasterRenderer, 3);
        square.draw();
        square.resize(2);
        square.draw();
    }
}
