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
5. Validate the generated password meets requirements

### Mini-Step 1.1: Create the Basic Structure
1. Set up the basic class structure
2. Create the generatePassword method
3. Add main method to test your generator

??? question "Need help with the basic structure?"
    Think about:
    - What imports will you need?
    - What should generatePassword return?
    - How will you test it works?
    
    Hint: Start with this structure and think about what goes where:
    ```java
    import java.util.Random;

    public class PasswordGenerator {
        public static void main(String[] args) {
            // How will you test your generator?
        }

        public static String generatePassword() {
            // What steps do you need here?
        }
    }
    ```

### Mini-Step 1.2: Generate Random Letters
1. Create a string of lowercase letters
2. Learn to select random positions
3. Pick one random letter

??? question "Need help with random selection?"
    Think about:
    - How can you represent all lowercase letters?
    - How do you get a random number in a specific range?
    - How do you get a character at a specific position?
    
    Technical Hints:
    ```java
    // Approach 1: Direct string definition
    String letters = "abcdefghijklmnopqrstuvwxyz";
    
    // Approach 2: ASCII value generation
    StringBuilder letters = new StringBuilder();
    for (char c = 'a'; c <= 'z'; c++) {
        letters.append(c);
    }
    
    // Approach 3: Using character array
    char[] letters = "abcdefghijklmnopqrstuvwxyz".toCharArray();
    
    // Random selection approaches:
    // Approach 1: Using nextInt (most common)
    int index = random.nextInt(letters.length());
    char letter = letters.charAt(index);
    
    // Approach 2: Using nextDouble
    int index = (int)(random.nextDouble() * letters.length());
    char letter = letters.charAt(index);
    
    // Approach 3: Using streams (Java 8+)
    String letters = "abcdefghijklmnopqrstuvwxyz";
    char randomLetter = letters.chars()
        .mapToObj(ch -> (char)ch)
        .skip(random.nextInt(letters.length()))
        .findFirst()
        .get();
    ```

### Mini-Step 1.3: Build the Password
1. Create a loop to generate 8 characters
2. Store and combine the characters efficiently
3. Return the final password

??? question "Need help building the password?"
    Think about:
    - How many times should your loop run?
    - What's the best way to combine characters?
    - How will you store the result?
    
    Hint: Consider using StringBuilder:
    - It's more efficient than String concatenation
    - You can add characters one at a time
    - Convert to String at the end

### Mini-Step 1.4: Add Validation
1. Check the password length
2. Verify only lowercase letters are used
3. Add error messages for invalid passwords

??? question "Need help with validation?"
    Think about:
    - What makes a password valid?
    - How can you check each character?
    - What should happen if validation fails?
    
    Hint: For each character:
    - Is it between 'a' and 'z'?
    - What message would help the user?
    - Should you stop at first error or show all?

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

