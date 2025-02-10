

[Private Constructors in Java | Baeldung](https://www.baeldung.com/java-private-constructors)


private constructors in java and what is their use?

###### ChatGPT said:

ChatGPT

### **Private Constructors in Java**

A **private constructor** in Java is a constructor that is declared with the `private` access modifier, meaning it cannot be accessed outside the class in which it is defined.

### **Uses of Private Constructors**

1. **Restricting Object Creation (Singleton Pattern)**
    
    - A private constructor is often used in **Singleton Design Pattern**, ensuring that only one instance of a class is created.
    - Example:
        
        java
        
        CopyEdit
        
        `class Singleton {     private static Singleton instance;      private Singleton() {} // Private constructor      public static Singleton getInstance() {         if (instance == null) {             instance = new Singleton();         }         return instance;     } }`
        
    - This prevents external instantiation and ensures controlled object creation.
2. **Preventing Instantiation of Utility Classes**
    
    - In utility/helper classes (like `Math` or `Collections` in Java), object instantiation is unnecessary.
    - A private constructor prevents users from creating instances.
    - Example:
        
        java
        
        CopyEdit
        
        `class Utility {     private Utility() {         throw new UnsupportedOperationException("Cannot instantiate this class");     }      public static int add(int a, int b) {         return a + b;     } }`
        
    - This enforces a **static-only** class.
3. **Ensuring Non-instantiability in Abstract Classes**
    
    - Even though an abstract class cannot be instantiated, a subclass can instantiate it.
    - Using a private constructor prevents subclassing:
        
        java
        
        CopyEdit
        
        `abstract class Base {     private Base() {} // Prevents subclass instantiation }`
        
4. **Implementing Factory Methods**
    
    - A class can prevent direct instantiation and instead provide controlled object creation through static factory methods.
    - Example:
        
        java
        
        CopyEdit
        
        `class Factory {     private Factory() {}      public static Factory createInstance() {         return new Factory();     } }`
        

### **Key Takeaways**

- **Restricts direct instantiation** from outside the class.
- Used in **Singleton Pattern** to ensure a single instance.
- Prevents object creation in **Utility Classes**.
- Helps in **Factory Method Pattern** for controlled object creation.