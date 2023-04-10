# Iterator pattern

Iterator is a behavioral design pattern that allows you to traverse elements of a collection without exposing its underlying representation (list, stack, tree, etc.).

<p align="center">
<img src="https://res.cloudinary.com/dz5pw4p7y/image/upload/v1681088167/design_patterns/iterator_pcy9mx.png" alt="mypic" width="75%">
</p>

## 😟 Problem

Imagina que tenemos una estanteria de libros, la cual contiene una lista de libros y queremos acceder a cada uno de los libros de manera correcta y eficiente.

```java
import java.util.ArrayList;

public class Bookshelf {

    private ArrayList<Book> books = new ArrayList<>();

    // Iterates through the ArrayList and returns the next book
    public Book getNextBook() {
        if (!books.isEmpty()) {
            Book book = books.get(0);
            books.remove(0);
            return book;
        } else {
            return null;
        }
    }
}
```

En este ejemplo, la clase `Bookshelf` no implementa la interfaz `Iterator` ni proporciona una clase de iterador separada. En su lugar, proporciona un único método llamado `getNextBook()` que itera a través del ArrayList de libros y devuelve el siguiente libro.

Esta implementación viola el patrón Iterator porque no proporciona una manera segura y consistente de iterar a través de la lista de libros. Por ejemplo, si el código llamante llama a `getNextBook()` más veces de lo que hay libros en la lista, el método devolverá `null` y el código llamante puede tener errores de tiempo de ejecución. Además, esta implementación no permite iterar sobre la lista en orden inverso o modificarla mientras se está iterando.

## 🙂 Solution

Para solucionar esto, se debería implementar una interfaz `Iterator` separada para la clase `Bookshelf`, con los métodos estándar `hasNext()`, `next()` y `remove()` para iterar de forma segura a través de la lista de libros.

```java
import java.util.ArrayList;
import java.util.Iterator;

public class Bookshelf implements Iterable<Book> {

    private ArrayList<Book> books = new ArrayList<>();

    // Implementa la interfaz Iterator con una clase interna
    private class BookIterator implements Iterator<Book> {
        private int index = 0;

        public boolean hasNext() {
            return index < books.size();
        }

        public Book next() {
            return books.get(index++);
        }

        public void remove() {
            books.remove(index - 1);
            index--;
        }
    }

    // Devuelve una instancia del iterador interno
    public Iterator<Book> iterator() {
        return new BookIterator();
    }
}
```
En esta implementación, la clase `Bookshelf` implementa la interfaz `Iterable` y proporciona una clase interna llamada `BookIterator` que implementa la interfaz `Iterator`. La clase `BookIterator` tiene los métodos estándar `hasNext()`, `next()` y `remove()` para iterar de forma segura a través de la lista de libros.

El método `iterator()` de la clase `Bookshelf` devuelve una instancia de la clase interna `BookIterator`, lo que permite que el código llamante itere de forma segura a través de la lista de libros utilizando un bucle `for-each` u otro enfoque de iteración.

