---
title: Java Course by CodeWithMosh part2笔记
date: 2021-03-09 14:18:49
tags:
- Java
- CodeWithMosh
categories: Java
---
Videos By: Mosh Hamedani
Link: https://www.bilibili.com/video/BV19J411t7dD
<!-- more -->

## 1 Getting Started

### 1.1 Programming Paradigms

- Procedural
- **Functional**
- **Object-oriented**
- Event-driven
- Logic
- Aspect-oriented

![image-20210130142255072](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210130142255072.png)

#### Object-oriented

bring **Data** and **Behavior** in a single object

#### Functional

**Data** and **Behavior** are different

#### Problem Solving

Process of **defining a problem**, identifying and comparing **different solutions** and picking the one that best solves that problem with respect to the **context** and **constraints**. 

### Choice in paradigms

Depends on the problem, context and budget. 

### 1.2 Benefits of Object-oriented Programming

- reduce complexity
- easier maintenance

- code reuse
- faster development

## 2 Classes

### 2.1 Classes and Objects

#### Class

A blueprint for creating objects. 

#### Objects

An instance of a class. 

#### UML

Short for **Unified Modeling Language**

![image-20210130215319545](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210130215319545.png)

### 2.2 Creating Classes

In src folder-> \<package> -> create a new class

Using Pascal Naming Convention

```java
package com.ryanhe;

public class TextBox {
    public String text; // field

    public void setText(String text){
        this.text = text; // "this" is used when the argument is the samme as the field.
        // In other cases, "this" is optional.
    }

    public void clear(){
        text = "";
    }
}
```

### 2.3 Creating Objects

If you do not initialize the reference type, it will be set to null.

```java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
       TextBox textBox1 = new TextBox();
        // var textBox1 = new TextBox();
        // "var" can only be used in editions after JDK10.
        // Current version: JDK8
        textBox1.setText("Box 1");
        System.out.println(textBox1.text.toUpperCase());

        TextBox textBox2 = new TextBox();
        textBox2.setText("Box 2");
        System.out.println(textBox2.text);
    }
}
```

### 2.4 Memory Allocation

![image-20210131085710681](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210131085710681.png)

```java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
       TextBox textBox1 = new TextBox();

       TextBox textBox2 = textBox1;

        textBox2.setText("Hello World");
        System.out.println(textBox1.text) ;
    }
}
```

The new TextBox object is stored in the heap.

The textBox1 is stored in the stack and it stores the address of the object.    

The textBox2 is referencing the same object.

#### Deallocation

Deallocation is automatically in Java -> Garbage collection.

### 2.5 Procedural Programming

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        int baseSalary = 50_000;
        int extraHours = 10;
        int hourlyRate = 20;
	    int wage = calculateWage(baseSalary, extraHours, hourlyRate);
        System.out.println(wage);
    }

    public static int calculateWage(
            int baseSalary,
            int extraHours,
            int hourlyRate
    ){
        return baseSalary + (extraHours * hourlyRate);
    }
}

~~~

In this program, the main class is bloated and the method has too many parameters.

So we'll use object-oriented programming to refactor it.

### 2.6 Encapsulation

#### Encapsulation

Encapsulation is to bundle the data and methods that operate on the data in a single unit. 

#### Employee.java

~~~java
package com.ryanhe;

public class Employee {
    public int baseSalary;
    public int hourlyRate;

    public int calculateWage(int extraHours){
        return baseSalary + hourlyRate * extraHours;
    }
}
~~~

#### Main.java

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        Employee employee = new Employee();
        employee.baseSalary = 50_000;
        employee.hourlyRate = 20;
        int wage = employee.calculateWage(10);
	    System.out.println(wage);
    }
}
~~~

### 2.7 Getters and Setters

Intro: what if the input salary is a negative integer?

One of the solutions: write a if statement to inspect the input of user. But it will make the main class bloated. So here we use setters and getters.

#### Main.java

```java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        Employee employee = new Employee();
        employee.setBaseSalary(50_000);
        employee.setHourlyRate(20);
        int wage = employee.calculateWage(10);
       System.out.println(wage);
    }
}
```

#### Employee.java

~~~java
package com.ryanhe;

public class Employee {
    private int baseSalary;
    private int hourlyRate;

    public int calculateWage(int extraHours){
        return baseSalary + hourlyRate * extraHours;
    }


