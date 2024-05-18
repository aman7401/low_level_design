The Composite Design Pattern is a structural design pattern that lets you compose objects into tree-like structures to represent part-whole hierarchies. It allows clients to treat individual objects and compositions of objects uniformly. In other words, whether dealing with a single object or a group of objects (composite), clients can use them interchangeably.

```java

import java.util.ArrayList;
import java.util.List;

// Component
interface Task {
	String getTitle();
	void setTitle(String title);
	void display();
}

// Leaf
class SimpleTask implements Task {
	private String title;

	public SimpleTask(String title) {
		this.title = title;
	}

	@Override
	public String getTitle() {
		return title;
	}

	@Override
	public void setTitle(String title) {
		this.title = title;
	}

	@Override
	public void display() {
		System.out.println("Simple Task: " + title);
	}
}

// Composite
class TaskList implements Task {
	private String title;
	private List<Task> tasks;

	public TaskList(String title) {
		this.title = title;
		this.tasks = new ArrayList<>();
	}

	@Override
	public String getTitle() {
		return title;
	}

	@Override
	public void setTitle(String title) {
		this.title = title;
	}

	public void addTask(Task task) {
		tasks.add(task);
	}

	public void removeTask(Task task) {
		tasks.remove(task);
	}

	@Override
	public void display() {
		System.out.println("Task List: " + title);
		for (Task task : tasks) {
			task.display();
		}
	}
}

// Client
public class TaskManagementApp {
	public static void main(String[] args) {
		// Creating simple tasks
		Task simpleTask1 = new SimpleTask("Complete Coding");
		Task simpleTask2 = new SimpleTask("Write Documentation");

		// Creating a task list
		TaskList projectTasks = new TaskList("Project Tasks");
		projectTasks.addTask(simpleTask1);
		projectTasks.addTask(simpleTask2);

		// Nested task list
		TaskList phase1Tasks = new TaskList("Phase 1 Tasks");
		phase1Tasks.addTask(new SimpleTask("Design"));
		phase1Tasks.addTask(new SimpleTask("Implementation"));

		projectTasks.addTask(phase1Tasks);

		// Displaying tasks
		projectTasks.display();
	}
}

```
Note : 

When to use Composite Design Pattern?
Composite Pattern should be used when clients need to ignore the difference between compositions of objects and individual objects. If programmers find that they are using multiple objects in the same way, and often have nearly identical code to handle each of them, then composite is a good choice, it is less complex in this situation to treat primitives and composites as homogeneous.

Less number of objects reduces the memory usage, and it manages to keep us away from errors related to memory like java.lang.OutOfMemoryError.
Although creating an object in Java is really fast, we can still reduce the execution time of our program by sharing objects.


Use the Composite Design Pattern when dealing with hierarchical structures that require uniform access and recursive behavior. Avoid using it when your objects lack a hierarchical structure, or when the overhead of managing composite structures outweighs the benefits, or when the problem domain is relatively simple and does not require uniform treatment of objects


When to Use Composite Design Pattern:
For hierarchical structures where objects are treated uniformly.
When there's a need for uniform access to objects regardless of complexity.
In scenarios requiring recursive behavior with objects containing similar objects.
For dynamically assembling or modifying structures at runtime.
Not suitable for non-hierarchical structures or when performance overhead is a concern.


