The Memento design pattern is a behavioral design pattern used to capture and restore the internal state of an object without exposing its implementation details.

Client: The client initiates the process by requesting the Originator to perform some operation that may modify its state or require the state to be saved. For example, the client might trigger an action like “save state” or “restore state.”

Originator: Upon receiving a request from the client, the Originator either creates a Memento to save its current state (if the request is to save state) or retrieves a Memento to restore its previous state (if the request is to restore state).

If the request is to save state:

The Originator creates a Memento object that captures its current state.
It returns the Memento to the client or Caretaker for storage.

If the request is to restore state:
The Originator retrieves the desired Memento containing the state it wants to restore.
It restores its state using the state stored in the Memento.


Caretaker: The Caretaker acts as an intermediary between the client and the Originator, managing the Memento objects.

If the client requests to save state:
The Caretaker receives the Memento from the Originator.
It stores the Memento for future use.

If the client requests to restore state:
The Caretaker retrieves the appropriate Memento from its storage.
It provides the Memento to the Originator for state restoration.

```java 

import java.util.ArrayList;
import java.util.List;

// Originator
class Document {
	private String content;

	public Document(String content) {
		this.content = content;
	}

	public void write(String text) {
		this.content += text;
	}

	public String getContent() {
		return this.content;
	}

	public DocumentMemento createMemento() {
		return new DocumentMemento(this.content);
	}

	public void restoreFromMemento(DocumentMemento memento) {
		this.content = memento.getSavedContent();
	}
}

// Memento
class DocumentMemento {
	private String content;

	public DocumentMemento(String content) {
		this.content = content;
	}

	public String getSavedContent() {
		return this.content;
	}
}

// Caretaker
class History {
	private List<DocumentMemento> mementos;

	public History() {
		this.mementos = new ArrayList<>();
	}

	public void addMemento(DocumentMemento memento) {
		this.mementos.add(memento);
	}

	public DocumentMemento getMemento(int index) {
		return this.mementos.get(index);
	}
}

public class Main {
	public static void main(String[] args) {
		Document document = new Document("Initial content\n");
		History history = new History();

		// Write some content
		document.write("Additional content\n");
		history.addMemento(document.createMemento());

		// Write more content
		document.write("More content\n");
		history.addMemento(document.createMemento());

		// Restore to previous state
		document.restoreFromMemento(history.getMemento(1));

		// Print document content
		System.out.println(document.getContent());
	}
}


```

When to use Memento Design Pattern

Undo functionality: When you need to implement an undo feature in your application that allows users to revert changes made to an object’s state.

Snapshotting: When you need to save the state of an object at various points in time to support features like versioning or checkpoints.

Transaction rollback: When you need to rollback changes to an object’s state in case of errors or exceptions, such as in database transactions.

Caching: When you want to cache the state of an object to improve performance or reduce redundant computations.
