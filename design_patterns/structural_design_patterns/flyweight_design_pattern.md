Flyweight pattern is one of the structural design patterns as this pattern provides ways to decrease object count thus improving application required objects structure. Flyweight pattern is used when we need to create a large number of similar objects (say 105). One important feature of flyweight objects is that they are immutable. This means that they cannot be modified once they have been constructed.

Why do we care for number of objects in our program?

Less number of objects reduces the memory usage, and it manages to keep us away from errors related to memory like java.lang.OutOfMemoryError.

Although creating an object in Java is really fast, we can still reduce the execution time of our program by sharing objects.

In Flyweight pattern we use a HashMap that stores reference to the object which have already been created, every object is associated with a key. Now when a client wants to create an object, he simply has to pass a key associated with it and if the object has already been created we simply get the reference to that object else it creates a new object and then returns it reference to the client.


Intrinsic State:

Definition: The part of an object's state that is shared among many objects. It is constant and stored within the object.

Example: In a text editor, the character code of a letter (like 'A', 'B', etc.) can be an intrinsic state since it doesn’t change regardless of where the letter appears.
Extrinsic State:

Definition: The part of an object's state that varies and is specific to each object instance. It is passed to the object and stored externally.

Example: The position and font style of a character in a text editor are extrinsic states since they can differ for each instance of the character 'A' on the screen.

Intrinsic state is shared to minimize memory usage, while extrinsic state is context-dependent and specific to each instance.

```java 

Flyweight Interface and Concrete Flyweights

import java.util.HashMap;
import java.util.Map;

// Flyweight Interface
interface Player {
    void assignWeapon(String weapon);
    void mission();
}

// Concrete Flyweight: Terrorist
class Terrorist implements Player {
    private final String TASK;
    private String weapon;

    public Terrorist() {
        TASK = "PLANT A BOMB";
    }

    @Override
    public void assignWeapon(String weapon) {
        this.weapon = weapon;
    }

    @Override
    public void mission() {
        System.out.println("Terrorist with weapon " + weapon + " | Task is " + TASK);
    }
}

// Concrete Flyweight: CounterTerrorist
class CounterTerrorist implements Player {
    private final String TASK;
    private String weapon;

    public CounterTerrorist() {
        TASK = "DIFFUSE A BOMB";
    }

    @Override
    public void assignWeapon(String weapon) {
        this.weapon = weapon;
    }

    @Override
    public void mission() {
        System.out.println("CounterTerrorist with weapon " + weapon + " | Task is " + TASK);
    }
}


Flyweight Factory

class PlayerFactory {
    private static Map<String, Player> playerMap = new HashMap<>();

    public static Player getPlayer(String type) {
        Player player = null;

        if (playerMap.containsKey(type)) {
            player = playerMap.get(type);
        } else {
            switch (type) {
                case "Terrorist":
                    System.out.println("Terrorist Created");
                    player = new Terrorist();
                    break;
                case "CounterTerrorist":
                    System.out.println("Counter Terrorist Created");
                    player = new CounterTerrorist();
                    break;
                default:
                    System.out.println("Unreachable code!");
            }
            playerMap.put(type, player);
        }
        return player;
    }
}

Client Code

public class CounterStrike {
    private static String[] playerType = {"Terrorist", "CounterTerrorist"};
    private static String[] weapons = {"AK-47", "M16", "Desert Eagle", "Glock", "Knife"};

    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            Player player = PlayerFactory.getPlayer(getRandomPlayerType());
            player.assignWeapon(getRandomWeapon());
            player.mission();
        }
    }

    public static String getRandomPlayerType() {
        int randIndex = (int) (Math.random() * playerType.length);
        return playerType[randIndex];
    }

    public static String getRandomWeapon() {
        int randIndex = (int) (Math.random() * weapons.length);
        return weapons[randIndex];
    }
}

```

Explanation:

Flyweight Interface (Player): Declares methods that concrete flyweight classes (Terrorist and CounterTerrorist) must implement.

Concrete Flyweights: Implement the Player interface and define the intrinsic state (the task) and extrinsic state (the weapon) which can be assigned at runtime.

Flyweight Factory (PlayerFactory): Manages a pool of flyweight objects and ensures that shared objects are reused. It creates a new object only if one does not already exist.

Client (CounterStrike): Simulates the game by creating players and assigning them weapons. It demonstrates how the Flyweight pattern reduces memory usage by reusing Player objects.

This implementation shows how you can use the Flyweight pattern to optimize memory usage in a game like Counter-Strike by reusing Player objects and only assigning the unique attributes (weapons) at runtime.

