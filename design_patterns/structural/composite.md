# Composite pattern

The Composite pattern is a software design pattern used to create hierarchies of objects that represent complex structures in a hierarchical tree. In this pattern, an object can be composed of other objects, which in turn can be composed of other objects, and so on.

The main purpose of the Composite pattern is to treat individual objects and compositions of objects in the same way. This means that clients using the composite object do not need to worry about whether they are working with an individual object or a composition of objects.

An example of the Factory pattern using Java code could be:

```java
    public interface MenuComponent {
        public String getName();
        public double getPrice();
        public void print();
}
```

Suppose we want to create a menu structure that can have both individual items and composite items. Each menu item can have a name and a price.

Then, we create two classes, MenuItem for individual items and Menu for compound items.

This is a class to create individual elements (menu items):

```java
public class MenuItem implements MenuComponent {
    private String name;
    private double price;

    public MenuItem(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public void print() {
        System.out.println(getName() + " $" + getPrice());
    }
}
```

This is a class to create composite elements :

```java

public class Menu implements MenuComponent {
    private List<MenuComponent> menuComponents = new ArrayList<>();
    private String name;

    public Menu(String name) {
        this.name = name;
    }

    public void add(MenuComponent menuComponent) {
        menuComponents.add(menuComponent);
    }

    public void remove(MenuComponent menuComponent) {
        menuComponents.remove(menuComponent);
    }

    public MenuComponent getChild(int index) {
        return menuComponents.get(index);
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        throw new UnsupportedOperationException();
    }

    public void print() {
        System.out.println(getName());
        System.out.println("--------------------");

        for (MenuComponent menuComponent : menuComponents) {
            menuComponent.print();
        }
    }
}
```

In the Menu class we create a list of objects that can contain single and compound elements. We use add(), remove(), and getChild() operations to work with this list. The getName() and getPrice() methods get information from the menu. The print() operation is responsible for printing all menu items, whether they are single or compound items.

```java
public class MenuDemo {
    public static void main(String[] args) {
        MenuComponent menu = new Menu("Menú Principal");
        MenuComponent menu1 = new Menu("Menú Desayuno");
        MenuComponent menu2 = new Menu("Menú Almuerzo");
        MenuComponent menu3 = new Menu("Menú Cena");

        menu1.add(new MenuItem("Café", 2.50));
        menu1.add(new MenuItem("Tostadas", 3.00));

        menu2.add(new MenuItem("Sopa del día", 4.50));
        menu2.add(new MenuItem("Plato principal", 12.50));

        menu3.add(new MenuItem("Ensalada", 8.50));
        menu3.add(new MenuItem("Postre", 5.50));
    }
}
```

Finally, we can use these classes to create a menu that has both individual items and composite items.

<p align="center">
<img src="https://res.cloudinary.com/dzxhdnqm4/image/upload/v1681005367/UML_Composite_aqcqxr.png" alt="mypic" width="50%">
</p>
In short, the Composite pattern uses aggregation to build hierarchical structures of composite objects and simplify the handling of individual and composite items in the same way. In the example, the Menu class uses aggregation to build a list of MenuComponent objects to handle both individual and composite menu items.
