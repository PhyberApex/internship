# Methods & Code Organization - Reference Handout

## What You'll Learn Today
- How to organize code with methods
- Declaring and calling methods
- Using parameters and return values
- Building a menu system

---

## Methods in Java
- **Method:** A block of code that does a specific task
- **Why use methods?**
    - Organize code
    - Avoid repetition
    - Make code easier to read

### Declaring a Method
```java
public static void sayHello() {
    System.out.println("Hello!");
}
```

### Calling a Method
```java
sayHello(); // prints Hello!
```

---

## Parameters and Return Values
- **Parameter:** Information you pass to a method
- **Return value:** What a method gives back

### Example:
```java
public static int add(int a, int b) {
    return a + b;
}

int sum = add(3, 5); // sum is 8
```

---

## Method Overloading
- Two or more methods with the same name but different parameters

### Example:
```java
public static void print(int x) {
    System.out.println(x);
}
public static void print(String s) {
    System.out.println(s);
}
```

---

## Mini-Exercises
1. Write a method to multiply two numbers
2. Write a method to print a welcome message
3. Try calling your methods from main

---

## Challenge: Menu System
- Build a text-based menu (e.g., calculator, greeting, exit)
- Use a method for each menu option
- Call methods from main based on user choice

### Example (Starter):
```java
import java.util.Scanner;

public class MenuSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (true) {
            printMenu();
            int choice = scanner.nextInt();
            if (choice == 1) greet();
            else if (choice == 2) addNumbers(scanner);
            else if (choice == 0) break;
            else System.out.println("Invalid choice");
        }
    }
    public static void printMenu() {
        System.out.println("1. Greet");
        System.out.println("2. Add Numbers");
        System.out.println("0. Exit");
        System.out.print("Choose: ");
    }
    public static void greet() {
        System.out.println("Hello, intern!");
    }
    public static void addNumbers(Scanner scanner) {
        System.out.print("Enter first number: ");
        int a = scanner.nextInt();
        System.out.print("Enter second number: ");
        int b = scanner.nextInt();
        System.out.println("Sum: " + (a + b));
    }
}
```

---

## Troubleshooting Tips
- **Method not found:** Check spelling and parameters
- **Wrong result:** Double-check your logic
- **Menu not working:** Make sure to call the right method for each choice

---

## End of Day Checklist
- [ ] Used methods to organize code
- [ ] Built a menu system
- [ ] Participated in meeting
- [ ] Asked at least one question

---

## Homework (Optional)
**Brainstorm:** Project ideas for next week

---

## Tomorrow's Preview: Project Work
- Start building your own Java project! 