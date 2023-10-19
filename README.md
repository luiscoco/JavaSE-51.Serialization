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
