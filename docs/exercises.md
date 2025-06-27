# Fun Programming Exercises 🎮

## Methods (Functions) 🎯

### 1. Marvel Rivals Team Comp Calculator
Create a method that calculates team composition strength:
```java
public static double calculateTeamStrength(int vanguards, int duelists, int strategists) {
    // A balanced team needs at least 1 of each role
    // Vanguards provide tankiness (x1.5 multiplier)
    // Duelists provide damage (x1.3 multiplier)
    // Strategists provide support (x1.2 multiplier)
    // Return a team power score based on composition
}
```

### 2. Ultimate Ability Cooldown Calculator
Write a method that calculates if an ultimate ability is ready:
```java
public static boolean isUltimateReady(int damageDealt, int healingDone, int timeInCombat) {
    // Ultimate charges from:
    // - Every 100 damage adds 5% charge
    // - Every 100 healing adds 3% charge
    // - Every 10 seconds in combat adds 2% charge
    // Return true if charge is >= 100%
}
```

## Loops 🔄

### 1. Among Us Task Simulator
```java
// Create a loop that simulates completing tasks in Among Us
// Start with 10 tasks
// Each iteration completes 1-3 tasks randomly
// If an impostor interrupts (20% chance each iteration), you lose one task progress
// Continue until all tasks are done or you get eliminated
```

### 2. Team Fight Simulator
```java
// Create a loop that simulates a Marvel Rivals team fight
// Track 6 players (3v3)
// Each iteration:
//   - Random player deals damage
//   - Check if any player dies (health <= 0)
//   - Strategists heal allies (20% chance per iteration)
//   - Vanguards block damage for allies (30% chance)
// Continue until one team is eliminated
```

## Data Types & Variables 📊

### 1. Hero Stats Manager
```java
// Create variables to track a Marvel Rivals hero:
// - Current Health (int)
// - Ultimate Charge (double percentage)
// - Hero Role (String: "Vanguard", "Duelist", or "Strategist")
// - Is On Cooldown (boolean)
// - Damage Dealt This Match (long)
// - Team-up Partner Name (String)
```

### 2. Match Statistics System
```java
// Create a program that tracks match stats:
// - Eliminations/Deaths/Assists (K/D/A)
// - Objective Time (in seconds)
// - Damage Dealt/Blocked/Healed
// - Ultimate Abilities Used
// - Win Streak
```

## The "Nice" Number Challenge 😏
```java
// Write a program that:
// 1. Takes a number as input
// 2. If the number is 69, print "Nice"
// 3. If the number is 420, print "Extra Nice"
// 4. If it's both 69 and 420 multiplied together, print "Super Nice"
// 5. For any other number, print "Not Nice"
```

## Boss Battle: The Ultimate Teabagger Counter
```java
// Create a program that:
// 1. Tracks how many times a player has crouched rapidly (teabagged)
// 2. If they crouch more than 5 times in 2 seconds, declare them a "Certified Teabagger"
// 3. Keep a high score of fastest teabags per second
// 4. Award achievements like "Master Teabagger" or "Tea Time Champion"
```

Remember:
- Test your code with different inputs
- Try to break it (that's half the fun!)
- Add your own gaming references
- Keep it silly but functional

Pro Tip: If your code works but looks ugly, remember what Doctor Strange says: "The code is not always what it seems." 