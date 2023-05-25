# Flyweight Patterns

The Flyweight pattern is used to optimize memory usage in an application. This approach is based on the idea of sharing repetitive objects instead of creating new instances of each one, which helps reduce or eliminate redundancy. This results in improved balance, flexibility, and performance.

This pattern is applied in situations where an application needs to handle a large number of similar objects, such as in a game where many enemies need to be drawn on the screen. Instead of creating a new instance of each enemy, the Flyweight pattern allows sharing a single instance among all enemies of the same type. This contributes to more efficient memory management and better application performance.

## 🏗️ Estructure
[![Estructura-Flyweight-drawio.png](https://i.postimg.cc/N0sbC8K2/Estructura-Flyweight-drawio.png)](https://postimg.cc/bZ5QstHq)
The Flyweight design pattern aims to optimize memory efficiency by sharing objects in a system, reducing data duplication, and improving performance. To achieve this, the Flyweight pattern divides an object into two parts: an intrinsic part and an extrinsic part.

The intrinsic part contains data that is common and does not change between different objects, while the extrinsic part contains specific and changing data that is unique to each object. By separating this data, it allows multiple objects to share the same intrinsic part, reducing the amount of memory used and improving system performance.

The Flyweight pattern generally consists of the following classes:

Flyweight: This is the base class or interface that defines the structure of flyweight objects. It can be an abstract class or an interface that declares common methods for flyweight objects.

ConcreteFlyweight: These are the concrete classes that implement the flyweight interface and represent the shared objects in the system. These classes are immutable, meaning they do not change once they are created.

FlyweightFactory: This is the factory that creates and manages flyweight objects. It maintains a pool of already created flyweight objects and reuses existing objects instead of creating new ones if they already exist. This ensures that objects are shared instead of duplicated.

Client: This is the client that uses flyweight objects through the FlyweightFactory. Clients can request flyweight objects from the factory and use them to perform their tasks, passing the necessary specific data (extrinsic part) for the operation.


## 😟 Problem
The Flyweight design pattern solves the problem of data duplication and memory inefficiency in systems that handle large quantities of similar objects. By sharing objects, the Flyweight pattern allows multiple objects to share the same common information, thereby reducing the amount of memory used and improving system performance.

Let's suppose we are developing a car racing video game, and we have noticed data duplication and inefficiency in memory usage. Every time a new instance of a car is created in the game, data such as the model, image, color, and other attributes are duplicated, resulting in high memory consumption. Furthermore, when there are many cars on the track with the same model, the duplication of data leads to decreased game performance due to unnecessary data overhead.

[![juego-drawio.png](https://i.postimg.cc/KvhPs7Vc/juego-drawio.png)](https://postimg.cc/Dm54SGnR)

~~~java
// Car class that does not use the Flyweight pattern
public class Car {
    private String model; // Car model
    private int posX; // X-axis position
    private int posY; // Y-axis position

    public Car(String model) {
        this.model = model;
    }

    public void show(int posX, int posY) {
        this.posX = posX;
        this.posY = posY;
        System.out.println("Showing car " + model + " at position (" + posX + ", " + posY + ")");
    }
}

// Game class that uses the Car class without the Flyweight pattern
public class Game {
    public static void main(String[] args) {
        // Create multiple instances of the Car class with the same model
        Car car1 = new Car("sedan");
        Car car2 = new Car("sedan");
        Car car3 = new Car("sedan");

        // Show the cars at different positions
        car1.show(10, 20);
        car2.show(30, 40);
        car3.show(50, 60);
    }
}
~~~
## 🙂 Soluction

Let's go back to our video game, and we will apply the Flyweight pattern to reduce data duplication and improve memory efficiency. The Car class acts as a Flyweight object that represents a car model, and the CarFactory class acts as a factory that creates and manages car instances. The cars share the same common information, such as the model, and are displayed at different positions on the screen. This allows for a reduction in the amount of memory used and improved system performance, especially when there are many cars on the screen with the same model.

[![juego-Flyweight-drawio.png](https://i.postimg.cc/zGXR9xkN/juego-Flyweight-drawio.png)](https://postimg.cc/6yg3ZLSb)

~~~java
// Car class that uses the Flyweight pattern
public class Car {
    private String model; // Car model
    private int posX; // X-axis position
    private int posY; // Y-axis position

    public Car(String model) {
        this.model = model;
    }

    public void display(int posX, int posY) {
        this.posX = posX;
        this.posY = posY;
        System.out.println("Displaying car " + model + " at position (" + posX + ", " + posY + ")");
    }
}

// CarFactory class that acts as a Flyweight object factory
public class CarFactory {
    private HashMap<String, Car> cars = new HashMap<>();

    public Car getCar(String model) {
        Car car = cars.get(model);

        // If the car does not exist, create a new one and add it to the HashMap
        if (car == null) {
            car = new Car(model);
            cars.put(model, car);
        }

        return car;
    }
}

// Game class that uses the Flyweight pattern
public class Game {
    public static void main(String[] args) {
        CarFactory factory = new CarFactory();

        // Obtain several Flyweight objects with the same car model
        Car car1 = factory.getCar("sedan");
        Car car2 = factory.getCar("sedan");
        Car car3 = factory.getCar("sedan");

        // Display the cars at different positions
        car1.display(10, 20);
        car2.display(30, 40);
        car3.display(50, 60);
    }
}
~~~





