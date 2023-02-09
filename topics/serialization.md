# **Serialization in Java**

## **Serialization**

- The process of converting an object into a byte stream.
- Persists (saves the state) the object after the program exits.
- This byte stream can be saved as a file ***or*** sent over a network. (can be sent to a different machine)
- Byte stream can be saved as a file (usually uses a `.ser` file extension) which is platform independent.
- Think of it as if you're saving a file with the obhect's information.

### **Steps to Serialize**

1. Object class implements `Serializable` interface
    - `User user = null;`
2. add `import java.io.Serializable;`
3. `FileOutputStream fileOut = new FileOutputStream(file path);`
4. `ObjectOutputStream out = new ObjectOutputStream(fileOut);`
5. `out.writeObject(objectName);`
6. `out.close(); fileOut.close();`

## **Deserialization**

- The reverse process of converting a byte stream into an object.
- Think of it as if you're loading a file.

### **Steps to Deserialize**

1. Declare the object (do not instantiate).
2. Object class implements `Serializable` interface
3. add `import java.io.Serializable;`
4. `FileInputStream fileIn - new FileInputStream(filePath;`
5. `ObjectInputStream in = new ObjectInputStream(fileIn);`
6. `objectName = (Class) in.readObject();`
7. `in.close(); fileIn.close();`

## **Example Code**
```Java
// example of serialization here
```
