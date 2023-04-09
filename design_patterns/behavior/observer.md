# Observer pattern

The Observer pattern is a design pattern that establishes a one-to-many relationship between objects, such that when an object (subject) changes its state, all its dependents (observers) are automatically notified and updated.

This pattern is useful for maintaining synchronization and consistency between related objects without them being tightly coupled, facilitating scalability, maintainability and modularity of the code.

An example of the Observer pattern using Java code could be:

```Java
// Interfaz Observer
public interface Observer {
    void update(String message);
}

// Interfaz Subject
public interface Subject {
    void addObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}
```

For this example we have two interfaces:
Observer and Subject interfaces.

The Observer interface, which defines the update method to be implemented by all observers.

The Subject interface, which defines the methods for adding, removing and notifying observers.

```java
public class ConcreteSubject implements Subject {
    private List<Observer> observers;
    private String state;

    public ConcreteSubject() {
        this.observers = new ArrayList<>();
    }

    @Override
    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(state);
        }
    }

    public void setState(String state) {
        this.state = state;
        notifyObservers();
    }
}
```

The ConcreteSubject class, which implements the Subject interface, maintains a list of observers and notifies all observers when their status changes.

```java
public class ConcreteObserver implements Observer {
    private String observerName;

    public ConcreteObserver(String observerName) {
        this.observerName = observerName;
    }

    @Override
    public void update(String message) {
        System.out.println(observerName + " received message: " + message);
    }
}
```

The ConcreteObserver class, which implements the Observer interface and performs some action when it receives a notification.

```java
public class ObserverPatternExample {
    public static void main(String[] args) {
        ConcreteSubject subject = new ConcreteSubject();

        ConcreteObserver observer1 = new ConcreteObserver("Observer 1");
        ConcreteObserver observer2 = new ConcreteObserver("Observer 2");

        subject.addObserver(observer1);
        subject.addObserver(observer2);

        subject.setState("New State 1");
        subject.setState("New State 2");
    }
}
```

<p align="center">
<img src="https://res.cloudinary.com/dzxhdnqm4/image/upload/v1681008518/UML_Observer_aczpve.png" alt="uml-observer" width="70%">
</p>
The ObserverPatternExample class contains the main method, which creates an instance of ConcreteSubject, adds two observers and changes the state of the subject to demonstrate how observers are notified.