    public void setBaseSalary(int baseSalary){
        if (baseSalary <= 0)
            throw new IllegalArgumentException("Salary cannot be o or less.");
        this.baseSalary = baseSalary;
    }

    public int getBaseSalary() { 
        return baseSalary;
    }

    public int getHourlyRate() {
        return hourlyRate;
    }

    public void setHourlyRate(int hourlyRate) {
        if (hourlyRate <= 0)
            throw new IllegalArgumentException("Hourly rate cannot be 0 or less.");
        this.hourlyRate = hourlyRate;
    }
}
~~~

#### Automatically add getters and setters

select the variable -> right click -> show context actions -> encapsulate field

### 2.8 Abstraction

#### Abstraction

Abstraction means to reduce complexity by hiding **unnecessary** details. 

### 2.9 Coupling

#### Coupling

Coupling is about how much a class is dependent upon or coupled to another class. 

![image-20210131100014398](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210131100014398.png)

hide or delete unnecessary coupling point 

```java
package com.ryanhe;

public class Employee {
    private int baseSalary;
    private int hourlyRate;

    public int calculateWage(int extraHours){
        return baseSalary + hourlyRate * extraHours;
    }


    public void setBaseSalary(int baseSalary){
        if (baseSalary <= 0)
            throw new IllegalArgumentException("Salary cannot be o or less.");
        this.baseSalary = baseSalary;
    }

    private int getBaseSalary() { // turn it into private to reduce the coupling point
        return baseSalary;
    }

    private int getHourlyRate() {
        return hourlyRate;
    }

    public void setHourlyRate(int hourlyRate) {
        if (hourlyRate <= 0)
            throw new IllegalArgumentException("Hourly rate cannot be 0 or less.");
        this.hourlyRate = hourlyRate;
    }


}
```

#### Easy way to create a method

~~~java
String address;
String ip = findIpAddress(address); 
~~~

Use the context action to create method automatically.

#### Easy way to create object

`new <Class Name>()` and use context action " Introduce local variable".

### 2.10 Constructor

~~~java
package com.ryanhe;

public class Employee {
    private int baseSalary;
    private int hourlyRate;

    public Employee(int baseSalary, int hourlyRate){ // constructor
        setBaseSalary(baseSalary);
        setHourlyRate(hourlyRate);
    }
    public int calculateWage(int extraHours){
        return baseSalary + hourlyRate * extraHours;
    }


    private void setBaseSalary(int baseSalary){
        if (baseSalary <= 0)
            throw new IllegalArgumentException("Salary cannot be o or less.");
        this.baseSalary = baseSalary;
    }

    private int getBaseSalary() { // turn it into private to reduce the coupling point
        return baseSalary;
    }

    private int getHourlyRate() {
        return hourlyRate;
    }

    private void setHourlyRate(int hourlyRate) {
        if (hourlyRate <= 0)
            throw new IllegalArgumentException("Hourly rate cannot be 0 or less.");
        this.hourlyRate = hourlyRate;
    }


}

~~~

### 2.11 Method Overloading

~~~java
public int calculateWage(int extraHours){
    return baseSalary + hourlyRate * extraHours;
}
public int calculateWage(){
    return calculateWage(0);
}
~~~

### 2.12 Constructor Overloading

~~~java
public Employee(int baseSalary){
        this(baseSalary, 0);
    }
public Employee(int baseSalary, int hourlyRate){
    setBaseSalary(baseSalary);
    setHourlyRate(hourlyRate);
}
~~~

#### Easy way to find parameters of a method

`ctrl` + `P`

### 2.13 Static Members

Instance members: belongs to **instances** or objects

Static menbers: belongs to a **class**

Example: `Employee.numberOfEmployees` is does not belongs to any object of Employee.

**It's unable for static method to access the non-static variables or methods unless you declare an object of the class.**

#### Why the main method is declared as static?

Because this is to enable Java runtime to directly call this method without having to create a new object.

## 3 Refactoring to an Object-oriented Design

### Easy way to move methods to new class

Select the method and use "refactor this" -> "Move" 

#### Why the `monthlyInterest` is refactored to a method instead of declaring and initializing in the constructor?

If we do so, it's unchangeable when the `annualInterest` is changed. 

### The Refactoring Result

#### Structure

4 classes:

- Main
- Console : Interact with users
- MortgageCalculator: Calculate relevant parameters 
- MortgageReport: Output the results

