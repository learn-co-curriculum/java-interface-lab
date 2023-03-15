# Interface Lab

## Learning Goals

- Create an interface
- Create classes that implement an interface

## Instructions

Fork and clone this lab.

You will implement the following interface hierarchy:

![interface lab uml](https://curriculum-content.s3.amazonaws.com/6677/pillars/interface_lab_uml.png)

Create a new interface named `Flippable` with one abstract method named `flip()` that
takes no parameters and has a `void` return type.

Create a new class named `Coin` that implements `Flippable`.  The `flip()` method should
print a random string of "Heads" or "Tails" each time it is called.

Create a new class named `Mattress` that implements `Flippable`. Add a boolean instance
variable named `labelSideUp` that should be initialized to `true`.  Implement the `flip()`
method to toggle the value of `labelSideUp` and print the value as shown in the sample output below:

```text
Label side up is false
```

Edit the `Main` driver to instantiate an instance of each class and call the flip method 5 times in a
loop:

```java
public class Main {
	public static void main(String []args)  {
		Flippable coin = new Coin();
		for (int i = 0; i<5; i++) {
			coin.flip();
		}

		Flippable mattress = new Mattress(); 
		for (int i = 0; i<5; i++) {
			mattress.flip();
		}
	}
}
```

Confirm the output (random values may differ):

```text
Tails
Tails
Heads
Heads
Tails
Label side up is false
Label side up is true
Label side up is false
Label side up is true
Label side up is false
```

Edit the Junit class `FlippableTest` to add two methods `coinFlip()` and `mattressFlip()`
for testing the `Coin` and `Mattress` classes:

```java
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import java.io.ByteArrayOutputStream;
import java.io.PrintStream;

import static org.junit.jupiter.api.Assertions.*;

class FlippableTest {

    private final PrintStream standardOut = System.out;
    private final ByteArrayOutputStream outputStreamCaptor = new ByteArrayOutputStream();

    @BeforeEach
    public void setUp() {
        System.setOut(new PrintStream(outputStreamCaptor));
    }

    @AfterEach
    public void tearDown() {
        System.setOut(standardOut);
    }

    @Test
    void coinFlip() {
        Flippable coin = new Coin();
        for (int i = 0; i<20; i++) {
            coin.flip();
        }

        // should have at least one Heads and one Tails after 20 flips.
        String output = outputStreamCaptor.toString();
        assertTrue(output.contains("Heads"));
        assertTrue(output.contains("Tails"));

    }


    @Test
    void mattressFlip() {
        String expectedOutput = "Label side up is false\n" +
                "Label side up is true\n" +
                "Label side up is false\n" +
                "Label side up is true\n" +
                "Label side up is false\n";

        Flippable mattress = new Mattress();
        for (int i = 0; i<5; i++) {
            mattress.flip();
        }

        //compare expected output with actual output
        assertEquals(expectedOutput, outputStreamCaptor.toString());
    }

}
```

Run the Junit tests to confirm they pass.  In the rare case that the
program flips exactly 20 heads or 20 tails and the `coinFlip()` test fails,
try running the test again.