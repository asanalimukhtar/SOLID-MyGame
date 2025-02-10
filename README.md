# 🚀 Applying SOLID Principles to Improve Game Code Structure

In this project, we apply SOLID principles to improve the organization’s structure and code. SOLID is a set of guidelines that helps us write clearer, more flexible, and easier-to-use code. Let’s dive into how we’ve implemented each principle.

## 1️⃣ Single Responsibility Principle (SRP)

This principle states that each class should only do its job. In our code, we follow this principle as shown below:
- **Player Class**: Responsible only for managing the player, including health, experience, and inventory.
- **CombatManager Class**: Handles only combat logic, such as managing damage.
- **Inventory Class**: Manages inventory items.

By adhering to SRP, each class has a single responsibility, ensuring that code doesn’t mix up different concerns.

## 2️⃣ Open/Closed Principle (OCP)

This principle emphasizes that we should be able to add new functionality without changing existing code. Here’s how we apply it:
- **CombatManager** works with any object implementing the `Damageable` interface, allowing us to easily add new enemy types (e.g., vampires, zombies) without modifying the existing logic.

This promotes extensibility without disrupting the original functionality.

## 3️⃣ Dependency Inversion Principle (DIP)

The principle suggests that high-level modules should not depend on low-level ones, but both should depend on abstractions. In our code:
- **CombatManager** does not depend on specific enemies, but rather on the `Damageable` interface. We can swap enemy types without altering **CombatManager**.

This keeps our system flexible and decoupled from specific classes.

## 4️⃣ Liskov Substitution Principle (LSP)

This principle states that we should be able to replace objects of a base class with those of a subclass without altering program behavior. Here’s how we implement this:
- All enemies implement the `Damageable` interface, so we can introduce new enemies (like zombies or vampires) without breaking the combat logic. As long as they implement the interface, everything works!

This ensures consistency and smooth extensibility.

## 5️⃣ Interface Segregation Principle (ISP)

The principle suggests that interfaces should be narrow and not overloaded with unnecessary methods. In our code:
- The `Damageable` interface is designed to handle only damage-related functionality, ensuring simplicity and focus.

This helps avoid classes implementing methods they don’t need and keeps the interfaces lean.

## ✨ Why SOLID Principles Matter?

By adhering to SOLID principles, we make our code not only cleaner but also more efficient:
- Adding new enemies? No need to dig into other classes—just create a new class!
- Want to extend game functionality? Easy, without the risk of breaking existing code.
- Encounter a bug? It’s easier to find and fix, thanks to isolated responsibilities in classes.

By following SOLID, we ensure our code is flexible, scalable, and maintainable, which is essential for long-term project success.

## 🧠 Code Examples

### 1️⃣ Damageable Interface

