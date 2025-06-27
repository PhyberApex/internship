# Java Basics - Reference Handout

## What You'll Learn Today
- Set up your Java development environment
- Understand what Java is and why it's important
- Write and run your first Java programs
- Participate in your first team meeting

---

## Java Quick Facts

### What is Java?
- **Programming Language**: Used to create software applications
- **Platform Independent**: Code runs on Windows, Mac, Linux
- **Compiled Language**: Code is translated to bytecode before running
- **Popular Uses**: Web applications, mobile apps, enterprise software

### Key Java Concepts
- **JDK**: Java Development Kit (tools for writing Java)
- **JVM**: Java Virtual Machine (runs your programs)
- **Bytecode**: Translated version of your code that JVM understands

---

## Basic Java Program Structure

```java
public class ClassName {
    public static void main(String[] args) {
        // Your code goes here
        System.out.println("Hello, World!");
    }
}
```

### Breaking it Down:
- **`public class ClassName`**: Creates a container for your code
- **`public static void main`**: The starting point of your program
- **`String[] args`**: Allows command line input (ignore for now)
- **`System.out.println()`**: Prints text to the screen
- **`//`**: Creates a comment (ignored by computer)

---

## Essential Commands

### Print to Screen
```java
System.out.println("Text here");  // Prints and moves to next line
System.out.print("Text here");    // Prints without moving to next line
```

### Special Characters
- **`\n`**: New line
- **`\t`**: Tab space
- **`\"`**: Quotation mark inside text

### Example:
```java
System.out.println("Hello\nWorld");  // Prints Hello on one line, World on next
System.out.println("She said \"Hi\"");  // Prints: She said "Hi"
```

---

## Naming Rules

### Class Names
- Start with capital letter
- Use PascalCase: `MyFirstClass`, `StudentRecord`
- No spaces, no special characters except underscore

### Method Names
- Start with lowercase letter
- Use camelCase: `printMessage`, `calculateTotal`

### Good Examples:
- ✅ `HelloWorld`
- ✅ `PersonalIntroduction`
- ✅ `MyCalculator`

### Bad Examples:
- ❌ `hello world` (space)
- ❌ `my-class` (hyphen)
- ❌ `2ndProgram` (starts with number)

---

## Today's Programs

### Program 1: Hello World
**Purpose**: Learn basic structure and run first program
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### Program 2: Personal Introduction
**Purpose**: Practice printing multiple lines
**Your Task**: Create a program that prints:
- Your name
- Your age
- Your favorite hobby
- Why you're interested in programming

### Program 3: ASCII Art Challenge
**Purpose**: Practice with multiple print statements
**Your Task**: Print your initials using asterisks (*)

---

## Meeting Participation Tips

### What to Do:
- ✅ Listen actively
- ✅ Take notes on technical terms you don't understand
- ✅ Observe how team members communicate
- ✅ Ask questions during appropriate breaks

### What to Avoid:
- ❌ Using your phone
- ❌ Interrupting ongoing discussions
- ❌ Feeling pressured to contribute immediately

---

## Troubleshooting Common Issues

### Error: "Could not find or load main class"
**Solution**: Make sure your class name matches your file name exactly

### Error: "';' expected"
**Solution**: Check that every statement ends with a semicolon (;)

### Error: "cannot find symbol"
**Solution**: Check spelling of commands like `System.out.println`

### Program Doesn't Print Anything
**Solution**: Make sure your text is inside quotation marks

---

## IntelliJ IDEA Quick Reference

### Essential Buttons/Actions:
- **Green Play Button (▶️)**: Run your program
- **Red Square (⏹️)**: Stop running program
- **Ctrl + S**: Save your work
- **Ctrl + Z**: Undo last action

### Project Structure:
```
JavaInternship/
├── src/
│   ├── HelloWorld.java
│   ├── PersonalIntro.java
│   └── (your other programs)
```

---

## End of Day Checklist

- [ ] Java JDK installed and working
- [ ] IntelliJ IDEA installed and configured
- [ ] Successfully ran "Hello World" program
- [ ] Created personal introduction program
- [ ] Attended first team meeting
- [ ] Attempted ASCII art challenge
- [ ] Understand basic Java program structure

---

## Questions for Self-Reflection

1. What was the most challenging part of today?
2. What concept do you want to understand better?
3. How did the team meeting help you understand the work environment?
4. What questions do you have for tomorrow?

---

## Homework (Optional)
**Research Topic**: "What are variables in programming?"
**Goal**: Come prepared to discuss what you learned

**Resources**:
- Oracle Java Documentation: https://docs.oracle.com/javase/tutorial/
- Search: "Java variables tutorial"

---

## Tomorrow's Preview: Variables and Data Types
- Learn to store and use information in your programs
- Make programs that can work with numbers and text
- Create a simple calculator

**Bring Tomorrow**:
- This handout
- Any questions from today
- Curiosity about making programs more interactive!