#### Main.java

```java
package com.ryanhe;

public class Main {
    public static void main(String[] args) {
        int principal = (int) Console.readNumber("Principal(￥1K - ￥1M): ", 1000, 1_000_000);
        float annualInterest = (float) Console.readNumber("Annual Interest Rate: ", 0, 30);
        byte years = (byte) Console.readNumber("Period(Years): ", 1, 30);

        MortgageCalculator calculator = new MortgageCalculator(principal, annualInterest, years);

        MortgageReport report = new MortgageReport(calculator);
        report.printMortgage();
        report.printPaymentSchedule();
    }
}
```

#### Console.java

```java
package com.ryanhe;

import java.util.Scanner;

public class Console {
    private static Scanner scanner = new Scanner(System.in);

    public static double readNumber(String prompt) {
        double value;
        System.out.print(prompt);
        value = scanner.nextDouble();
        return value;
    } // overload without min and max

    public static double readNumber(String prompt, double min, double max) {
        double value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextDouble();
            if (value >= min && value <= max)
                break;
            System.out.println("Enter a value between " + min + " and " + max + ".");
        }
        return value;
    }
}
```

#### MortgageCalculator.java

```java
package com.ryanhe;

public class MortgageCalculator {
    private final static byte MONTHS_IN_YEAR = 12;
    private final static byte PERCENT = 100;

    private int principal;
    private float annualInterest;
    private byte years;

    public MortgageCalculator(int principal, float annualInterest, byte years) {
        this.principal = principal;
        this.annualInterest = annualInterest;
        this.years = years;
    }

    public double calculateBalance(
            int numberOfPaymentsMade) {
        int numberOfPayments = getNumberOfPayments();
        double monthlyInterest = getMonthlyInterest();
        double balance = principal * (Math.pow(1 + monthlyInterest, numberOfPayments) - Math.pow(1 + monthlyInterest,
                numberOfPaymentsMade)) / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);
        return balance;
    }

    public double calculateMortgage() {
        int numberOfPayments = getNumberOfPayments();
        double monthlyInterest = getMonthlyInterest();

        double mortgage = principal * monthlyInterest * Math.pow(1 + monthlyInterest,
                numberOfPayments) / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);
        return mortgage;
    }

    public double[] getRemainingBalances(){
        double[] balances = new double[getNumberOfPayments()];
        for (short month = 0; month < balances.length; month++) {
            balances[month] = calculateBalance(month + 1);
        }
        return balances;
    }
    private double getMonthlyInterest() {
        return annualInterest / MONTHS_IN_YEAR / PERCENT;
    }

    private int getNumberOfPayments() {
        return  years * MONTHS_IN_YEAR;
    }
}
```

#### MortgageReport.java

```java
package com.ryanhe;

import java.text.NumberFormat;

public class MortgageReport {
    private final NumberFormat currency;
    private MortgageCalculator calculator;

    public MortgageReport(MortgageCalculator calculator) {
        this.calculator = calculator;
        currency = NumberFormat.getCurrencyInstance();
    }

    public void printPaymentSchedule() {
        System.out.println();
        System.out.println("PAYMENT SCHEDULE");
        System.out.println("----------------");
        for (double balance : calculator.getRemainingBalances()){
            System.out.println(currency.format(balance));
        }
    }

    public void printMortgage() {
        double mortgage = calculator.calculateMortgage();
        System.out.println("MORTGAGE");
        System.out.println("--------");
        System.out.println("Monthly Payments:" + currency.format(mortgage));
    }
}
```

## 4 Inheritance

### 4.1 Inheritance

![image-20210131202024208](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210131202024208.png)

```java
public class TextBox extends UIControl{
    private String text="";
}
```

### 4.2 The Object Class

All the classes extends the class **Object**, which is from Java.lang.

Core methods:

- equals()

- hashCode()

- toString()  package it originally is from, followed by an @ sign and finally the hash code, represented as hexadecimal.

  Example: `com.ryanhe.TextBox@1b6d3586`

- getClass()

### 4.3 Constructor and Inheritance

```java
package com.ryanhe;

public class TextBox extends UIControl{
    private String text="";

    public TextBox() {
        super(true); // super() is used to pass parameters to the base class constructor
        System.out.println("Textbox");
    }
}
```

### 4.4 Access Modifier

private is not inherited by subclasses.

protected and (default) should be avoided.

