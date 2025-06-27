# Password Generator Project 🔐

This is a progressive exercise that will take you through creating a password generator, starting with basic concepts and gradually adding more features. Work through each section at your own pace, making sure you understand the concepts before moving on.

!!! important "Before You Start"
    - The solutions provided are just ONE way to solve the problem. Your solution might look different, and that's perfectly fine!
    - Simply copying the solutions won't help you learn. You should be able to explain every line of code you write.
    - If you don't understand something, PLEASE ASK FOR HELP! It's better to ask questions than to copy code you don't understand.
    - Use the solutions to:
        - Check your work after you've tried solving it yourself
        - Learn different approaches to solving problems
        - Understand alternative implementations
        - Get unstuck when you're really stuck (but still make sure you understand why it works)
    - Remember: The goal is to learn and understand, not just to make it work!

## Level 1: Basic Password Generator

### Goal
Create a simple password generator that creates random passwords of a specified length.

### Requirements
1. Create a method that generates a random password
2. Password should be 8 characters long
3. Use only lowercase letters (a-z)
4. Print the generated password

!!! hint "Tips for Success"
    - Use the `Random` class for generating random numbers
    - Remember that strings in Java are zero-indexed
    - StringBuilder can be more efficient than String concatenation
    - Test your code with multiple generations to ensure randomness

!!! example "Starting Code"
    ```java
    import java.util.Random;

    public class PasswordGenerator {
        public static void main(String[] args) {
            String password = generatePassword();
            System.out.println("Your generated password is: " + password);
        }

        public static String generatePassword() {
            // Your code here
        }
    }
    ```

??? success "Solution"
    ```java
    import java.util.Random;

    public class PasswordGenerator {
        public static void main(String[] args) {
            String password = generatePassword();
            System.out.println("Your generated password is: " + password);
        }

        public static String generatePassword() {
            Random random = new Random();
            StringBuilder password = new StringBuilder();
            String letters = "abcdefghijklmnopqrstuvwxyz";
            
            for (int i = 0; i < 8; i++) {
                int index = random.nextInt(letters.length());
                password.append(letters.charAt(index));
            }
            
            return password.toString();
        }
    }
    ```

### Mini-Step 1.1: Add Password Length Validation
1. Create a method to check if password length is exactly 8
2. Print an error message if the length is wrong

??? success "Mini-Step 1.1 Solution"
    ```java
    public static boolean isValidLength(String password) {
        if (password.length() != 8) {
            System.out.println("Error: Password must be exactly 8 characters long");
            return false;
        }
        return true;
    }

    // In main method or where you generate the password:
    String password = generatePassword();
    if (!isValidLength(password)) {
        System.out.println("Generated password has invalid length!");
    }
    ```

### Mini-Step 1.2: Add Character Validation
1. Create a method to verify only lowercase letters are used
2. Print which characters were invalid (if any)

??? success "Mini-Step 1.2 Solution"
    ```java
    public static boolean containsOnlyLowercase(String password) {
        for (int i = 0; i < password.length(); i++) {
            char c = password.charAt(i);
            if (c < 'a' || c > 'z') {
                System.out.println("Invalid character found: " + c + " at position " + (i + 1));
                return false;
            }
        }
        return true;
    }

    // In main method or where you generate the password:
    String password = generatePassword();
    if (!containsOnlyLowercase(password)) {
        System.out.println("Generated password contains invalid characters!");
    }
    ```

## Level 2: Enhanced Password Generator

### Goal
Improve the password generator by adding more character types and allowing custom length.

