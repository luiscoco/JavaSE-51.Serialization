# JavaSE-Serialization

Serialization in Java is the process of converting an object into a stream of bytes so that it can be easily stored or transmitted. 

This is useful, for example, when you want to save the state of an object to a file or send it over the network. 

Deserialization is the process of reconstructing the object from the serialized form.

Here's a simple example in Java using the Serializable interface:

```java
import java.io.*;

// A simple class to serialize
class Person implements Serializable {
    private static final long serialVersionUID = 1L; // Generated unique ID for the class
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + '}';
    }
}

public class SerializationExample {
    public static void main(String[] args) {
        // Creating an object to serialize
        Person person = new Person("John Doe", 25);

        // Serialization
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.ser"))) {
            oos.writeObject(person);
            System.out.println("Serialization successful");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialization
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.ser"))) {
            Person deserializedPerson = (Person) ois.readObject();
            System.out.println("Deserialization successful");
            System.out.println("Deserialized Person: " + deserializedPerson);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

In this example:

The Person class implements the Serializable interface.

An object of the Person class is created and serialized to a file called "person.ser."

The same object is deserialized from the file, and the deserialized data is printed.

Note the serialVersionUID field in the Person class. It's a version control for the serialization process.

If you modify the class later, it's good practice to update this ID to avoid compatibility issues.

Remember to handle exceptions appropriately in a real-world scenario, and also, it's important to close the streams properly using try-with-resources or by explicitly closing them in the finally block.

# More samples about Serialization in Java

Serialization is a powerful feature in Java, and it can be used in various scenarios. 

Let's explore a few more examples:

## Example 1: Collection Serialization

```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;

public class CollectionSerializationExample {
    public static void main(String[] args) {
        // Creating a list of objects to serialize
        List<String> colors = new ArrayList<>();
        colors.add("Red");
        colors.add("Green");
        colors.add("Blue");

        // Serialization
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("colors.ser"))) {
            oos.writeObject(colors);
            System.out.println("Serialization of List successful");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialization
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("colors.ser"))) {
            List<String> deserializedColors = (List<String>) ois.readObject();
            System.out.println("Deserialization of List successful");
            System.out.println("Deserialized Colors: " + deserializedColors);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

In this example, a list of strings is serialized and then deserialized.

## Example 2: Inheritance and Serialization

```java
import java.io.*;

class Animal implements Serializable {
    private static final long serialVersionUID = 1L;
    private String type;

    Animal(String type) {
        this.type = type;
    }

    @Override
    public String toString() {
        return "Animal{" + "type='" + type + '\'' + '}';
    }
}

class Dog extends Animal {
    private static final long serialVersionUID = 1L;
    private String breed;

    Dog(String type, String breed) {
        super(type);
        this.breed = breed;
    }

    @Override
    public String toString() {
        return "Dog{" + "type='" + getType() + "', breed='" + breed + '\'' + '}';
    }
}

public class InheritanceSerializationExample {
    public static void main(String[] args) {
        // Creating a Dog object to serialize
        Dog myDog = new Dog("Canine", "Golden Retriever");

        // Serialization
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("dog.ser"))) {
            oos.writeObject(myDog);
            System.out.println("Serialization of Dog successful");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialization
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("dog.ser"))) {
            Dog deserializedDog = (Dog) ois.readObject();
            System.out.println("Deserialization of Dog successful");
            System.out.println("Deserialized Dog: " + deserializedDog);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```
This example demonstrates serialization and deserialization of an object that inherits from another serialized object.

# More advanced topics about Serialization in Java

