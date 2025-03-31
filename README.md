                            ## Assignment Java Backend Developer

```java

                    Section 1: Theoretical Questions

### 1. Explain the difference between an interface and an abstract class in Java. When would you use one over the other?

## Answer:

Both interfaces and abstract classes in Java are used to achieve abstraction, but they have some key differences.

# Abstract Classes:

- An abstract class can have both abstract methods (methods without a body) and concrete methods (methods with a body).
- It can have instance variables (fields).
- A class can extend only one abstract class (single inheritance).
- It can provide a common base implementation for derived classes.
- It can have constructors.

# Interfaces:

- An interface can only have abstract methods (before Java 8). After Java 8, interfaces can have default and static methods.
- It can only have constant variables.
- A class can implement multiple interfaces (multiple inheritance).
- It specifies a contract that implementing classes must follow.
- It cannot have constructors.

# When to use one over the other:

- Use an abstract class when:

  - when we  need to provide a common base implementation for derived classes.
  - when we need instance variables that derived classes can inherit.
  - There is an "is-a" relationship (e.g., `Dog extends Animal`).

- Use an interface when:
  - when we want to define a contract for unrelated classes (e.g., `Flyable` for `Airplane` and `Bird`).
  - when we need multiple inheritance.
  - There is a "can-do" relationship.

---

### 2. What is the purpose of the `final`, `finally`, and `finalize` keywords in Java? Provide examples.

## Answer:

# `final` keyword:

- Used to restrict modification.
  - Variables: Become constants (value cannot change).
  - Methods: Cannot be overridden.
  - Classes: Cannot be subclassed.

 Example:



class Values {
    final int CONST_VALUE = 30; // final variable
    final void myFinalMethod() { // final method
        System.out.println("Cannot override this.");
    }
}

final class FinalClass { } // Cannot inherit this class

# finally :

Used in try-catch blocks to execute code always (e.g., resource cleanup).

* Example:

try {
    int result = 25 / 0;
} catch (ArithmeticException e) {
    System.out.println("Division by zero!");
} finally {
    System.out.println("This runs no matter what.");
}

# finalize():

A method called by the garbage collector before object destruction. Used for cleanup.

* Example:

class MyClass {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Finalize called.");
        super.finalize();
    }
}

### 3. How does Java handle memory management and garbage collection? What is the role of the JVM in this process?

Answer:

# Memory Management:

  Heap Memory: Stores objects (shared across threads).

  Stack Memory: Stores method calls, local primitives, and references (per-thread).

  Code/Native Memory: JVM internal use.

  Garbage Collection (GC):

* Steps:

  Mark: Identify unreachable objects (no active references).

  Sweep: Remove marked objects.

  Compact: Reorganize memory (optional).

* Types:

  Minor GC: Cleans Young Generation (frequent).

  Major/Full GC: Cleans Old Generation (slower).

* JVM Role:

  Manages memory allocation (heap/stack).

  Runs GC algorithms (e.g., G1, Parallel).

  Triggers GC when memory thresholds are reached.



                                 Section 2: Coding Problems


### 4. Find the First Non-Repeating Character in a String


## Solution Code:


public class FirstUniqueCharacter {
    public static Character findFirstNonRepeatingChar(String str) {
        if (str == null || str.isEmpty()) return null;
        int[] charCount = new int[256]; // ASCII support

        for (char c : str.toCharArray()) charCount[c]++;
        for (char c : str.toCharArray()) {
            if (charCount[c] == 1) return c;
        }
        return null;
    }

    public static void main(String[] args) {
        System.out.println(findFirstNonRepeatingChar("swiss"));
        System.out.println(findFirstNonRepeatingChar("DIGI5"));
    }
}

## Output:

First non-repeating character in swiss: w
First non-repeating character in DIGI5: D


### 5. Reverse Words in a Sentence

## Solution Code:


public class ReverseWords {
    public static String reverseWords(String sentence) {
        if (sentence == null || sentence.isEmpty()) return "";
        char[] arr = sentence.toCharArray();
        reverse(arr, 0, arr.length - 1); // Reverse entire sentence

        int wordStart = 0;
        for (int i = 0; i <= arr.length; i++) {
            if (i == arr.length || arr[i] == ' ') {
                reverse(arr, wordStart, i - 1); // Reverse individual word
                wordStart = i + 1;
            }
        }
        return new String(arr);
    }

    private static void reverse(char[] arr, int start, int end) {
        while (start < end) {
            char temp = arr[start];
            arr[start++] = arr[end];
            arr[end--] = temp;
        }
    }

    public static void main(String[] args) {
        System.out.println(reverseWords("Java is awesome"));
        System.out.println(reverseWords("DIGI5 to Welcome"));
    }
}

Output:

awesome is Java
Welcome to DIGI5
```
