# Interface Lab

## Learning Goals

- Create an interface
- Create classes that implement an interface

## Instructions

Fork and clone this lab.

You will implement the following interface hierarchy:

![task3 uml](https://curriculum-content.s3.amazonaws.com/6677/pillars/task3_uml.png)

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