### Requirements
1. Add support for:
   - Uppercase letters (A-Z)
   - Numbers (0-9)
   - Special characters (!@#$%^&*)
2. Allow user to specify password length (minimum 8)
3. Let user choose which character types to include
4. Ensure at least one character type is selected

!!! hint "Tips for Success"
    - Use Scanner.nextLine() instead of next() for better input handling
    - Consider what happens if no character types are selected
    - Test edge cases (minimum length, all options false, etc.)
    - Think about user experience when asking for input

!!! example "Starting Code"
    ```java
    import java.util.Random;
    import java.util.Scanner;

    public class PasswordGenerator {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            
            System.out.print("Enter password length (minimum 8): ");
            int length = scanner.nextInt();
            
            // Add your code to get user preferences for character types
            
            String password = generatePassword(length /* add other parameters as needed */);
            System.out.println("Your generated password is: " + password);
        }

        public static String generatePassword(int length /* add other parameters */) {
            // Your code here
        }
    }
    ```

??? success "Solution"
    ```java
    import java.util.Random;
    import java.util.Scanner;

    public class PasswordGenerator {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            
            // Get password length
            int length;
            do {
                System.out.print("Enter password length (minimum 8): ");
                length = scanner.nextInt();
                if (length < 8) {
                    System.out.println("Password must be at least 8 characters long!");
                }
            } while (length < 8);
            
            // Get character type preferences
            System.out.println("Include lowercase letters? (y/n): ");
            boolean includeLower = scanner.next().toLowerCase().equals("y");
            System.out.println("Include uppercase letters? (y/n): ");
            boolean includeUpper = scanner.next().toLowerCase().equals("y");
            System.out.println("Include numbers? (y/n): ");
            boolean includeNumbers = scanner.next().toLowerCase().equals("y");
            System.out.println("Include special characters? (y/n): ");
            boolean includeSpecial = scanner.next().toLowerCase().equals("y");
            
            String password = generatePassword(length, includeLower, includeUpper, 
                                            includeNumbers, includeSpecial);
            System.out.println("Your generated password is: " + password);
        }

        public static String generatePassword(int length, boolean includeLower, 
                                           boolean includeUpper, boolean includeNumbers, 
                                           boolean includeSpecial) {
            StringBuilder characters = new StringBuilder();
            Random random = new Random();
            
            if (includeLower) characters.append("abcdefghijklmnopqrstuvwxyz");
            if (includeUpper) characters.append("ABCDEFGHIJKLMNOPQRSTUVWXYZ");
            if (includeNumbers) characters.append("0123456789");
            if (includeSpecial) characters.append("!@#$%^&*");
            
            if (characters.length() == 0) {
                System.out.println("Warning: No character types selected. Using lowercase letters.");
                characters.append("abcdefghijklmnopqrstuvwxyz");
            }
            
            StringBuilder password = new StringBuilder();
            for (int i = 0; i < length; i++) {
                int index = random.nextInt(characters.length());
                password.append(characters.charAt(index));
            }
            
            return password.toString();
        }
    }
    ```

### Mini-Step 2.1: Add Length Control
1. Modify generatePassword to accept length parameter
2. Add validation for minimum length

??? success "Mini-Step 2.1 Solution"
    ```java
    public static String generatePassword(int length) {
        if (length < 8) {
            throw new IllegalArgumentException("Password length must be at least 8 characters");
        }
        
        Random random = new Random();
        StringBuilder password = new StringBuilder();
        String letters = "abcdefghijklmnopqrstuvwxyz";
        
        for (int i = 0; i < length; i++) {
            int index = random.nextInt(letters.length());
            password.append(letters.charAt(index));
        }
        
        return password.toString();
    }

    // In main method:
    try {
        String password = generatePassword(6); // This will throw an exception
    } catch (IllegalArgumentException e) {
        System.out.println("Error: " + e.getMessage());
    }
    ```

### Mini-Step 2.2: Add Character Types
1. Add uppercase letters support
2. Add numbers support
3. Add special characters support

??? success "Mini-Step 2.2 Solution"
    ```java
    public static String generatePassword(int length, boolean includeUppercase, 
                                       boolean includeNumbers, boolean includeSpecial) {
        StringBuilder characters = new StringBuilder("abcdefghijklmnopqrstuvwxyz");
        
        if (includeUppercase) {
            characters.append("ABCDEFGHIJKLMNOPQRSTUVWXYZ");
        }
        if (includeNumbers) {
            characters.append("0123456789");
        }
        if (includeSpecial) {
            characters.append("!@#$%^&*");
        }
        
        Random random = new Random();
        StringBuilder password = new StringBuilder();
        
        for (int i = 0; i < length; i++) {
            int index = random.nextInt(characters.length());
            password.append(characters.charAt(index));
        }
        
        return password.toString();
    }

    // In main method:
    String password = generatePassword(8, true, true, false);
    System.out.println("Password with uppercase and numbers: " + password);
    ```

## Level 3: Advanced Features

### Goal
Add password strength checking and additional features.

### Requirements
1. Add a password strength checker that considers:
   - Length
   - Mix of character types
   - Common patterns to avoid
2. Generate multiple password options
3. Allow saving passwords to a file
4. Add a method to check if a password contains common words

!!! hint "Tips for Success"
    - Break down the strength checker into smaller parts
    - Consider using regex for pattern matching
    - Remember to close file resources properly
    - Think about password security best practices

!!! example "Starting Code"
    ```java
    import java.util.Random;
    import java.util.Scanner;
    import java.io.FileWriter;
    import java.io.IOException;

    public class PasswordGenerator {
        public static void main(String[] args) {
            // Previous code here...
            
            String password = generatePassword(/* parameters */);
            int strength = checkPasswordStrength(password);
            printPasswordStrength(strength);
        }

        public static int checkPasswordStrength(String password) {
            // Your code here
            // Return a score from 1-5
        }

        public static void printPasswordStrength(int strength) {
            // Your code here
        }

        public static void savePasswordToFile(String password) {
            // Your code here
        }
    }
    ```

??? success "Solution"
    ```java
    import java.util.Random;
    import java.util.Scanner;
    import java.io.FileWriter;
    import java.io.IOException;
    import java.time.LocalDateTime;

    public class PasswordGenerator {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            
            // Previous input code here...
            
            System.out.println("How many passwords would you like to generate? ");
            int count = scanner.nextInt();
            
            for (int i = 0; i < count; i++) {
                String password = generatePassword(length, includeLower, includeUpper, 
                                                includeNumbers, includeSpecial);
                int strength = checkPasswordStrength(password);
                System.out.println("\nPassword #" + (i + 1) + ": " + password);
                printPasswordStrength(strength);
                
                System.out.println("Would you like to save this password? (y/n): ");
                if (scanner.next().toLowerCase().equals("y")) {
                    savePasswordToFile(password);
                }
            }
        }

        public static int checkPasswordStrength(String password) {
            int score = 0;
            
            // Length check
            if (password.length() >= 12) score += 2;
            else if (password.length() >= 8) score += 1;
            
            // Character type checks
            if (password.matches(".*[a-z].*")) score += 1;
            if (password.matches(".*[A-Z].*")) score += 1;
            if (password.matches(".*[0-9].*")) score += 1;
            if (password.matches(".*[!@#$%^&*].*")) score += 1;
            
            // Check for common patterns
            if (password.matches(".*123.*") || 
                password.matches(".*abc.*") || 
                password.matches(".*password.*")) {
                score -= 1;
            }
            
            return Math.max(1, Math.min(5, score)); // Keep score between 1-5
        }

        public static void printPasswordStrength(int strength) {
            System.out.print("Password Strength: ");
            switch (strength) {
                case 1: System.out.println("Very Weak ❌"); break;
                case 2: System.out.println("Weak ⚠️"); break;
                case 3: System.out.println("Medium ⚠️"); break;
                case 4: System.out.println("Strong ✅"); break;
                case 5: System.out.println("Very Strong 💪"); break;
            }
        }

        public static void savePasswordToFile(String password) {
            try {
                FileWriter writer = new FileWriter("passwords.txt", true);
                writer.write(LocalDateTime.now() + ": " + password + "\n");
                writer.close();
                System.out.println("Password saved to file!");
            } catch (IOException e) {
                System.out.println("Error saving password to file: " + e.getMessage());
            }
        }
    }
    ```

### Mini-Step 3.1: Basic Strength Checking
1. Implement length checking
2. Add character variety checking
3. Create simple scoring system

??? success "Mini-Step 3.1 Solution"
    ```java
    public static int calculateBasicStrength(String password) {
        int score = 0;
        
        // Length check
        if (password.length() >= 12) score += 2;
        else if (password.length() >= 8) score += 1;
        
        // Character variety check
        if (password.matches(".*[a-z].*")) score += 1;
        if (password.matches(".*[A-Z].*")) score += 1;
        if (password.matches(".*[0-9].*")) score += 1;
        if (password.matches(".*[!@#$%^&*].*")) score += 1;
        
        return Math.min(5, score); // Cap score at 5
    }

    // In main method:
    String password = generatePassword(/* parameters */);
    int strength = calculateBasicStrength(password);
    System.out.println("Password strength (1-5): " + strength);
    ```

### Mini-Step 3.2: Pattern Detection
1. Add common sequence detection
2. Add repeated character detection

??? success "Mini-Step 3.2 Solution"
    ```java
    public static boolean hasCommonPatterns(String password) {
        // Check for common sequences
        String[] commonSequences = {"123", "abc", "qwerty", "password"};
        for (String sequence : commonSequences) {
            if (password.toLowerCase().contains(sequence)) {
                System.out.println("Warning: Contains common sequence: " + sequence);
                return true;
            }
        }
        
        // Check for repeated characters
        for (int i = 0; i < password.length() - 2; i++) {
            if (password.charAt(i) == password.charAt(i + 1) && 
                password.charAt(i) == password.charAt(i + 2)) {
                System.out.println("Warning: Contains repeated character: " + 
                                 password.charAt(i));
                return true;
            }
        }
        
        return false;
    }

    // In main method:
    String password = generatePassword(/* parameters */);
    if (hasCommonPatterns(password)) {
        System.out.println("Password contains common patterns and might be weak");
    }
    ```

### Mini-Step 3.3: File Operations
1. Add basic file writing
2. Add error handling

??? success "Mini-Step 3.3 Solution"
    ```java
    public static void savePassword(String password, String filename) {
        try (FileWriter writer = new FileWriter(filename, true)) {
            writer.write(password + "\n");
            System.out.println("Password saved successfully!");
        } catch (IOException e) {
            System.out.println("Error saving password: " + e.getMessage());
        }
    }

    public static void savePasswordWithMetadata(String password, int strength) {
        try (FileWriter writer = new FileWriter("passwords.txt", true)) {
            String timestamp = LocalDateTime.now().toString();
            writer.write(String.format("%s | Strength: %d | %s%n", 
                        timestamp, strength, password));
            System.out.println("Password saved with metadata!");
        } catch (IOException e) {
            System.out.println("Error saving password: " + e.getMessage());
            // Optionally, create the file if it doesn't exist
            try {
                new File("passwords.txt").createNewFile();
                System.out.println("Created new passwords file");
                savePasswordWithMetadata(password, strength); // Try again
            } catch (IOException ex) {
                System.out.println("Could not create passwords file");
            }
        }
    }

    // In main method:
    String password = generatePassword(/* parameters */);
    int strength = calculateBasicStrength(password);
    savePasswordWithMetadata(password, strength);
    ```

## Bonus Challenge: Object-Oriented Version

Once you're comfortable with object-oriented programming concepts, try refactoring the password generator into a class-based version!

### Requirements
1. Create a `PasswordGenerator` class with:
   - Instance variables for preferences
   - Constructor(s) for initialization
   - Methods for generation and validation
2. Create a `Password` class to represent a password with:
   - Strength checking
   - Save/load functionality
   - toString() method
3. Add a `PasswordStrength` enum
4. Consider adding interfaces for different generation strategies

!!! hint "OOP Tips"
    - Think about what should be static vs instance methods
    - Consider which fields should be private vs public
    - Use enums for fixed sets of values
    - Consider using the Builder pattern for configuration
    - Think about how to make the code more maintainable and reusable

??? example "Object-Oriented Structure"
    ```java
    // This is just the structure - try implementing it yourself!
    
    public class PasswordGenerator {
        private boolean includeLower;
        private boolean includeUpper;
        private boolean includeNumbers;
        private boolean includeSpecial;
        private int defaultLength;
        
        // Constructor
        
        // Generation methods
        
        // Utility methods
    }

    public class Password {
        private String value;
        private PasswordStrength strength;
        private LocalDateTime generatedAt;
        
        // Constructor
        
        // Methods
    }

    public enum PasswordStrength {
        VERY_WEAK(1, "Very Weak ❌"),
        WEAK(2, "Weak ⚠️"),
        MEDIUM(3, "Medium ⚠️"),
        STRONG(4, "Strong ✅"),
        VERY_STRONG(5, "Very Strong 💪");
        
        // Enum implementation
    }
    ```

Remember:

   - Test your code with different inputs
   - Add comments to explain your logic
   - Consider edge cases
   - Think about user experience
   - Keep your code organized

!!! tip "Pro Tip"
    Use the Java documentation to learn more about the classes and methods you're using!

??? success "Complete OOP Solution"
    ```java
    import java.io.FileWriter;
    import java.io.IOException;
    import java.time.LocalDateTime;
    import java.util.Random;
    import java.util.ArrayList;
    import java.util.List;

    // Enum to represent password strength levels
    public enum PasswordStrength {
        VERY_WEAK(1, "Very Weak ❌"),
        WEAK(2, "Weak ⚠️"),
        MEDIUM(3, "Medium ⚠️"),
        STRONG(4, "Strong ✅"),
        VERY_STRONG(5, "Very Strong 💪");

        private final int score;
        private final String description;

        PasswordStrength(int score, String description) {
            this.score = score;
            this.description = description;
        }

        public static PasswordStrength fromScore(int score) {
            for (PasswordStrength strength : values()) {
                if (strength.score == score) return strength;
            }
            return VERY_WEAK; // Default
        }

        @Override
        public String toString() {
            return description;
        }
    }

    // Interface for different password generation strategies
    public interface PasswordGenerationStrategy {
        String generatePassword(int length, CharacterPool pool);
    }

    // Basic random generation strategy
    public class RandomGenerationStrategy implements PasswordGenerationStrategy {
        private final Random random = new Random();

        @Override
        public String generatePassword(int length, CharacterPool pool) {
            StringBuilder password = new StringBuilder();
            String characters = pool.getCharacters();
            
            for (int i = 0; i < length; i++) {
                password.append(characters.charAt(random.nextInt(characters.length())));
            }
            
            return password.toString();
        }
    }

    // Class to manage available characters for password generation
    public class CharacterPool {
        private final StringBuilder characters = new StringBuilder();
        
        public void addLowercase() {
            characters.append("abcdefghijklmnopqrstuvwxyz");
        }
        
        public void addUppercase() {
            characters.append("ABCDEFGHIJKLMNOPQRSTUVWXYZ");
        }
        
        public void addNumbers() {
            characters.append("0123456789");
        }
        
        public void addSpecial() {
            characters.append("!@#$%^&*");
        }
        
        public String getCharacters() {
            return characters.toString();
        }
        
        public boolean isEmpty() {
            return characters.length() == 0;
        }
    }

    // Class to represent a password
    public class Password {
        private final String value;
        private final LocalDateTime generatedAt;
        private final PasswordStrength strength;
        
        public Password(String value) {
            this.value = value;
            this.generatedAt = LocalDateTime.now();
            this.strength = calculateStrength();
        }
        
        private PasswordStrength calculateStrength() {
            int score = 0;
            
            // Length check
            if (value.length() >= 12) score += 2;
            else if (value.length() >= 8) score += 1;
            
            // Character variety check
            if (value.matches(".*[a-z].*")) score += 1;
            if (value.matches(".*[A-Z].*")) score += 1;
            if (value.matches(".*[0-9].*")) score += 1;
            if (value.matches(".*[!@#$%^&*].*")) score += 1;
            
            // Pattern check
            if (hasCommonPatterns()) score -= 1;
            
            return PasswordStrength.fromScore(Math.max(1, Math.min(5, score)));
        }
        
        private boolean hasCommonPatterns() {
            String[] patterns = {"123", "abc", "password", "qwerty"};
            for (String pattern : patterns) {
                if (value.toLowerCase().contains(pattern)) return true;
            }
            return false;
        }
        
        public void save() throws IOException {
            try (FileWriter writer = new FileWriter("passwords.txt", true)) {
                writer.write(String.format("%s | %s | %s%n", 
                    generatedAt, strength, value));
            }
        }
        
        @Override
        public String toString() {
            return String.format("Password: %s (Strength: %s)", value, strength);
        }
    }

    // Main password generator class
    public class PasswordGenerator {
        private final PasswordGenerationStrategy strategy;
        private final CharacterPool characterPool;
        private int defaultLength;
        
        // Builder pattern for configuration
        public static class Builder {
            private boolean includeLower = true;
            private boolean includeUpper = false;
            private boolean includeNumbers = false;
            private boolean includeSpecial = false;
            private int defaultLength = 8;
            
            public Builder withLowercase(boolean include) {
                this.includeLower = include;
                return this;
            }
            
            public Builder withUppercase(boolean include) {
                this.includeUpper = include;
                return this;
            }
            
            public Builder withNumbers(boolean include) {
                this.includeNumbers = include;
                return this;
            }
            
            public Builder withSpecial(boolean include) {
                this.includeSpecial = include;
                return this;
            }
            
            public Builder withDefaultLength(int length) {
                if (length < 8) {
                    throw new IllegalArgumentException("Length must be at least 8");
                }
                this.defaultLength = length;
                return this;
            }
            
            public PasswordGenerator build() {
                return new PasswordGenerator(this);
            }
        }
        
        private PasswordGenerator(Builder builder) {
            this.strategy = new RandomGenerationStrategy();
            this.characterPool = new CharacterPool();
            this.defaultLength = builder.defaultLength;
            
            if (builder.includeLower) characterPool.addLowercase();
            if (builder.includeUpper) characterPool.addUppercase();
            if (builder.includeNumbers) characterPool.addNumbers();
            if (builder.includeSpecial) characterPool.addSpecial();
            
            if (characterPool.isEmpty()) {
                characterPool.addLowercase(); // Default to lowercase
            }
        }
        
        public Password generatePassword() {
            return generatePassword(defaultLength);
        }
        
        public Password generatePassword(int length) {
            if (length < 8) {
                throw new IllegalArgumentException("Length must be at least 8");
            }
            
            String value = strategy.generatePassword(length, characterPool);
            return new Password(value);
        }
        
        public List<Password> generateMultiplePasswords(int count) {
            List<Password> passwords = new ArrayList<>();
            for (int i = 0; i < count; i++) {
                passwords.add(generatePassword());
            }
            return passwords;
        }
    }

    // Example usage
    public class Main {
        public static void main(String[] args) {
            // Create a password generator with custom configuration
            PasswordGenerator generator = new PasswordGenerator.Builder()
                .withUppercase(true)
                .withNumbers(true)
                .withSpecial(true)
                .withDefaultLength(12)
                .build();
            
            // Generate a single password
            Password password = generator.generatePassword();
            System.out.println(password);
            
            // Generate multiple passwords
            List<Password> passwords = generator.generateMultiplePasswords(5);
            passwords.forEach(p -> {
                System.out.println(p);
                try {
                    p.save(); // Save each password to file
                } catch (IOException e) {
                    System.out.println("Error saving password: " + e.getMessage());
                }
            });
        }
    }
    ```

The OOP solution demonstrates several important object-oriented principles and patterns:

1. **Encapsulation**
   - Each class has clear responsibilities
   - Private fields with public methods
   - Immutable Password class

2. **Design Patterns**
   - Builder pattern for PasswordGenerator configuration
   - Strategy pattern for password generation algorithms
   - Factory method in PasswordStrength

3. **SOLID Principles**
   - Single Responsibility Principle: Each class has one job
   - Open/Closed Principle: Easy to extend with new generation strategies
   - Interface Segregation: Clean interfaces for different behaviors

4. **Error Handling**
   - Proper exception handling
   - Input validation
   - Safe file operations

5. **Extensibility**
   - Easy to add new password generation strategies
   - Easy to modify strength calculation
   - Easy to add new character types

Key Features:
- Configurable password generation
- Password strength calculation
- File storage
- Multiple password generation
- Pattern detection
- Comprehensive toString methods
- Builder pattern for easy configuration
- Strategy pattern for generation algorithms

Remember:
- This is just one possible implementation
- You can modify and extend it based on your needs
- Focus on understanding the principles behind the design
- Try implementing your own variations

[Rest of the file remains the same] 