| modifier  | Current Class | Classes in the same package | Inheritance | Other classes |
| --------- | ------------- | --------------------------- | ----------- | ------------- |
| private   | √             | ×                           | ×           | ×             |
| (default) | √             | √                           | ×           | ×             |
| protected | √             | √                           | √           | ×             |
| public    | √             | √                           | √           | √             |

### 4.5 Method Overriding

**Pay attention to the difference between overload and override.**

#### Annotation

Annotation is basically a label that we attach to a class member.

Example: `@Override`

```
@Override
public String toString(){
    return text;
}
```

```java
// System.out.println(textBox.toString());
System.out.println(textBox); // println() automatically calls toString()
```

### 4.6 Upcasting and Downcasting

Upcasting is casting an object to one of its **super** types. 

Downcasting is casting an object to one of its **sub** types. 

```java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
       UIControl control = new UIControl(true);
       TextBox textBox = new TextBox();
       show(textBox);
       // show(control); will throw out an exception
        // control cannot be casted to the TextBox class.
    }
    public static void show(UIControl control){
        TextBox textBox = (TextBox)control;
        textBox.setText("Hello World");
        System.out.println(control);
    }
}
```

#### instanceof

instanceof is used to judge whether a variable is an instance of a class

Example: `control instanceof TextBox` 

#### Correction

```java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
       UIControl control = new UIControl(true);
       TextBox textBox = new TextBox();
       show(textBox);
    }
    public static void show(UIControl control){
        if (control instanceof TextBox) {
            TextBox textBox = (TextBox) control;
            textBox.setText("Hello World");
        }
        System.out.println(control);
    }
}
```

### 4.7 Comparing Objects

1. Right Click -> `generate` -> `Override Methods`

2. Right Click -> `generate` -> `equals() and hashCode()`

#### Method 1

```java
@Override
public boolean equals(Object obj) {
    if (this == obj)
        return true;
    if (!(obj instanceof Point))
        return false;
    Point other = (Point)obj;
    return other.x ==x && other.y == y;
}

@Override
public int hashCode() {
    return Objects.hash(x, y);
}
```

#### Method 2

~~~java
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Point point = (Point) o;
    return x == point.x && y == point.y;
}

@Override
public int hashCode() {
    return Objects.hash(x, y);
}
~~~

#### Main.java

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
	    Point point1 = new Point(1,2);
	    Point point2 = new Point(1,2);
        System.out.println(point1 == point2); // false, because they have different addresses.
        System.out.println(point1.equals(point2));// before override: false
        System.out.println(point1.hashCode());
        System.out.println(point2.hashCode());
    }

}
~~~

### 4.8 Polymorphism

In the UIControl class, define an empty render method. And in its sub classes, override the render method.

### 4.9 Abstract Classes and Methods

declare the class as abstract

~~~java
package com.ryanhe;

public abstract class UIControl {
    public boolean isEnabled = true;

    public abstract void render(); 
    // When we declare the method as abstract,
    // The subclasses must override this method.
    public void enable(){
        isEnabled = true;
    }
    public void disable(){
        isEnabled = false;
    }
}

~~~

### 4.10 Final Classes and Methods

#### Final Classes

If a class is declared as final, it cannot be extended.

#### Final Methods

If a method is declared as final, it cannot be overriden.

### 4.11 Deep Inheritance Hierarchies

**Do not create deep inheritance hierarchies.**

Example:

![image-20210131214847361](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210131214847361.png)

If Entity is modified, all these children and grandchildren should be compiled and redeployed. 

**NO MORE THAN 3 LEVELS.**

###  4.12 Multiple Inheritance

![image-20210131215324828](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210131215324828.png)

![image-20210131215356600](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210131215356600.png)

#### Diamond Problem

![image-20210131215427082](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210131215427082.png)

**Java does not support Multiple Inheritance.**

## 5 Inferface

### 5.1 What is Interface

We use interface to build loosely-coupled extensible testable applications. 

interface only have method declarations

![image-20210201223808995](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210201223808995.png)

- Interface tells us **what** should be done. 
- Classes tells us **how** it should be done. 

### 5.2 Creating an Interface

In the interface, public is not needed when declaring a method.

#### TaxCalculator.java

```java
package com.ryanhe;

public interface TaxCalculator {
    public double calculateTax();
}
```

#### TaxCalulator2018.java

