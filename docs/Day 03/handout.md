# Conditionals & Logic - Reference Handout

## What You'll Learn Today
- How to make decisions in your programs
- Using if/else and switch statements
- Combining conditions with logical operators
- Building a grade calculator

---

## Conditionals in Java
- **if:** Runs code if a condition is true
- **else if:** Checks another condition if the first is false
- **else:** Runs if none of the above are true

### Example:
```java
int score = 85;
if (score >= 90) {
    System.out.println("A");
} else if (score >= 80) {
    System.out.println("B");
} else {
    System.out.println("C or below");
}
```

---

## Comparison & Logical Operators
- **==** (equals), **!=** (not equal), **<**, **>**, **<=**, **>=**
- **&&** (and), **||** (or), **!** (not)

### Example:
```java
int age = 16;
if (age >= 13 && age <= 19) {
    System.out.println("Teenager");
}
```

---

## Switch Statements
- Use when you have many possible values for one variable

### Example:
```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Other day");
}
```

---

## Mini-Exercises
1. Write a program to check if a number is positive, negative, or zero
2. Use switch to print the name of the day for a number (1-7)

---

## Challenge: Grade Calculator
- Ask the user for a score (0-100)
- Print the letter grade (A, B, C, D, F)
- Try both if/else and switch approaches

### Example (Starter):
```java
import java.util.Scanner;

public class GradeCalculator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter your score: ");
        int score = scanner.nextInt();
        if (score >= 90) {
            System.out.println("A");
        } else if (score >= 80) {
            System.out.println("B");
        } else if (score >= 70) {
            System.out.println("C");
        } else if (score >= 60) {
            System.out.println("D");
        } else {
            System.out.println("F");
        }
    }
}
```

---

## Troubleshooting Tips
- **Wrong grade:** Double-check your conditions
- **No output:** Make sure your if/else covers all cases
- **Switch not working:** Remember to use break after each case

---

## End of Day Checklist
- [ ] Used if/else and switch
- [ ] Built a grade calculator
- [ ] Participated in meeting
- [ ] Asked at least one question

---

## Homework (Optional)
**Research Topic:** "How do loops work in Java?"

**Resource:**
- https://www.w3schools.com/java/java_loops.asp

---

## Tomorrow's Preview: Loops
- Repeat actions with for, while, and do-while
- Build a number guessing game 