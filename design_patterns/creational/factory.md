# Factory pattern

The Factory pattern is an object-oriented design pattern in object-oriented programming that provides an interface for creating objects in a superclass, allowing subclasses to decide which object class to instantiate.

It facilitates the creation of objects without exposing the creation logic to the client, promoting decoupling and scalability of the code.

An example of the Factory pattern using Java code could be:

```java
// Component interface
public interface File {
    void open();
    void save();
    void close();
}
// Concrete file classes
public class TextFile implements File {
    @Override
    public void open() {
        System.out.println("Opening a text file.");
    }

    @Override
    public void save() {
        System.out.println("Saving a text file.");
    }

    @Override
    public void close() {
        System.out.println("Closing a text file.");
    }
}

public class ImageFile implements File {
    @Override
    public void open() {
        System.out.println("Opening an image file.");
    }

    @Override
    public void save() {
        System.out.println("Saving an image file.");
    }

    @Override
    public void close() {
        System.out.println("Closing an image file.");
    }
}

public class AudioFile implements File {
    @Override
    public void open() {
        System.out.println("Opening an audio file.");
    }

    @Override
    public void save() {
        System.out.println("Saving an audio file.");
    }

    @Override
    public void close() {
        System.out.println("Closing an audio file.");
    }
}
```

In this example, it needs to create different objects of different File subclasses at runtime without coupling the code to specific concrete classes.

In this example, the File interface defines the operations required to open, save, and close a file, and there are three concrete classes that implement the interface: TextFile, ImageFile, and AudioFile.

```java
// FileFactory class
class FileFactory {
    public static File createFile(String fileType) {
        if (fileType.equalsIgnoreCase("text")) {
            return new TextFile();
        } else if (fileType.equalsIgnoreCase("image")) {
            return new ImageFile();
        } else if (fileType.equalsIgnoreCase("audio")) {
            return new AudioFile();
        } else {
            throw new IllegalArgumentException("Invalid file type.");
        }
    }
}
```

The FileFactory class is responsible for creating objects from the subclasses of File according to the type of file required.

The Factory pattern is used, creating the common File interface, concrete subclasses such as TextFile, ImageFile, and AudioFile, and the FileFactory class that encapsulates the creation of objects from these subclasses.

This makes the code more modular, easier to maintain and flexible by allowing the creation of different types of files without modifying the code of the main Main class.

```java
// Main class
public class Main {
    public static void main(String[] args) {
        File textFile = FileFactory.createFile("text");
        textFile.open();
        textFile.save();
        textFile.close();

        File imageFile = FileFactory.createFile("image");
        imageFile.open();
        imageFile.save();
        imageFile.close();

        File audioFile = FileFactory.createFile("audio");
        audioFile.open();
        audioFile.save();
        audioFile.close();
    }
}
```

<p align="center">
<img src="https://res.cloudinary.com/dzxhdnqm4/image/upload/v1680996327/UML_Factory_2_siieqw.png" alt="mypic" width="75%">
</p>

The main class Main creates different types of files using the FileFactory class, and calls the open(), save(), and close() operations on each. In this way, the Factory pattern is used to create different file objects according to the file type.