```java
package com.ryanhe;

public class TaxCalculator2018 implements TaxCalculator{
    private double taxableIncome;

    public TaxCalculator2018(double taxableIncome) {
        this.taxableIncome = taxableIncome;
    }

    @Override
    public double calculateTax(){
        return taxableIncome * 0.3;
    }
}
```

#### TaxReport.java

```java
package com.ryanhe;

public class TaxReport {
    private TaxCalculator2018 calculator;

    public TaxReport(){
        calculator = new TaxCalculator2018(100_000);
    }

    public void show(){
        double tax = calculator.calculateTax();
        System.out.println(tax);
    }
}
```

### 5.3 Dependency Injection

Our Classes should not instantiate their dependencies.

- Constructor Injection
- Setter Injection 
- Method Injection

### 5.4 Constructor Injection

#### TaxReport.java

~~~java
package com.ryanhe;

public class TaxReport {
    private TaxCalculator calculator;

    public TaxReport(TaxCalculator calculator){ // constructor injection
        this.calculator = calculator;
    }

    public void show(){
        double tax = calculator.calculateTax();
        System.out.println(tax);
    }
}
~~~

#### Main.java

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        TaxCalculator2018 calculator = new TaxCalculator2018(100_000);
        TaxReport report = new TaxReport(calculator);
    }
}
~~~

### 5.5 Setter Injection

#### TaxReport.java

~~~java
package com.ryanhe;

public class TaxReport {

    private TaxCalculator calculator;

    public TaxReport(TaxCalculator calculator){ // constructor injection
        this.calculator = calculator;
    }

    public void show(){
        double tax = calculator.calculateTax();
        System.out.println(tax);
    }
    public void setCalculator(TaxCalculator calculator) { // setter injection
        this.calculator = calculator;
    }
}
~~~

#### Main.java

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        TaxCalculator2018 calculator = new TaxCalculator2018(100_000);
        TaxReport report = new TaxReport(calculator);
        report.show();

        report.setCalculator(new TaxCalculator2019());
        report.show();
    }
}
~~~

### 5.6 Method Injection

#### TaxReport.java

~~~java
package com.ryanhe;

public class TaxReport {

    private TaxCalculator calculator;

    public void show(TaxCalculator calculator){
        double tax = calculator.calculateTax();
        System.out.println(tax);
    }
}
~~~

#### Main.java

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        TaxCalculator2018 calculator = new TaxCalculator2018(100_000);
        TaxReport report = new TaxReport();
        report.show(calculator);
        report.show(new TaxCalculator2019());

    }
}
~~~

### 5.7 Interface Segregation Principle

Divide a big fat interface into a bunch of smaller ones.

**Class cannot have multiple parents, but an interface can have multiple parents.**

#### UIWidget.java

~~~java
package com.ryanhe;

public interface UIWidget
        extends Draggable, Resizable {
    void render();
}
~~~

Though every time we use the drag and resize, we should instantiate an object of UIWidget, the three methods belongs to different interface so, they are independent.

#### Draggable.java

```java
package com.ryanhe;

public interface Draggable {
    void drag();
}
```

#### Resizable.java

```java
package com.ryanhe;

public interface Resizable {
    void resize(int size);
    void resize(int x, int y);
    void resizeTo(UIWidget widget);
}
```

#### Dragger.java

```java
package com.ryanhe;

public class Dragger {
    public void drag(UIWidget widget) {
        widget.drag();
        System.out.println("Dragging done!");
    }
}
```

### 5.8 Bad Features on Interfaces

- Fields

  Declaring fields in our interfaces. 

  Fields are **final and static**.

  Fields should be declared in the implementations, so we should avoid using fields in our interfaces. 

- Static Methods

  ~~~java
  package com.ryanhe;
  
  public interface TaxCalculator {
      float minimumTax = 100; // final and static
      double calculateTax();
      static double getTaxableIncome(double income, double expenses){
          return income - expenses;
      }
  }
  ~~~

  Here we add a static method into the interface, but it will make our Interface have implementation.

  Solution: declare a new abstract method

- Private Methods

### 5.9 Interfaces and Abstract Classes

![image-20210202110958742](https://gitee.com/hrongxuan/my-photo/raw/master/image-20210202110958742.png)

### 5.10 When to Use Interface?

#### Benefits of Interface

- Swap Implementations
- Extend Your Applications
- Test Your Classes in Isolation