```java
interface Damageable {
    void takeDamage(int damage);
}

	•	Interface Segregation Principle (ISP): Focused on taking damage—no unrelated methods.
	•	Open/Closed Principle (OCP): Add new classes that implement this interface without altering existing code.

2️⃣ Player Class

public class Player implements Damageable {
    String name;
    int health = 100;
    int experience = 0;
    Inventory inventory;

    public Player(String name) {
        this.name = name;
        this.inventory = new Inventory();
    }

    public void takeDamage(int damage) {
        health -= damage;
        System.out.println(name + " takes damage: " + damage + ", health: " + health);
    }

    public void gainExperience(int exp) {
        experience += exp;
        System.out.println(name + " gains experience: " + exp + ", total experience: " + experience);
    }

    public void pickUpItem(String item) {
        inventory.addItem(item);
    }
}

	•	Single Responsibility Principle (SRP): The Player class focuses only on managing the player’s state.
	•	Liskov Substitution Principle (LSP): We can substitute the Player class with its subclasses (like Mage) without breaking the code.

3️⃣ Enemy Class

public class Enemy implements Damageable {
    String type;
    int health;

    public Enemy(String type, int health) {
        this.type = type;
        this.health = health;
    }

    public void takeDamage(int damage) {
        health -= damage;
        System.out.println(type + " takes damage: " + damage + ", health: " + health);
    }

    public String getType() {
        return type;
    }
}

	•	Single Responsibility Principle (SRP): This class only handles the enemy’s logic (type and health).
	•	Open/Closed Principle (OCP): You can add new enemy types without modifying the Enemy class—just create a subclass!

4️⃣ CombatManager Class

public class CombatManager {
    public static void attack(Damageable target, int damage) {
        target.takeDamage(damage);
    }
}

	•	Dependency Inversion Principle (DIP): CombatManager works with any object that implements Damageable, decoupling it from specific classes.
	•	Open/Closed Principle (OCP): New damageable objects can be added without changing the combat logic.

5️⃣ Inventory Class

import java.util.ArrayList;
import java.util.List;

public class Inventory {
    private List<String> items = new ArrayList<>();

    public void addItem(String item) {
        items.add(item);
        System.out.println("You picked up item: " + item);
    }
}

	•	Single Responsibility Principle (SRP): The class manages only the player’s inventory.

6️⃣ Level and Score Management

class LevelManager {
    int level = 1;

    public void levelUp() {
        level++;
        System.out.println("Level Up! New level: " + level);
    }
}

class ScoreManager {
    int score = 0;

    public void addScore(int points) {
        score += points;
        System.out.println("Your score: " + score);
    }
}

	•	Single Responsibility Principle (SRP): Each class manages only one aspect: level or score.

7️⃣ Main Game Class

import java.util.Scanner;

public class Game {
    public static void main(String[] args) {
        Scanner game = new Scanner(System.in);
        Player player = new Player("Hero");
        Enemy enemy = new Enemy("Goblin", 30);
        EnemyManager enemyManager = new EnemyManager();
        enemyManager.addEnemy(enemy);
        ItemManager itemManager = new ItemManager();
        LevelManager levelManager = new LevelManager();
        ScoreManager scoreManager = new ScoreManager();
        player.pickUpItem("sword");
        itemManager.useItem(player, "sword");
        System.out.print("Player Damage: ");
        int playerDamage = game.nextInt();
        CombatManager.attack(enemy, playerDamage);
        player.gainExperience(10);

        levelManager.levelUp();
        scoreManager.addScore(50);
        System.out.print("Goblin Damage: ");
        int enemyDamage = game.nextInt();
        enemyManager.attackPlayer(player, enemy, enemyDamage);
    }
}

	•	Single Responsibility Principle (SRP): The Game class orchestrates the game, delegating tasks to other classes.

🎉 Conclusion

By applying SOLID principles, we’ve made the game:
	•	Easier to understand
	•	More extensible: Adding new features or enemies doesn’t break existing functionality.
	•	More maintainable: Bugs are easier to fix, thanks to well-structured code.

SOLID principles help us ensure that our code remains clean, modular, and future-proof. Whether you’re working on a large or small project, SOLID makes all the difference!

📂 SOLID-AdventureGame Directory Structure

📂 SOLID-AdventureGame
│── 📂 src
│   ├── 📂 player
│   │   ├── Player.java
│   │   ├── Inventory.java
│   ├── 📂 combat
│   │   ├── CombatManager.java
│   ├── 📂 enemies
│   │   ├── Enemy.java
│   │   ├── Goblin.java
│   │   ├── Zombie.java
│   │   ├── Vampire.java
│   ├── 📂 items
│   │   ├── ItemManager.java
│   │   ├── Sword.java
│   │   ├── Shield.java
│   │   ├── HealthPotion.java
│   ├── 📂 level
│   │   ├── LevelManager.java
│   ├── 📂 score
│   │   ├── ScoreManager.java
│   ├── Game.java
│
│── 📂 docs
│   ├── UML-Before-Refactor.png
│   ├── UML-After-Refactor.png
│   ├── SOLID-Refactoring-Report.pdf
│
│── README.md
