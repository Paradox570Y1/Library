## **1. What is a package?**

A **package** in Java is like a folder for your classes and interfaces — it organizes related code and avoids naming conflicts.

- Example: `java.util` is a package containing utility classes like `ArrayList`, `HashMap`, etc.
    

---

## **2. Creating a Package**

**Step 1: Create a directory structure matching your package name**  
Package names follow **reverse domain naming** to keep them unique:

`mkdir -p src/com/example/mypackage`

**Step 2: Create your Java file with `package` declaration**  `src/com/example/mypackage/MyClass.java`:

java

Copy code

```java
package com.example.mypackage;

public class MyClass {
    public void sayHello() {
        System.out.println("Hello from MyClass!");
    }
}
```

**Step 3: Compile with the correct path**  
From the `src` directory:

`javac com/example/mypackage/MyClass.java`

This will create `MyClass.class` inside the same directory structure.

---

## **3. Using the Package**

Create another file outside the package — e.g., `src/TestPackage.java`:

```java
import com.example.mypackage.MyClass; // Importing class from our package

public class TestPackage {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.sayHello();
    }
}
```

`javac TestPackage.java`

Run (make sure your `src` folder is in the classpath):


`java -cp . TestPackage`

---

## **4. Things to Take Care of When Dealing with Packages**

|**Point**|**Explanation**|
|---|---|
|**Package statement**|Must be the **first non-comment line** in the file.|
|**Directory structure**|Must match the package name exactly (case-sensitive).|
|**ClassPath**|When running, ensure the root of the package structure is in the `classpath`.|
|**Unique naming**|Use reverse domain naming to avoid clashes (`com.mycompany.project`).|
|**Access modifiers**|Default (no modifier) = accessible only in the same package. Use `public` if needed outside.|
|**No mixing**|One `.java` file can only belong to **one** package.|
|**Avoid cyclic dependencies**|Keep packages logically separated to prevent circular imports.|
|**Avoid naming conflicts**|If two packages have a class with the same name, you must fully qualify it (`packageA.ClassName`).|

---

## **5. Quick Example with Multiple Classes**

```java
src/
 ├── com/example/utils/Printer.java
 ├── com/example/models/User.java
 └── MainApp.java
```

**Printer.java**

```java
package com.example.utils;

public class Printer {
    public static void printMessage(String msg) {
        System.out.println(msg);
    }
}
```

**User.java**
```java
package com.example.models;

public class User {
    public String name;
    public User(String name) { this.name = name; }
}
```

**MainApp.java**
```java
import com.example.utils.Printer;
import com.example.models.User;

public class MainApp {
    public static void main(String[] args) {
        User user = new User("Alice");
        Printer.printMessage("Welcome, " + user.name);
    }
}
```

Compile all at once:

```java
javac com/example/utils/Printer.java com/example/models/User.java MainApp.java
```

Run:

`java MainApp`