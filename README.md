## Assignment 5 – Strategy Pattern

Yerkezhan Balagazinova. SE-2527  
**Topic:** Calculator using Strategy Pattern

## About the Project

This project demonstrates the Strategy Design Pattern using a simple calculator.

The calculator can perform different mathematical operations using separate strategy classes.

The available strategies are:

- `AddStrategy`
- `SubtractStrategy`
- `MultiplyStrategy`
- `DivideStrategy`

All strategies implement the same `CalculationStrategy` interface.

The `Calculator` class works as the Context. It stores the current strategy and delegates the calculation to it.

## Project Structure

```text
src/
├── CalculationStrategy.java
├── AddStrategy.java
├── SubtractStrategy.java
├── MultiplyStrategy.java
├── DivideStrategy.java
├── Calculator.java
└── Main.java
```

## How It Works

The common strategy interface is:

```java
public interface CalculationStrategy {
    double calculate(double a, double b);
}
```

Each operation has its own strategy class.

For example:

```java
public class AddStrategy implements CalculationStrategy {
    @Override
    public double calculate(double a, double b) {
        return a + b;
    }
}
```

The `Calculator` stores a reference to the current strategy:

```java
private CalculationStrategy strategy;
```

and delegates the calculation to it:

```java
public double calculate(double a, double b) {
    return strategy.calculate(a, b);
}
```

The strategy can also be changed at runtime:

```java
calculator.setStrategy(new MultiplyStrategy());
```

This means that the `Calculator` itself does not need to know how addition, subtraction, multiplication, or division are implemented.

## Runtime Strategy Switching

In `Main`, the calculator starts with one strategy:

```java
Calculator calculator = new Calculator(new AddStrategy());
```

Then the strategy can be changed:

```java
calculator.setStrategy(new SubtractStrategy());
calculator.setStrategy(new MultiplyStrategy());
calculator.setStrategy(new DivideStrategy());
```

The same `Calculator` object is reused while its behavior changes depending on the selected strategy.

## Example Output

```text
10 + 5 = 15.0
10 - 5 = 5.0
10 * 5 = 50.0
10 / 5 = 2.0
```

## How to Run

Open the project in IntelliJ IDEA and run `Main.java`.

## How to Add a New Strategy

To add a new mathematical operation, create a new class that implements `CalculationStrategy`.

For example:

```java
public class PowerStrategy implements CalculationStrategy {
    @Override
    public double calculate(double a, double b) {
        return Math.pow(a, b);
    }
}
```

Then the new strategy can be used without changing the `Calculator` class:

```java
calculator.setStrategy(new PowerStrategy());
```

This shows one of the main advantages of the Strategy Pattern: new behavior can be added without changing the existing Context.

## Strategy Pattern Structure

```text
                Main
                 |
                 v
             Calculator
                 |
                 v
        CalculationStrategy
          ^    ^    ^    ^
          |    |    |    |
        Add   Sub  Mult  Divide
```

`Main` is the Client.

`Calculator` is the Context.

`CalculationStrategy` is the Strategy interface.

`AddStrategy`, `SubtractStrategy`, `MultiplyStrategy`, and `DivideStrategy` are Concrete Strategies.
