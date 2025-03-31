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

# final keyword:

final keyword is used to restrict modification. It can be applied to variables, methods, and classes.

* final variables become constants (their value can't be changed).
* final methods cannot be overridden by subclasses.
* final classes cannot be subclassed (inherited from).

Example:

class values {
    final int const_value = 30; // final variable
    final void myFinalMethod() { // final method
        System.out.println("This method cannot be overridden.");
    }
}

 final class FinalClass { // final class
    // ...
}

# finally:

* finally keyword is used in try-catch blocks to define a block of code that always executes, regardless of whether an
  exception is thrown or not.
* It's typically used to release resources (like closing files or database connections) that need to be cleaned up.

Example:

try {

    int result = 25 / 0;
    System.out.println(result);
} catch (ArithmeticException e) {
    System.out.println("Division by zero!");
} finally {
    System.out.println("This code always runs."); // Resource cleanup
}




# finalize():

finalize is a method (not a keyword like the others).
It's called by the garbage collector before an object is reclaimed.
It's intended for cleanup operations, like releasing native resources.

Example:

class MyClass {
    @Override
    protected void finalize() throws Throwable {
        // Cleanup code (e.g., closing a file)
        System.out.println("Finalize method called.");
        super.finalize();
    }
}


### 3. How does Java handle memory management and garbage collection? What is the role of the JVM in this process?

Answer:

1. Memory Management in Java

The JVM organizes memory into distinct runtime areas:

* Heap Memory:
-> Stores objects and their instance variables.
-> Shared across all threads.

* Stack Memory:
-> It stores method calls, local primitives, and object references (pointers to heap objects).
-> Each thread has its own stack.

*Code Cache: JIT-compiled native code.

* Native Memory: For JVM internal operations,which is not part of the heap.


2. Garbage Collection

The JVM automatically reclaims memory by removing unreachable objects.

Key steps:

-> Identify Garbage:
* Objects that are no longer referenced by any active thread or static variable are marked as unreachable.
* GC algorithms traverse the object graph starting from GC roots (e.g., static fields, thread stacks).


-> Collect Garbage:

* Different algorithms  reclaim memory:
* Minor GC: Cleans the Young Generation (fast but frequent).
* Major/Full GC: Cleans the Old Generation (slower, pauses the application).


3. Role of the JVM

The JVM is central to memory management and garbage collection:

Memory Allocation:
-> Allocates heap/stack memory and tracks object references.

GC Execution:
-> Runs garbage collectors (e.g:  Serial, Parallel) based on heap usage and configuration.
-> Triggers GC when memory pools  fill up.





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
        String string1 = "swiss";
        System.out.println("First non-repeating character in :" + string1 + "is :" + findFirstNonRepeatingChar(string1));
        String string2 = "DIGI5";
        System.out.println("First non-repeating character in :" + string2 + "is :" + findFirstNonRepeatingChar(string2));
    }
}

## Output:

First non-repeating character in swiss: w
First non-repeating character in DIGI5: D


### 5. Reverse Words in a Sentence

Write a Java function that takes a sentence as input and reverses the order of words while
keeping the characters in each word unchanged

Example :
Input: "Java is awesome"
Output: "awesome is Java"

Constraints:
• You cannot use built-in functions like Collections.reverse().
• Preserve spaces between words as in the input.


Solution :


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