??? success "Complete Level 1 Solution"
    ```java
    import java.util.Random;

    public class PasswordGenerator {
        private static final Random random = new Random();
        private static final String LOWERCASE_LETTERS = "abcdefghijklmnopqrstuvwxyz";
        
        public static void main(String[] args) {
            String password = generatePassword();
            if (isValidPassword(password)) {
                System.out.println("Your generated password is: " + password);
            } else {
                System.out.println("Failed to generate valid password!");
            }
        }

        public static String generatePassword() {
            StringBuilder password = new StringBuilder();
            for (int i = 0; i < 8; i++) {
                int index = random.nextInt(LOWERCASE_LETTERS.length());
                password.append(LOWERCASE_LETTERS.charAt(index));
            }
            return password.toString();
        }
        
        public static boolean isValidPassword(String password) {
            if (password.length() != 8) {
                System.out.println("Error: Password must be exactly 8 characters");
                return false;
            }
            
            for (char c : password.toCharArray()) {
                if (c < 'a' || c > 'z') {
                    System.out.println("Error: Invalid character found: " + c);
                    return false;
                }
            }
            return true;
        }
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

### Mini-Step 2.1: Expand Character Sets
1. Create constants for each character type
2. Modify the generator to use multiple character sets
3. Test with all character types enabled

!!! tip "Building on Level 1"
    Remember how we handled lowercase letters in Level 1? We'll use the same technique but expand it:
    - Instead of one character set, we'll manage multiple sets
    - The random selection process remains the same
    - We'll combine sets when needed

??? question "Need help with character sets?"
    Technical Hints:
    ```java
    // Approach 1: Direct string constants
    private static final String LOWERCASE = "abcdefghijklmnopqrstuvwxyz";
    private static final String UPPERCASE = LOWERCASE.toUpperCase();
    private static final String NUMBERS = "0123456789";
    private static final String SPECIAL = "!@#$%^&*";
    
    // Approach 2: Character ranges
    private static String generateCharRange(char start, char end) {
        StringBuilder range = new StringBuilder();
        for (char c = start; c <= end; c++) {
            range.append(c);
        }
        return range.toString();
    }
    private static final String LOWERCASE = generateCharRange('a', 'z');
    private static final String NUMBERS = generateCharRange('0', '9');
    
    // Approach 3: Using arrays and joining
    private static final char[][] CHAR_SETS = {
        "abcdefghijklmnopqrstuvwxyz".toCharArray(),
        "ABCDEFGHIJKLMNOPQRSTUVWXYZ".toCharArray(),
        "0123456789".toCharArray(),
        "!@#$%^&*".toCharArray()
    };
    
    // Different ways to combine character sets:
    // Approach 1: StringBuilder (most efficient)
    private static String buildCharacterPool(boolean[] useSet) {
        StringBuilder pool = new StringBuilder();
        for (int i = 0; i < useSet.length; i++) {
            if (useSet[i]) pool.append(CHAR_SETS[i]);
        }
        return pool.toString();
    }
    
    // Approach 2: Stream concatenation (more functional)
    private static String buildCharacterPool(boolean[] useSet) {
        return IntStream.range(0, useSet.length)
            .filter(i -> useSet[i])
            .mapToObj(i -> new String(CHAR_SETS[i]))
            .collect(Collectors.joining());
    }
    
    // Approach 3: Using Set for unique characters
    private static String buildCharacterPool(boolean[] useSet) {
        Set<Character> uniqueChars = new LinkedHashSet<>();
        for (int i = 0; i < useSet.length; i++) {
            if (useSet[i]) {
                for (char c : CHAR_SETS[i]) {
                    uniqueChars.add(c);
                }
            }
        }
        return uniqueChars.stream()
            .map(String::valueOf)
            .collect(Collectors.joining());
    }
    ```

### Mini-Step 2.2: Add User Input
1. Create methods to get user preferences
2. Handle invalid input gracefully
3. Store user choices for use in generation

!!! tip "Input Validation"
    This builds on the validation from Level 1:
    - We validated character types in Level 1
    - Now we'll validate user input before generation
    - We'll add error handling for invalid inputs

??? question "Need help with user input?"
    Technical Hints:
    ```java
    // Approach 1: Simple boolean flags
    class PasswordPreferences {
        int length;
        boolean includeLowercase;
        boolean includeUppercase;
        boolean includeNumbers;
        boolean includeSpecial;
    }
    
    // Approach 2: Using EnumSet for character types
    enum CharacterType { LOWER, UPPER, NUMBERS, SPECIAL }
    
    class PasswordPreferences {
        int length;
        EnumSet<CharacterType> includedTypes;
        
        public PasswordPreferences() {
            includedTypes = EnumSet.noneOf(CharacterType.class);
        }
    }
    
    // Approach 3: Builder pattern
    class PasswordPreferences {
        private final int length;
        private final Set<CharacterType> types;
        
        private PasswordPreferences(Builder builder) {
            this.length = builder.length;
            this.types = EnumSet.copyOf(builder.types);
        }
        
        public static class Builder {
            private int length = 8;  // default
            private EnumSet<CharacterType> types = EnumSet.noneOf(CharacterType.class);
            
            public Builder length(int length) {
                this.length = length;
                return this;
            }
            
            public Builder includeType(CharacterType type) {
                types.add(type);
                return this;
            }
            
            public PasswordPreferences build() {
                if (length < 8) throw new IllegalArgumentException("Length too short");
                if (types.isEmpty()) types.add(CharacterType.LOWER);  // default
                return new PasswordPreferences(this);
            }
        }
    }
    
    // Different ways to handle user input:
    // Approach 1: Direct console input
    private static boolean getYesNo(Scanner scanner, String prompt) {
        System.out.print(prompt + " (y/n): ");
        return scanner.nextLine().trim().toLowerCase().startsWith("y");
    }
    
    // Approach 2: Menu-based selection
    private static Set<CharacterType> getCharacterTypes(Scanner scanner) {
        Set<CharacterType> types = EnumSet.noneOf(CharacterType.class);
        System.out.println("Select character types (enter numbers, empty to finish):");
        System.out.println("1. Lowercase");
        System.out.println("2. Uppercase");
        System.out.println("3. Numbers");
        System.out.println("4. Special");
        
        while (true) {
            String input = scanner.nextLine().trim();
            if (input.isEmpty()) break;
            try {
                int choice = Integer.parseInt(input);
                switch (choice) {
                    case 1: types.add(CharacterType.LOWER); break;
                    case 2: types.add(CharacterType.UPPER); break;
                    case 3: types.add(CharacterType.NUMBERS); break;
                    case 4: types.add(CharacterType.SPECIAL); break;
                }
            } catch (NumberFormatException e) {
                System.out.println("Please enter a number");
            }
        }
        return types;
    }
    
    // Approach 3: Command-line arguments
    private static PasswordPreferences parseArgs(String[] args) {
        PasswordPreferences.Builder builder = new PasswordPreferences.Builder();
        for (int i = 0; i < args.length; i++) {
            switch (args[i].toLowerCase()) {
                case "-l": builder.length(Integer.parseInt(args[++i])); break;
                case "-u": builder.includeType(CharacterType.UPPER); break;
                case "-n": builder.includeType(CharacterType.NUMBERS); break;
                case "-s": builder.includeType(CharacterType.SPECIAL); break;
            }
        }
        return builder.build();
    }
    ```

### Mini-Step 2.3: Implement Dynamic Character Pool
1. Create a method to build character pool based on preferences
2. Ensure at least one type is selected
3. Handle the case when no types are selected

??? question "Need help combining character sets?"
    Think about:
    - How can you combine strings efficiently?
    - What happens if no character types are selected?
    - How will you verify the final pool is valid?
    
    Hint: Use StringBuilder to combine sets:
    - Add each selected character set
    - Check the final length
    - Have a default fallback

### Mini-Step 2.4: Update Password Generation
1. Modify generator to use custom length
2. Use the dynamic character pool
3. Add validation for new requirements

??? question "Need help with the new generation logic?"
    Think about:
    - How does the length parameter affect your loop?
    - How do you ensure the password is valid?
    - What new validation is needed?
    
    Hint: Consider:
    - Validating length before generation
    - Using the combined character pool
    - Checking for required character types

!!! example "Starting Code"
    ```java
    import java.util.Random;
    import java.util.Scanner;

    public class PasswordGenerator {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            // Your code here
        }

        public static String generatePassword(int length, boolean includeLower, 
                                           boolean includeUpper, boolean includeNumbers, 
                                           boolean includeSpecial) {
            // Your code here
        }
    }
    ```

??? success "Complete Level 2 Solution"
    ```java
    import java.util.Random;
    import java.util.Scanner;

    public class PasswordGenerator {
        private static final Random random = new Random();
        private static final String LOWERCASE = "abcdefghijklmnopqrstuvwxyz";
        private static final String UPPERCASE = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        private static final String NUMBERS = "0123456789";
        private static final String SPECIAL = "!@#$%^&*";

        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            PasswordPreferences prefs = getPreferences(scanner);
            
            if (prefs != null) {
                String password = generatePassword(prefs);
                System.out.println("Your generated password is: " + password);
            }
        }

        static class PasswordPreferences {
            int length;
            boolean includeLowercase;
            boolean includeUppercase;
            boolean includeNumbers;
            boolean includeSpecial;

            boolean isValid() {
                return length >= 8 && 
                       (includeLowercase || includeUppercase || 
                        includeNumbers || includeSpecial);
            }
        }

        private static PasswordPreferences getPreferences(Scanner scanner) {
            PasswordPreferences prefs = new PasswordPreferences();
            
            try {
                System.out.print("Enter password length (minimum 8): ");
                prefs.length = Integer.parseInt(scanner.nextLine().trim());
                
                System.out.print("Include lowercase letters? (y/n): ");
                prefs.includeLowercase = scanner.nextLine().trim().equalsIgnoreCase("y");
                
                System.out.print("Include uppercase letters? (y/n): ");
                prefs.includeUppercase = scanner.nextLine().trim().equalsIgnoreCase("y");
                
                System.out.print("Include numbers? (y/n): ");
                prefs.includeNumbers = scanner.nextLine().trim().equalsIgnoreCase("y");
                
                System.out.print("Include special characters? (y/n): ");
                prefs.includeSpecial = scanner.nextLine().trim().equalsIgnoreCase("y");
                
                if (!prefs.isValid()) {
                    System.out.println("Error: Invalid preferences. Ensure:");
                    System.out.println("- Length is at least 8");
                    System.out.println("- At least one character type is selected");
                    return null;
                }
                
                return prefs;
            } catch (NumberFormatException e) {
                System.out.println("Error: Please enter a valid number for length");
                return null;
            }
        }

        private static String buildCharacterPool(PasswordPreferences prefs) {
            StringBuilder pool = new StringBuilder();
            
            if (prefs.includeLowercase) pool.append(LOWERCASE);
            if (prefs.includeUppercase) pool.append(UPPERCASE);
            if (prefs.includeNumbers) pool.append(NUMBERS);
            if (prefs.includeSpecial) pool.append(SPECIAL);
            
            return pool.toString();
        }

        public static String generatePassword(PasswordPreferences prefs) {
            String characterPool = buildCharacterPool(prefs);
            StringBuilder password = new StringBuilder();
            
            for (int i = 0; i < prefs.length; i++) {
                int index = random.nextInt(characterPool.length());
                password.append(characterPool.charAt(index));
            }
            
            return password.toString();
        }
    }
    ```

## Level 3: Advanced Features

Now that you have a basic password generator working, let's add more advanced features to make it more useful and secure.

### Mini-Step 3.1: Strength Checking

??? question "Need help with strength checking?"
    Think about:
    - What makes a password strong?
    - How can you score different aspects?
    - How will you combine scores?
    
    Technical Hints:
    ```java
    // Approach 1: Simple scoring system
    private static int calculateStrength(String password) {
        int score = 0;
        score += Math.min(3, password.length() / 8);  // Length: 0-3 points
        score += getCharacterVarietyScore(password);  // Variety: 0-4 points
        score -= getWeaknessScore(password);         // Penalties: 0-2 points
        return Math.max(1, Math.min(5, score));
    }
    
    private static int getCharacterVarietyScore(String password) {
        int score = 0;
        if (password.matches(".*[a-z].*")) score++;  // Lowercase
        if (password.matches(".*[A-Z].*")) score++;  // Uppercase
        if (password.matches(".*\\d.*")) score++;    // Numbers
        if (password.matches(".*[^a-zA-Z0-9].*")) score++;  // Special
        return score;
    }
    
    private static int getWeaknessScore(String password) {
        int penalties = 0;
        // Check for repeating characters
        if (password.matches(".*(.)\\1{2,}.*")) penalties++;
        // Check for common patterns
        if (password.toLowerCase().matches(".*(password|123|abc).*")) penalties++;
        return penalties;
    }
    ```

### Mini-Step 3.2: Pattern Detection

??? question "Need help with pattern detection?"
    Think about:
    - What patterns make passwords weak?
    - How can you detect sequences?
    - How to handle case sensitivity?
    
    Technical Hints:
    ```java
    private static boolean hasWeakPattern(String password) {
        // Convert to lowercase once for case-insensitive checks
        String lower = password.toLowerCase();
        
        // Check for sequences
        for (int i = 0; i < lower.length() - 2; i++) {
            char c1 = lower.charAt(i);
            char c2 = lower.charAt(i + 1);
            char c3 = lower.charAt(i + 2);
            
            // Sequential letters (abc, def, etc.)
            if (Character.isLetter(c1) && 
                c2 == c1 + 1 && 
                c3 == c2 + 1) {
                return true;
            }
            
            // Sequential numbers (123, 456, etc.)
            if (Character.isDigit(c1) && 
                c2 == c1 + 1 && 
                c3 == c2 + 1) {
                return true;
            }
            
            // Repeated characters (aaa, 111, etc.)
            if (c1 == c2 && c2 == c3) {
                return true;
            }
        }
        
        // Check for common patterns
        String[] patterns = {
            "password", "admin", "123456", "qwerty",
            "letmein", "welcome"
        };
        
        for (String pattern : patterns) {
            if (lower.contains(pattern)) return true;
        }
        
        return false;
    }
    ```

### Mini-Step 3.3: Multiple Password Generation

??? question "Need help with generating multiple passwords?"
    Think about:
    - How will you store multiple passwords?
    - How can you ensure variety?
    - How will you present choices?
    
    Technical Hints:
    ```java
    public static List<String> generateMultiplePasswords(int count, int length) {
        List<String> passwords = new ArrayList<>();
        Set<String> used = new HashSet<>();  // Avoid duplicates
        
        while (passwords.size() < count) {
            String password = generatePassword(length);
            if (!hasWeakPattern(password) && !used.contains(password)) {
                passwords.add(password);
                used.add(password);
            }
        }
        
        // Sort by strength
        passwords.sort((p1, p2) -> 
            calculateStrength(p2) - calculateStrength(p1));
        
        return passwords;
    }
    
    public static void presentPasswords(List<String> passwords) {
        System.out.println("\nGenerated Passwords:");
        for (int i = 0; i < passwords.size(); i++) {
            String password = passwords.get(i);
            int strength = calculateStrength(password);
            System.out.printf("%d. %s (Strength: %d/5)%n", 
                i + 1, password, strength);
        }
    }
    ```

### Mini-Step 3.4: Password Storage

??? question "Need help with password storage?"
    Think about:
    - What information should you store?
    - How will you format the data?
    - How will you handle errors?
    
    Technical Hints:
    ```java
    public static void savePassword(String password) {
        try {
            // Create directory if it doesn't exist
            Files.createDirectories(Paths.get("passwords"));
            
            // Prepare the data
            String timestamp = LocalDateTime.now()
                .format(DateTimeFormatter.ISO_LOCAL_DATE_TIME);
            int strength = calculateStrength(password);
            String data = String.format("%s,%s,Strength:%d%n",
                timestamp, password, strength);
            
            // Save to file (append mode)
            Files.write(
                Paths.get("passwords/passwords.txt"),
                data.getBytes(),
                StandardOpenOption.CREATE,
                StandardOpenOption.APPEND
            );
            
        } catch (IOException e) {
            System.err.println("Error saving password: " + e.getMessage());
        }
    }
    
    public static List<String> loadPasswords() {
        List<String> passwords = new ArrayList<>();
        Path file = Paths.get("passwords/passwords.txt");
        
        if (Files.exists(file)) {
            try {
                List<String> lines = Files.readAllLines(file);
                for (String line : lines) {
                    String[] parts = line.split(",");
                    if (parts.length >= 2) {
                        passwords.add(parts[1]);  // Password is second field
                    }
                }
            } catch (IOException e) {
                System.err.println("Error loading passwords: " + e.getMessage());
            }
        }
        
        return passwords;
    }
    ```

### Complete Level 3 Solution

??? success "Complete Level 3 Solution"
    ```java
    import java.io.IOException;
    import java.nio.file.*;
    import java.time.LocalDateTime;
    import java.time.format.DateTimeFormatter;
    import java.util.*;
    
    public class PasswordGenerator {
        private static final Random random = new Random();
        private static final String LOWERCASE = "abcdefghijklmnopqrstuvwxyz";
        private static final String UPPERCASE = LOWERCASE.toUpperCase();
        private static final String NUMBERS = "0123456789";
        private static final String SPECIAL = "!@#$%^&*";
        
        // Previous methods from Level 1 and 2 remain the same...
        
        public static int calculateStrength(String password) {
            int score = 0;
            
            // Length score (0-3 points)
            score += Math.min(3, password.length() / 8);
            
            // Character variety (0-4 points)
            if (password.matches(".*[a-z].*")) score++;
            if (password.matches(".*[A-Z].*")) score++;
            if (password.matches(".*\\d.*")) score++;
            if (password.matches(".*[^a-zA-Z0-9].*")) score++;
            
            // Pattern penalty (0-2 points)
            if (hasWeakPattern(password)) score -= 2;
            
            return Math.max(1, Math.min(5, score));
        }
        
        public static boolean hasWeakPattern(String password) {
            String lower = password.toLowerCase();
            
            // Check for sequences
            for (int i = 0; i < lower.length() - 2; i++) {
                char c1 = lower.charAt(i);
                char c2 = lower.charAt(i + 1);
                char c3 = lower.charAt(i + 2);
                
                if ((Character.isLetter(c1) && c2 == c1 + 1 && c3 == c2 + 1) ||
                    (Character.isDigit(c1) && c2 == c1 + 1 && c3 == c2 + 1) ||
                    (c1 == c2 && c2 == c3)) {
                    return true;
                }
            }
            
            // Check for common patterns
            String[] patterns = {"password", "admin", "123456", "qwerty",
                "letmein", "welcome"
            };
            
            for (String pattern : patterns) {
                if (lower.contains(pattern)) return true;
            }
            
            return false;
        }
        
        public static List<String> generateMultiplePasswords(
                int count, int length, boolean includeLower,
                boolean includeUpper, boolean includeNumbers,
                boolean includeSpecial) {
            
            List<String> passwords = new ArrayList<>();
            Set<String> used = new HashSet<>();
            
            while (passwords.size() < count) {
                String password = generatePassword(length, includeLower,
                    includeUpper, includeNumbers, includeSpecial);
                    
                if (!hasWeakPattern(password) && !used.contains(password)) {
                    passwords.add(password);
                    used.add(password);
                }
            }
            
            passwords.sort((p1, p2) -> calculateStrength(p2) - calculateStrength(p1));
            return passwords;
        }
        
        public static void savePassword(String password) {
            try {
                Files.createDirectories(Paths.get("passwords"));
                
                String data = String.format("%s,%s,Strength:%d%n",
                    LocalDateTime.now().format(DateTimeFormatter.ISO_LOCAL_DATE_TIME),
                    password,
                    calculateStrength(password));
                
                Files.write(
                    Paths.get("passwords/passwords.txt"),
                    data.getBytes(),
                    StandardOpenOption.CREATE,
                    StandardOpenOption.APPEND
                );
                
            } catch (IOException e) {
                System.err.println("Error saving password: " + e.getMessage());
            }
        }
        
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            
            // Get user preferences
            System.out.print("Password length (min 8): ");
            int length = Integer.parseInt(scanner.nextLine());
            
            System.out.print("Include lowercase? (y/n): ");
            boolean includeLower = scanner.nextLine().trim().toLowerCase().startsWith("y");
            
            System.out.print("Include uppercase? (y/n): ");
            boolean includeUpper = scanner.nextLine().trim().toLowerCase().startsWith("y");
            
            System.out.print("Include numbers? (y/n): ");
            boolean includeNumbers = scanner.nextLine().trim().toLowerCase().startsWith("y");
            
            System.out.print("Include special characters? (y/n): ");
            boolean includeSpecial = scanner.nextLine().trim().toLowerCase().startsWith("y");
            
            System.out.print("How many passwords? ");
            int count = Integer.parseInt(scanner.nextLine());
            
            // Generate and display passwords
            List<String> passwords = generateMultiplePasswords(
                count, length, includeLower, includeUpper, 
                includeNumbers, includeSpecial
            );
            
            System.out.println("\nGenerated Passwords:");
            for (int i = 0; i < passwords.size(); i++) {
                String password = passwords.get(i);
                System.out.printf("%d. %s (Strength: %d/5)%n",
                    i + 1, password, calculateStrength(password));
            }
            
            // Save selected password
            System.out.print("\nSelect a password to save (1-" + count + "): ");
            int choice = Integer.parseInt(scanner.nextLine()) - 1;
            
            if (choice >= 0 && choice < passwords.size()) {
                savePassword(passwords.get(choice));
                System.out.println("Password saved!");
            }
        }
    }
    ```

### Moving to Level 4

Now that you have a working password generator with multiple features, you might notice some limitations of the current design:

1. All methods are static, making it hard to:
   - Test individual components
   - Change behavior without modifying code
   - Reuse code in different contexts

2. The code has multiple responsibilities mixed together:
   - Password generation
   - Strength calculation
   - Pattern detection
   - File operations
   - User interface

3. Configuration is scattered throughout the code:
   - Character sets are hardcoded
   - File paths are hardcoded
   - Validation rules are embedded in methods

In Level 4, we'll learn how to solve these problems using object-oriented design principles.

## Level 4: Object-Oriented Password Generator

In this level, we'll transform our procedural code into a well-structured OOP solution. Each mini-step will focus on a specific OOP concept and design pattern.

### Mini-Step 4.1: Password Class Design

Your task is to create a proper Password class that encapsulates password data and behavior. This is your first step into OOP!

What you'll learn:
- Encapsulation principles
- Immutable object design
- Builder pattern basics
- Private vs public members

What to change:
1. Move password-related code into a dedicated class
2. Make the password value immutable
3. Add proper validation in the constructor
4. Implement the Builder pattern for flexible creation

Helpful search terms:
- "Java immutable class example"
- "Builder pattern in Java"
- "Java encapsulation best practices"
- "Java class design principles"
- "Java constructor validation"

??? question "Need help with the Password class?"
    Technical Hints:
    ```java
    // Approach 1: Basic immutable Password class
    public class Password {
        private final String value;
        private final int strength;
        private final LocalDateTime generatedAt;
        
        public Password(String value) {
            this.value = value;
            this.strength = calculateStrength();
            this.generatedAt = LocalDateTime.now();
        }
        
        // Getters only - no setters for immutability
        public String getValue() { return value; }
        public int getStrength() { return strength; }
        public LocalDateTime getGeneratedAt() { return generatedAt; }
        
        @Override
        public String toString() {
            return String.format("%s (Strength: %d/5)", value, strength);
        }
    }
    
    // Approach 2: Builder pattern for Password
    public class Password {
        private final String value;
        private final int strength;
        private final LocalDateTime generatedAt;
        private final Set<CharacterType> usedTypes;
        
        private Password(Builder builder) {
            this.value = builder.value;
            this.strength = builder.strength;
            this.generatedAt = LocalDateTime.now();
            this.usedTypes = EnumSet.copyOf(builder.usedTypes);
        }
        
        public static class Builder {
            private String value;
            private int strength;
            private Set<CharacterType> usedTypes = EnumSet.noneOf(CharacterType.class);
            
            public Builder value(String value) {
                this.value = value;
                return this;
            }
            
            public Builder strength(int strength) {
                this.strength = strength;
                return this;
            }
            
            public Builder addType(CharacterType type) {
                usedTypes.add(type);
                return this;
            }
            
            public Password build() {
                if (value == null || value.isEmpty()) {
                    throw new IllegalStateException("Password value is required");
                }
                return new Password(this);
            }
        }
    }
    ```

### Mini-Step 4.2: Character Set Abstraction

Your task is to improve how we handle character sets by creating proper abstractions. This will make the code more flexible and easier to extend.

What you'll learn:
- Interface design
- Enum usage
- Strategy pattern
- Code to interface principle

What to change:
1. Create interfaces for character set behavior
2. Move character sets from static strings to proper classes
3. Implement different character set strategies
4. Use enums for type safety

Helpful search terms:
- "Java interface vs abstract class"
- "Strategy pattern Java example"
- "Java enum best practices"
- "SOLID principles Java"
- "Java type safety examples"

??? question "Need help with character set abstraction?"
    Technical Hints:
    ```java
    // Approach 1: Enum-based character sets
    public enum CharacterType {
        LOWERCASE("abcdefghijklmnopqrstuvwxyz"),
        UPPERCASE("ABCDEFGHIJKLMNOPQRSTUVWXYZ"),
        NUMBERS("0123456789"),
        SPECIAL("!@#$%^&*");
        
        private final String characters;
        
        CharacterType(String characters) {
            this.characters = characters;
        }
        
        public String getCharacters() { return characters; }
    }
    
    // Approach 2: Strategy pattern for character sets
    public interface CharacterSet {
        String getCharacters();
        boolean contains(char c);
        char getRandomCharacter(Random random);
    }
    
    public class LowercaseCharacterSet implements CharacterSet {
        private static final String CHARS = "abcdefghijklmnopqrstuvwxyz";
        
        @Override
        public String getCharacters() { return CHARS; }
        
        @Override
        public boolean contains(char c) {
            return Character.isLowerCase(c);
        }
        
        @Override
        public char getRandomCharacter(Random random) {
            return CHARS.charAt(random.nextInt(CHARS.length()));
        }
    }
    ```

### Mini-Step 4.3: Password Generator Strategy

Your task is to separate the password generation logic into its own component using the Strategy pattern. This will allow for different generation algorithms.

What you'll learn:
- Strategy pattern implementation
- Dependency injection
- Interface segregation
- Single responsibility principle

What to change:
1. Create a PasswordGeneratorStrategy interface
2. Move generation logic into separate classes
3. Implement different generation strategies
4. Use dependency injection for flexibility

Helpful search terms:
- "Strategy pattern real world example"
- "Dependency injection Java"
- "SOLID principles explained"
- "Java interface segregation"
- "Clean code Java examples"

??? question "Need help with generator strategy?"
    Technical Hints:
    ```java
    // Approach 1: Simple strategy interface
    public interface PasswordGeneratorStrategy {
        String generatePassword(int length, Set<CharacterType> types);
    }
    
    public class RandomPasswordGenerator implements PasswordGeneratorStrategy {
        private final Random random;
        
        public RandomPasswordGenerator(Random random) {
            this.random = random;
        }
        
        @Override
        public String generatePassword(int length, Set<CharacterType> types) {
            StringBuilder pool = new StringBuilder();
            for (CharacterType type : types) {
                pool.append(type.getCharacters());
            }
            
            StringBuilder password = new StringBuilder(length);
            for (int i = 0; i < length; i++) {
                int index = random.nextInt(pool.length());
                password.append(pool.charAt(index));
            }
            return password.toString();
        }
    }
    
    // Approach 2: Advanced strategy with requirements
    public interface PasswordRequirement {
        boolean isSatisfied(String password);
        void enforce(StringBuilder password, Random random);
    }
    
    public class CharacterTypeRequirement implements PasswordRequirement {
        private final CharacterType type;
        
        public CharacterTypeRequirement(CharacterType type) {
            this.type = type;
        }
        
        @Override
        public boolean isSatisfied(String password) {
            return password.chars().anyMatch(c -> 
                type.getCharacters().indexOf(c) >= 0);
        }
        
        @Override
        public void enforce(StringBuilder password, Random random) {
            String chars = type.getCharacters();
            int pos = random.nextInt(password.length());
            password.setCharAt(pos, 
                chars.charAt(random.nextInt(chars.length())));
        }
    }
    ```

### Mini-Step 4.4: Password Validation and Strength

Your task is to create a flexible validation system using the Composite pattern and implement a modular strength calculation approach.

What you'll learn:
- Composite pattern
- Chain of responsibility
- Open/closed principle
- Separation of concerns

What to change:
1. Create separate validator classes
2. Implement composite validator
3. Make strength rules pluggable
4. Use chain of responsibility for validation

Helpful search terms:
- "Composite pattern Java"
- "Chain of responsibility example"
- "Java validation framework"
- "Open closed principle Java"
- "Design patterns validation"

??? question "Need help with validation and strength?"
    Technical Hints:
    ```java
    // Approach 1: Composite validator
    public interface PasswordValidator {
        boolean isValid(String password);
        String getErrorMessage();
    }
    
    public class CompositeValidator implements PasswordValidator {
        private final List<PasswordValidator> validators;
        private String lastError;
        
        public CompositeValidator(List<PasswordValidator> validators) {
            this.validators = validators;
        }
        
        @Override
        public boolean isValid(String password) {
            for (PasswordValidator validator : validators) {
                if (!validator.isValid(password)) {
                    lastError = validator.getErrorMessage();
                    return false;
                }
            }
            return true;
        }
        
        @Override
        public String getErrorMessage() {
            return lastError;
        }
    }
    
    // Approach 2: Strength calculator with strategy
    public interface StrengthCalculator {
        int calculateStrength(String password);
    }
    
    public class DefaultStrengthCalculator implements StrengthCalculator {
        private final List<StrengthRule> rules;
        
        public DefaultStrengthCalculator(List<StrengthRule> rules) {
            this.rules = rules;
        }
        
        @Override
        public int calculateStrength(String password) {
            return rules.stream()
                .mapToInt(rule -> rule.evaluateStrength(password))
                .sum();
        }
    }
    
    public interface StrengthRule {
        int evaluateStrength(String password);
    }
    ```

### Mini-Step 4.5: Password Storage

Your task is to implement a proper storage system using the Repository pattern and handle persistence concerns separately from business logic.

What you'll learn:
- Repository pattern
- Data access object (DAO)
- Separation of concerns
- Error handling best practices

What to change:
1. Create a PasswordRepository interface
2. Implement different storage strategies
3. Add proper error handling
4. Separate storage concerns

Helpful search terms:
- "Repository pattern Java"
- "DAO vs Repository pattern"
- "Java persistence patterns"
- "Error handling best practices"
- "Java file operations patterns"

??? question "Need help with password storage?"
    Technical Hints:
    ```java
    // Approach 1: Repository pattern
    public interface PasswordRepository {
        void save(Password password);
        List<Password> loadAll();
        Optional<Password> findByValue(String value);
    }
    
    public class FilePasswordRepository implements PasswordRepository {
        private final Path filePath;
        private final ObjectMapper mapper;
        
        public FilePasswordRepository(Path filePath) {
            this.filePath = filePath;
            this.mapper = new ObjectMapper()
                .registerModule(new JavaTimeModule());
        }
        
        @Override
        public void save(Password password) {
            try {
                Files.createDirectories(filePath.getParent());
                List<Password> passwords = loadAll();
                passwords.add(password);
                mapper.writeValue(filePath.toFile(), passwords);
            } catch (IOException e) {
                throw new PasswordStorageException("Failed to save password", e);
            }
        }
    }
    
    // Approach 2: Event-driven storage
    public interface PasswordEvent {
        Password getPassword();
        LocalDateTime getTimestamp();
    }
    
    public class PasswordStorage {
        private final List<PasswordEventListener> listeners = new ArrayList<>();
        
        public void addListener(PasswordEventListener listener) {
            listeners.add(listener);
        }
        
        public void savePassword(Password password) {
            PasswordEvent event = new PasswordSavedEvent(password);
            for (PasswordEventListener listener : listeners) {
                listener.onPasswordEvent(event);
            }
        }
    }
    ```

### Mini-Step 4.6: Putting It All Together

Your task is to create the main application class that coordinates all the components using dependency injection and proper configuration.

What you'll learn:
- Application architecture
- Dependency injection
- Configuration management
- Component coordination

What to change:
1. Create the main application class
2. Implement dependency injection
3. Add configuration handling
4. Connect all components

Helpful search terms:
- "Java application architecture"
- "Dependency injection container"
- "Java configuration patterns"
- "Clean architecture Java"
- "SOLID principles example"

??? question "Need help with the main application?"
    ```java
    public class PasswordGeneratorApp {
        private final PasswordGeneratorStrategy generator;
        private final PasswordValidator validator;
        private final StrengthCalculator calculator;
        private final PasswordRepository repository;
        private final PasswordConfig config;
        
        // Constructor with dependency injection
        public PasswordGeneratorApp(
                PasswordGeneratorStrategy generator,
                PasswordValidator validator,
                StrengthCalculator calculator,
                PasswordRepository repository,
                PasswordConfig config) {
            this.generator = generator;
            this.validator = validator;
            this.calculator = calculator;
            this.repository = repository;
            this.config = config;
        }
        
        // Main generation method
        public Password generatePassword() {
            String value;
            do {
                value = generator.generatePassword(
                    config.getLength(),
                    config.getCharacterTypes()
                );
            } while (!validator.isValid(value));
            
            return new Password.Builder()
                .value(value)
                .strength(calculator.calculateStrength(value))
                .build();
        }
        
        // Generate multiple passwords
        public List<Password> generateMultiple(int count) {
            return IntStream.range(0, count)
                .mapToObj(i -> generatePassword())
                .sorted(Comparator.comparing(Password::getStrength).reversed())
                .collect(Collectors.toList());
        }
        
        // Save password
        public void savePassword(Password password) {
            repository.save(password);
        }
        
        // Example configuration
        public static void main(String[] args) {
            // Create components
            PasswordGeneratorStrategy generator = new SecureRandomGenerator();
            
            PasswordValidator validator = new CompositeValidator(Arrays.asList(
                new LengthValidator(8),
                new CharacterTypeValidator(),
                new PatternValidator()
            ));
            
            StrengthCalculator calculator = new DefaultStrengthCalculator(
                Arrays.asList(
                    new LengthRule(),
                    new CharacterVarietyRule(),
                    new PatternRule()
                )
            );
            
            PasswordRepository repository = new FilePasswordRepository(
                Paths.get("passwords.json")
            );
            
            PasswordConfig config = new PasswordConfig.Builder()
                .length(12)
                .addCharacterType(CharacterType.LOWERCASE)
                .addCharacterType(CharacterType.UPPERCASE)
                .addCharacterType(CharacterType.NUMBERS)
                .addCharacterType(CharacterType.SPECIAL)
                .build();
            
            // Create application
            PasswordGeneratorApp app = new PasswordGeneratorApp(
                generator, validator, calculator, repository, config
            );
            
            // Use the application
            Password password = app.generatePassword();
            System.out.println("Generated: " + password);
            
            app.savePassword(password);
            System.out.println("Password saved!");
        }
    }
    ```

### Complete Level 4 Solution

??? success "Complete OOP Solution"
    ```java
    // Character set abstraction
    public enum CharacterType {
        LOWERCASE("abcdefghijklmnopqrstuvwxyz"),
        UPPERCASE("ABCDEFGHIJKLMNOPQRSTUVWXYZ"),
        NUMBERS("0123456789"),
        SPECIAL("!@#$%^&*");
        
        private final String characters;
        
        CharacterType(String characters) {
            this.characters = characters;
        }
        
        public String getCharacters() { return characters; }
    }
    
    // Password class with builder
    public class Password {
        private final String value;
        private final int strength;
        private final LocalDateTime generatedAt;
        private final Set<CharacterType> usedTypes;
        
        private Password(Builder builder) {
            this.value = builder.value;
            this.strength = builder.strength;
            this.generatedAt = LocalDateTime.now();
            this.usedTypes = EnumSet.copyOf(builder.usedTypes);
        }
        
        // Getters
        public String getValue() { return value; }
        public int getStrength() { return strength; }
        public LocalDateTime getGeneratedAt() { return generatedAt; }
        public Set<CharacterType> getUsedTypes() { return EnumSet.copyOf(usedTypes); }
        
        @Override
        public String toString() {
            return String.format("%s (Strength: %d/5)", value, strength);
        }
        
        public static class Builder {
            private String value;
            private int strength;
            private Set<CharacterType> usedTypes = EnumSet.noneOf(CharacterType.class);
            
            public Builder value(String value) {
                this.value = value;
                return this;
            }
            
            public Builder strength(int strength) {
                this.strength = strength;
                return this;
            }
            
            public Builder addType(CharacterType type) {
                usedTypes.add(type);
                return this;
            }
            
            public Password build() {
                if (value == null || value.isEmpty()) {
                    throw new IllegalStateException("Password value is required");
                }
                return new Password(this);
            }
        }
    }
    
    // Generator strategy
    public interface PasswordGeneratorStrategy {
        String generatePassword(int length, Set<CharacterType> types);
    }
    
    public class SecureRandomGenerator implements PasswordGeneratorStrategy {
        private final SecureRandom random = new SecureRandom();
        
        @Override
        public String generatePassword(int length, Set<CharacterType> types) {
            if (types.isEmpty()) {
                throw new IllegalArgumentException("At least one character type is required");
            }
            
            // Build character pool
            StringBuilder pool = new StringBuilder();
            for (CharacterType type : types) {
                pool.append(type.getCharacters());
            }
            
            // Generate password
            StringBuilder password = new StringBuilder(length);
            for (int i = 0; i < length; i++) {
                int index = random.nextInt(pool.length());
                password.append(pool.charAt(index));
            }
            
            // Ensure at least one character from each type
            for (CharacterType type : types) {
                if (!containsType(password.toString(), type)) {
                    int pos = random.nextInt(length);
                    String chars = type.getCharacters();
                    password.setCharAt(pos, 
                        chars.charAt(random.nextInt(chars.length())));
                }
            }
            
            return password.toString();
        }
        
        private boolean containsType(String password, CharacterType type) {
            return password.chars().anyMatch(c -> 
                type.getCharacters().indexOf(c) >= 0);
        }
    }
    
    // Validation
    public interface PasswordValidator {
        boolean isValid(String password);
        String getErrorMessage();
    }
    
    public class CompositeValidator implements PasswordValidator {
        private final List<PasswordValidator> validators;
        private String lastError;
        
        public CompositeValidator(List<PasswordValidator> validators) {
            this.validators = validators;
        }
        
        @Override
        public boolean isValid(String password) {
            for (PasswordValidator validator : validators) {
                if (!validator.isValid(password)) {
                    lastError = validator.getErrorMessage();
                    return false;
                }
            }
            return true;
        }
        
        @Override
        public String getErrorMessage() {
            return lastError;
        }
    }
    
    public class LengthValidator implements PasswordValidator {
        private final int minLength;
        
        public LengthValidator(int minLength) {
            this.minLength = minLength;
        }
        
        @Override
        public boolean isValid(String password) {
            return password.length() >= minLength;
        }
        
        @Override
        public String getErrorMessage() {
            return "Password must be at least " + minLength + " characters long";
        }
    }
    
    public class CharacterTypeValidator implements PasswordValidator {
        @Override
        public boolean isValid(String password) {
            return password.matches(".*[a-z].*") &&
                   password.matches(".*[A-Z].*") &&
                   password.matches(".*\\d.*") &&
                   password.matches(".*[^a-zA-Z0-9].*");
        }
        
        @Override
        public String getErrorMessage() {
            return "Password must contain lowercase, uppercase, numbers, and special characters";
        }
    }
    
    public class PatternValidator implements PasswordValidator {
        @Override
        public boolean isValid(String password) {
            String lower = password.toLowerCase();
            
            // Check for sequences
            for (int i = 0; i < lower.length() - 2; i++) {
                char c1 = lower.charAt(i);
                char c2 = lower.charAt(i + 1);
                char c3 = lower.charAt(i + 2);
                
                if ((Character.isLetter(c1) && c2 == c1 + 1 && c3 == c2 + 1) ||
                    (Character.isDigit(c1) && c2 == c1 + 1 && c3 == c2 + 1) ||
                    (c1 == c2 && c2 == c3)) {
                    return false;
                }
            }
            
            // Check for common patterns
            String[] patterns = {"password", "admin", "123456", "qwerty"};
            for (String pattern : patterns) {
                if (lower.contains(pattern)) return false;
            }
            
            return true;
        }
        
        @Override
        public String getErrorMessage() {
            return "Password contains common patterns or sequences";
        }
    }
    
    // Strength calculation
    public interface StrengthCalculator {
        int calculateStrength(String password);
    }
    
    public interface StrengthRule {
        int evaluateStrength(String password);
    }
    
    public class DefaultStrengthCalculator implements StrengthCalculator {
        private final List<StrengthRule> rules;
        
        public DefaultStrengthCalculator(List<StrengthRule> rules) {
            this.rules = rules;
        }
        
        @Override
        public int calculateStrength(String password) {
            int score = rules.stream()
                .mapToInt(rule -> rule.evaluateStrength(password))
                .sum();
            return Math.max(1, Math.min(5, score));
        }
    }
    
    public class LengthRule implements StrengthRule {
        @Override
        public int evaluateStrength(String password) {
            return Math.min(3, password.length() / 8);
        }
    }
    
    public class CharacterVarietyRule implements StrengthRule {
        @Override
        public int evaluateStrength(String password) {
            int score = 0;
            if (password.matches(".*[a-z].*")) score++;
            if (password.matches(".*[A-Z].*")) score++;
            if (password.matches(".*\\d.*")) score++;
            if (password.matches(".*[^a-zA-Z0-9].*")) score++;
            return score;
        }
    }
    
    public class PatternRule implements StrengthRule {
        @Override
        public int evaluateStrength(String password) {
            PatternValidator validator = new PatternValidator();
            return validator.isValid(password) ? 0 : -2;
        }
    }
    
    // Storage
    public interface PasswordRepository {
        void save(Password password);
        List<Password> loadAll();
        Optional<Password> findByValue(String value);
    }
    
    public class FilePasswordRepository implements PasswordRepository {
        private final Path filePath;
        private final ObjectMapper mapper;
        
        public FilePasswordRepository(Path filePath) {
            this.filePath = filePath;
            this.mapper = new ObjectMapper()
                .registerModule(new JavaTimeModule())
                .enable(SerializationFeature.INDENT_OUTPUT);
        }
        
        @Override
        public void save(Password password) {
            try {
                Files.createDirectories(filePath.getParent());
                List<Password> passwords = loadAll();
                passwords.add(password);
                mapper.writeValue(filePath.toFile(), passwords);
            } catch (IOException e) {
                throw new PasswordStorageException("Failed to save password", e);
            }
        }
        
        @Override
        public List<Password> loadAll() {
            if (!Files.exists(filePath)) {
                return new ArrayList<>();
            }
            
            try {
                return mapper.readValue(filePath.toFile(),
                    new TypeReference<List<Password>>() {});
            } catch (IOException e) {
                throw new PasswordStorageException("Failed to load passwords", e);
            }
        }
        
        @Override
        public Optional<Password> findByValue(String value) {
            return loadAll().stream()
                .filter(p -> p.getValue().equals(value))
                .findFirst();
        }
    }
    
    public class PasswordStorageException extends RuntimeException {
        public PasswordStorageException(String message, Throwable cause) {
            super(message, cause);
        }
    }
    
    // Configuration
    public class PasswordConfig {
        private final int length;
        private final Set<CharacterType> characterTypes;
        
        private PasswordConfig(Builder builder) {
            this.length = builder.length;
            this.characterTypes = EnumSet.copyOf(builder.characterTypes);
        }
        
        public int getLength() { return length; }
        public Set<CharacterType> getCharacterTypes() { 
            return EnumSet.copyOf(characterTypes); 
        }
        
        public static class Builder {
            private int length = 12;  // Default length
            private Set<CharacterType> characterTypes = EnumSet.noneOf(CharacterType.class);
            
            public Builder length(int length) {
                if (length < 8) {
                    throw new IllegalArgumentException("Length must be at least 8");
                }
                this.length = length;
                return this;
            }
            
            public Builder addCharacterType(CharacterType type) {
                characterTypes.add(type);
                return this;
            }
            
            public PasswordConfig build() {
                if (characterTypes.isEmpty()) {
                    characterTypes.add(CharacterType.LOWERCASE);  // Default type
                }
                return new PasswordConfig(this);
            }
        }
    }
    
    // Main application class
    public class PasswordGeneratorApp {
        private final PasswordGeneratorStrategy generator;
        private final PasswordValidator validator;
        private final StrengthCalculator calculator;
        private final PasswordRepository repository;
        private final PasswordConfig config;
        
        public PasswordGeneratorApp(
                PasswordGeneratorStrategy generator,
                PasswordValidator validator,
                StrengthCalculator calculator,
                PasswordRepository repository,
                PasswordConfig config) {
            this.generator = generator;
            this.validator = validator;
            this.calculator = calculator;
            this.repository = repository;
            this.config = config;
        }
        
        public Password generatePassword() {
            String value;
            do {
                value = generator.generatePassword(
                    config.getLength(),
                    config.getCharacterTypes()
                );
            } while (!validator.isValid(value));
            
            return new Password.Builder()
                .value(value)
                .strength(calculator.calculateStrength(value))
                .build();
        }
        
        public List<Password> generateMultiple(int count) {
            return IntStream.range(0, count)
                .mapToObj(i -> generatePassword())
                .sorted(Comparator.comparing(Password::getStrength).reversed())
                .collect(Collectors.toList());
        }
        
        public void savePassword(Password password) {
            repository.save(password);
        }
        
        // Example usage
        public static void main(String[] args) {
            // Create components
            PasswordGeneratorStrategy generator = new SecureRandomGenerator();
            
            PasswordValidator validator = new CompositeValidator(Arrays.asList(
                new LengthValidator(8),
                new CharacterTypeValidator(),
                new PatternValidator()
            ));
            
            StrengthCalculator calculator = new DefaultStrengthCalculator(
                Arrays.asList(
                    new LengthRule(),
                    new CharacterVarietyRule(),
                    new PatternRule()
                )
            );
            
            PasswordRepository repository = new FilePasswordRepository(
                Paths.get("passwords.json")
            );
            
            PasswordConfig config = new PasswordConfig.Builder()
                .length(12)
                .addCharacterType(CharacterType.LOWERCASE)
                .addCharacterType(CharacterType.UPPERCASE)
                .addCharacterType(CharacterType.NUMBERS)
                .addCharacterType(CharacterType.SPECIAL)
                .build();
            
            // Create application
            PasswordGeneratorApp app = new PasswordGeneratorApp(
                generator, validator, calculator, repository, config
            );
            
            // Generate and save a password
            Password password = app.generatePassword();
            System.out.println("Generated: " + password);
            
            app.savePassword(password);
            System.out.println("Password saved!");
            
            // Generate multiple passwords
            List<Password> passwords = app.generateMultiple(5);
            System.out.println("\nMultiple passwords:");
            passwords.forEach(System.out::println);
        }
    }
    ```

This complete solution demonstrates:
- Clear separation of concerns with distinct classes and interfaces
- Use of multiple design patterns (Builder, Strategy, Composite, Repository)
- Proper encapsulation and immutability
- Flexible and extensible architecture
- Clean error handling
- Type safety with enums
- Dependency injection
- SOLID principles implementation

Each component is independently testable, and new features can be added by implementing the appropriate interfaces. 