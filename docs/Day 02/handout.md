# Variables, Data Types & Input - Reference Handout

## What You'll Learn Today
- What variables are and why we use them
- Different data types in Java
- How to get input from the user
- How to build a simple calculator

---

## Variables in Java
- **Variable:** A container for storing data
- **Declaration:** Telling Java what type of data you want to store
- **Initialization:** Giving your variable a value

### Example:
```java
int age = 15; // declares an integer variable called age
String name = "Alex"; // declares a String variable called name
```

---

## Common Data Types
- **int:** Whole numbers (e.g., 5, -3, 100)
- **double:** Decimal numbers (e.g., 3.14, -0.5)
- **boolean:** true or false
- **char:** Single character (e.g., 'A', 'z')
- **String:** Text (e.g., "Hello")

---

## Getting User Input
- Use the **Scanner** class to read input from the keyboard

### Example:
```java
import java.util.Scanner;

public class InputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();
        System.out.println("Hello, " + name + "!");
    }
}
```

---

## Type Conversion (Casting)
- Sometimes you need to change one type to another
- Example: turning a double into an int

```java
double price = 9.99;
int rounded = (int) price; // rounded is 9
```

---

## Mini-Exercises
1. Ask the user for their favorite number and print it
2. Ask for their age and print a message
3. Try changing variable types and see what happens

---

## Challenge: Build a Simple Calculator
- Ask the user for two numbers
- Ask for an operation (+, -, *, /)
- Print the result

### Example (Starter):
```java
import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter first number: ");
        int num1 = scanner.nextInt();
        System.out.print("Enter second number: ");
        int num2 = scanner.nextInt();
        System.out.print("Enter operation (+, -, *, /): ");
        String op = scanner.next();
        int result = 0;
        if (op.equals("+")) {
            result = num1 + num2;
        } else if (op.equals("-")) {
            result = num1 - num2;
        } else if (op.equals("*")) {
            result = num1 * num2;
        } else if (op.equals("/")) {
            result = num1 / num2;
        }
        System.out.println("Result: " + result);
    }
}
```

---

## Troubleshooting Tips
- **InputMismatchException:** Make sure you enter the right type (e.g., a number for int)
- **Variable not found:** Check your spelling
- **Result is wrong:** Double-check your operations

---

## End of Day Checklist
- [ ] Declared and used variables
- [ ] Used Scanner to get user input
- [ ] Built a simple calculator
- [ ] Participated in meeting
- [ ] Asked at least one question

---

## Homework (Optional)
**Research Topic:** "How do if/else statements work in Java?"

**Resource:**
- https://www.w3schools.com/java/java_conditions.asp

---

## Tomorrow's Preview: Conditionals
- Make your programs smarter with decisions
- Learn about if/else and switch
- Try building a grade calculator