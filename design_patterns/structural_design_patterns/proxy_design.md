The Proxy Design Pattern is a structural design pattern that provides a surrogate or placeholder for another object to control access to it. This pattern is useful when you want to add an extra layer of control over access to an object. The proxy acts as an intermediary, controlling access to the real object.

A real-world example can be a cheque or credit card as a proxy for what is in our bank account. It can be used in place of cash and provides a means of accessing that cash when required.

And that’s exactly what the Proxy pattern does – ” Controls and manages access to the object they are protecting”.

```java 
// Subject
interface Image {
	void display();
}

// RealSubject
class RealImage implements Image {
	private String filename;

	public RealImage(String filename) {
		this.filename = filename;
		loadImageFromDisk();
	}

	private void loadImageFromDisk() {
		System.out.println("Loading image: " + filename);
	}

	public void display() {
		System.out.println("Displaying image: " + filename);
	}
}

// Proxy
class ProxyImage implements Image {
	private RealImage realImage;
	private String filename;

	public ProxyImage(String filename) {
		this.filename = filename;
	}

	public void display() {
		if (realImage == null) {
			realImage = new RealImage(filename);
		}
		realImage.display();
	}
}

// Client code
public class ProxyPatternExample {
	public static void main(String[] args) {
		Image image = new ProxyImage("example.jpg");

		// Image will be loaded from disk only when display() is called
		image.display();

		// Image will not be loaded again, as it has been cached in the Proxy
		image.display();
	}
}


Why do we need Proxy Design Pattern?

The Proxy Design Pattern is employed to address various concerns and scenarios in software development, providing a way to control access to objects, add functionality, or optimize performance.

Lazy Loading:

One of the primary use cases for proxies is lazy loading. In situations where creating or initializing an object is resource-intensive, the proxy delays the creation of the real object until it is actually needed.
This can lead to improved performance by avoiding unnecessary resource allocation.

Access Control:
Proxies can enforce access control policies.
By acting as a gatekeeper to the real object, proxies can restrict access based on certain conditions, providing security or permission checks.

Protection Proxy:

Protection proxies control access to a real object by adding an additional layer of security checks.
They can ensure that the client code has the necessary permissions before allowing access to the real object.

Caching:

Proxies can implement caching mechanisms to store results or resources.
This is particularly useful when repeated operations on a real object can be optimized by caching previous results, avoiding redundant computations or data fetching.

Logging and Monitoring:

Proxies provide a convenient point to add logging or monitoring functionalities.
By intercepting method calls to the real object, proxies can log information, track usage, or measure performance without modifying the real object.



When not to use Proxy Design Pattern?

Overhead for Simple Operations: Avoid using a proxy for simple objects or operations that don’t involve resource-intensive tasks. Introducing a proxy might add unnecessary complexity in such cases.

Unnecessary Abstraction: If your application doesn’t require lazy loading, access control, or additional functionalities provided by proxies, introducing proxies may lead to unnecessary abstraction and code complexity.

Performance Impact: If the introduction of a proxy negatively impacts performance rather than improving it, especially in cases where objects are lightweight and creation is not a significant overhead.

When Access Control Isn’t Needed: If there are no access control requirements and the client code can directly interact with the real object without any restrictions.

When Eager Loading is Acceptable: If eager loading of objects is acceptable and doesn’t affect the performance of the system, introducing a proxy for lazy loading might be unnecessary.