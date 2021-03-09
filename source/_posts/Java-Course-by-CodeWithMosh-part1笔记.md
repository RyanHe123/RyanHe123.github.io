---
title: Java Course by CodeWithMosh part1笔记
date: 2021-03-09 13:15:28
tags:
- Java
- CodeWithMosh
categories: 
- Java
toc: true
---

Videos by: Mosh Hamedani
Link: https://www.bilibili.com/video/BV19J411t7dD
<!-- more -->

## 1 Getting Started

### 1.1 Installing Java

JDK: Java Development Kit

### 1.2 Anatomy of a Java Program

#### Function

~~~java
void sendEmail(){
    ...
}
~~~

every java program should have at least one function: **main()**

function belongs to class

#### Class

container for related functions 

~~~java
class Main{
    void main(){
        
    }
}
~~~

method: a function that is part of a class

#### Access Modifier

public private etc.

~~~java
public class Main{
    public void main(){
        
    }
}
~~~

#### Name Convention

Classes: pascal **P**ascal**N**aming**C**onvention

Methods: camel camel**N**aming**C**onvention

### 1.3 Your First Java Program

#### Package

Group related classes。

#### Structure

- Project
  - src :source folder
    - com.package (base package)
      - class Main

~~~java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
	    System.out.println("Hello World"); // System:class out:field println:function
    }
}
~~~

### 1.4 How Java Code Gets Executed

Two steps: compilation execution

#### Compilation

![屏幕截图 2021-01-28 171307](https://gitee.com/hrongxuan/my-photo/raw/master/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202021-01-28%20171307.jpg)

In cmd: javac Main.java

Get the file: Main.class

#### Execution

Java Runtime Environment (JRE)

![屏幕截图 2021-01-28 172139](https://gitee.com/hrongxuan/my-photo/raw/master/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202021-01-28%20172139.jpg)

In cmd: java com.\<package name>.Main

### 1.5 5 Interesting Facts about Java

1. Four editions of Java
   - Standard Edition SE
   - Enterprise Edition EE: 
     - large scale and distributed system 
     - fault tolerant distributed multi-tiered software
   - Micro Edition ME:
     - mobile devices
   - Java Card:
     - smart card

## 2 Types

### 2.1 Variables

~~~java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
	    int myAge = 30;
	    int herAge = myAge;
        System.out.println(herAge);
    }
}
~~~

### 2.2 Primitive Types

- Primitive for storing simple values
- Reference for storing complex objects

| Type    | Bytes | Range             |
| ------- | ----- | ----------------- |
| byte    | 1     | [-128,127]        |
| short   | 2     | [-32K,32K]        |
| int     | 4     | [-2B,2B]          |
| long    | 8     |                   |
| float   | 4     |                   |
| double  | 8     |                   |
| char    | 2     | A,B,C...(UNICODE) |
| boolean | 1     | true/false        |

~~~java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
	    byte age = 30;
	    int viewsCount = 123_456_789; //use underscore to represent long integer (optional)
        long viewsCount2 = 3_123_456_789L; //remember the L(both upper and lower are OK,but upper recommended)
        float price = 10.99f; //10.99 is viewed as double by default, so add f/F at the end of the number
        char letter = 'A';
        boolean isEligible = true;
    }
}
~~~

### 2.3 Reference Types

sout + `Tab` can easily call out `System.out.println();`

~~~java
package com.ryanhe; // package statement

import java.util.Date; // This line is added automatically.

public class Main {

    public static void main(String[] args) {
	    byte age = 30;
        Date now = new Date();
        System.out.println(now); // get the current time on your device
    }
}
~~~

### 2.4 Primitive VS. Reference

#### Primitive 

~~~java
package com.ryanhe; // package statement


public class Main {

    public static void main(String[] args) {
	    byte x = 1;
	    byte y = x;
	    x = 2;
        System.out.println(y); // 1
        // x & y are independent.
    }
}
~~~

#### Reference

~~~java
package com.ryanhe; // package statement

import java.awt.*;

public class Main {

    public static void main(String[] args) {
        Point point1 = new Point(1, 1);
        Point point2 = point1;
        point1.x = 2;
        System.out.println(point2.x);
    }
}
~~~

point1 and point2 stores the address, so the 2 variables share the same value.

### 2.5 Strings

~~~java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
        // String message = new String("Hello world");
        String message = "  Hello world" + "!!"; //string is still reference type
        System.out.println(message.startsWith("!!"));
        System.out.println(message.endsWith("!!"));
        System.out.println(message.length());
        System.out.println(message.indexOf("sky")); 
        System.out.println(message.replace("!","*"));
        //target & replacement are parameters !  * are arguments
        System.out.println(message.toLowerCase());
        System.out.println(message.trim()); // remove the space at the beginning or end of the string
        System.out.println(message); // Hello world!!
        // string is immutable!!!
    }
}
false
true
15
-1
  Hello world**
  hello world!!
Hello world!!
  Hello world!!
~~~

### 2.6 Escape Sequences

`\"	` 	`\\` 	`\n		` 	`\t`

~~~java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
        // c:\Windows\...
        String address = "c:\\Windows\\..."; // c:\Windows\...
        System.out.println(address);
        String message = "Hello \t\"Ryan\"";
        System.out.println(message);
        System.out.println(address + '\n' + message);
    }
}
~~~

### 2.7 Arrays

~~~java
package com.ryanhe; // package statement

import java.util.Arrays;

public class Main {

    public static void main(String[] args) {
        int[] numbers = new int[5]; // array is reference type
        numbers[0] = 1;
        numbers[1] = 2;
        // numbers[10] = 3;
        //Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 10
        // at com.ryanhe.Main.main(Main.java:9)
        System.out.println(numbers); // [I@1b6d3586
        System.out.println(Arrays.toString(numbers)); // [1, 2, 0, 0, 0] 0 is default
        // In boolean array false is default
        // In string array empty string is default
        int[] numbers2 = {2,3,5,1,4};
        System.out.println(numbers2.length);
        Arrays.sort(numbers2);
        System.out.println(Arrays.toString(numbers2));
    }
}
~~~

### 2.8 Multi-dimensional Arrays

~~~java
package com.ryanhe; // package statement

import java.util.Arrays;

public class Main {

    public static void main(String[] args) {
        int[][] numbers = new int[2][3]; // array is reference type
        numbers[0][0] = 1;
        System.out.println(Arrays.toString(numbers)); // [[I@1b6d3586, [I@4554617c]
        System.out.println(Arrays.deepToString(numbers));
        int [][] numbers2 = {{1,2,3},{4,5,6}};
        System.out.println(Arrays.deepToString(numbers2)); //[[1, 2, 3], [4, 5, 6]]
    }
}
~~~

### 2.9 Constants

~~~java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
        final float PI = 3.14f;
        // PI = 1; Cannot assign a value to final variable 'PI'
    }
}
~~~

### 2.10 Arithmetic Expressions

~~~java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
        int result = 10 / 3;
        System.out.println(result); // 3
        double result2 = (double)10 / (double)3; // 3.3333333333333335
        System.out.println(result2);
        int x = 1;
        x++; // ++ increment operator
        // ++x;
        int y = x++;
        System.out.println(x); // 3
        System.out.println(y); // 2
        int z = ++y;
        System.out.println(y); // 3
        System.out.println(z); // 3
        x += 2; // augmented/compound assignment operator
    }
}
~~~

### 2.11 Order of Operations

```java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
        int x = 10 + 3 * 2;
        System.out.println(x); // 16
        int y = (10 + 3) * 2;
        System.out.println(y); // 26
    }
}
```

### 2.12 Casting

#### Implicit Casting

~~~java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
        // Implicit casting
        // byte > short > int > long > float > double 
        short x = 1;
        int y = x + 2;
        System.out.println(y); // 3
        double j = 1.1;
        double k = j + 2;
        System.out.println(k); // 3.1
    }
}
~~~

1. create an anonymous variable
2. copy the value of x to this memory space
3. add the two numbers together

#### Explicit Casting  

~~~java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
        double x = 1.1;
        int y = (int)x + 2;
        System.out.println(y); // 3
    }
}
~~~

<font color ='red' >Explicit casting only happens between compatible variables.</font>

We cannot cast a string to a number.

#### String to numbers

```java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
        String x = "1";
        int y = Integer.parseInt(x) + 2; // Integer class in java.lang
        // Short.parseShort();
        // Float.parseFloat();
        System.out.println(y);
    }
}
```

### 2.13 The Math Class

```java
package com.ryanhe; // package statement

public class Main {

    public static void main(String[] args) {
        int result = Math.round(1.1f);
        System.out.println(result);
        int x = (int)Math.ceil(1.1f); // the return value of ceil is double
        int y = (int)Math.floor(1.1f);
        int z = Math.max(x,y);
        double j = Math.random(); // 0~1
        int k = (int)Math.round(Math.random()*100);
        System.out.println(j);
    }
}
```

### 2.14 Formatting Numbers

#### Factory Method

`getCurrencyInstance()`

#### Rename variables

1. refactor -> rename
2. `shift`	+	`F6`

#### Method Chaining

~~~java
NumberFormat.getPercentInstance().format(0.1)
~~~

~~~java
package com.ryanhe; // package statement

import java.text.NumberFormat;

public class Main {

    public static void main(String[] args) {
        // NumberFormat currency = new NumberFormat();
        // 'NumberFormat' is abstract cannot be instantiated
        NumberFormat currency = NumberFormat.getCurrencyInstance();
        String result = currency.format(1234567.891);
        System.out.println(result); // ￥1,234,567.89
        NumberFormat percentage = NumberFormat.getPercentInstance();
        String result2 = percentage.format(0.1); // 10%
        System.out.println(result2);
    }
}
~~~

### 2.15 Reading Input

```java
package com.ryanhe; // package statement

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Age: "); // don't start a new line
        byte age = scanner.nextByte();
        // nextLine nextBoolean ...
        // don't have nextString
        System.out.println("You are " + age);
        System.out.print("Name: ");
        // String name = scanner.next();  it only reads one token at a time
        scanner.nextLine();
        String name = scanner.nextLine().trim();
        System.out.println("You are " + name);
    }
}
```

### 2.16 Project: Mortgage Calculator

#### Mortgage Calculation Formula

Premise: the same mortgage for each month

Principal $P$ 

Monthly interest rate $r$

Period(months) $n$

The formula: $M=P\frac{r(1+r)^n}{(1+r)^n-1}$

Proof:

**Remaining Mortgage**

The first month:  $P(1+r)-M$

The second month: $(P(1+r)-M)(1+r)-M=P(1+r)^2-M(1+1+r)$

The third month: $P(1+r)^2-M(1+1+r)](1+r)-M=P(1+r)^3-M(1+(1+r)+(1+r)^2)$

$\cdots$

The n-th month: $P(1+r)^n-M(1+(1+r)+\cdots+(1+r)^{n-1})=0$

#### My Answer

```java
package com.ryanhe;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Principal: ");
        double principal = scanner.nextDouble();
        System.out.print("Annual Interest Rate: ");
        double annualInterestRate = scanner.nextDouble();
        double monthlyInterestRate = annualInterestRate/1200;
        System.out.print("Period(Years): ");
        int period = scanner.nextInt();
        int months = period*12;
        double mortgage = principal*monthlyInterestRate*Math.pow(1+monthlyInterestRate,
                (double)months)/(Math.pow(1+monthlyInterestRate,(double)months)-1);
        System.out.print("Mortgage: ");
        NumberFormat currency = NumberFormat.getCurrencyInstance();
        System.out.println(currency.format(mortgage));
    }
}
```

#### Solution

~~~java
final byte MONTHS_IN_YEAR = 12;
final byte PERCENT = 100;
~~~

The usage of the final variables  is to avoid **Magic Number**.

#### Magic Number

In wikipedia:

> - Unique values with unexplained meaning or multiple occurrences which could (preferably) be replaced with named constants
> - A constant numerical or text value used to identify a [file format](https://en.wikipedia.org/wiki/File_format) or protocol; for files, see [List of file signatures](https://en.wikipedia.org/wiki/List_of_file_signatures)
> - Distinctive unique values that are unlikely to be mistaken for other meanings (e.g., [Globally Unique Identifiers](https://en.wikipedia.org/wiki/Globally_Unique_Identifier))

Here the magic number is the first meaning. 

A number without name is hard for others to understand or correct your code.

So it should be replaced by constants.

## 3 Control Flow

### 3.1 Comparison operators

#### Boolean Expression

`x == y`

`x != y`

`x <= y`

### 3.2 Logical Operators

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
	    int temperature = 22;
	    boolean isWarm = temperature > 20 && temperature < 30;
        System.out.println(isWarm);
        boolean hasHighIncome = true;
        boolean hasGoodCredit = true;
        boolean hasCriminalRecord = false;
        boolean isEligible = (hasHighIncome || hasGoodCredit) && !hasCriminalRecord;
    }
}
~~~

### 3.3 If Statements

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
	    int temperature = 32;
	    if(temperature > 30){
            System.out.println("It's a hot day");
            System.out.println("Drink water");
        } 
	    else if(temperature > 20)
            System.out.println("Beautiful day");
	    else
            System.out.println("Cold day");
    }
}
~~~

### 3.4 Simplifying If Statements

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        int income = 120_000;
        // boolean hasHighIncome = false; 
        // give the hasHignIncome a default value to simplify the condition judgement
        // if (income > 100_100)
            // hasHighIncome = true;
        boolean hasHighIncome = (income > 100_000);
    }
}

~~~

### 3.5 The Ternary Operator

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        int income = 120_000;
//        String className = "Economy";
//        if (income > 100_000)
//            className = "First";
        String className = income > 100_000 ? "First" : "Economy";
    }
}
~~~

### 3.6 Switch Statements

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        String role = "admin";
        switch (role){
            case "admin":
                System.out.println("You're an admin.");
                break;
            case "moderator":
                System.out.println("You're a moderator");
            default:
                System.out.println("You're a guest");
        }
    }
}
~~~

### 3.7 Exercise : FizzBuzz

#### My Answer

~~~java
package com.ryanhe;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        int FIZZ = 5;
        int BUZZ = 3;
	    Scanner scanner = new Scanner(System.in);
        System.out.print("Number: ");
        int number = scanner.nextInt();
        if (number % FIZZ == 0)
            System.out.print("FIZZ");
        if (number % BUZZ == 0)
            System.out.println("BUZZ");
        if (number % FIZZ != 0 && number % BUZZ !=0)
            System.out.println(number);
    }
}
~~~

#### Solution

Use one if statement -> Avoid nested structure

### 3.8 For Loops

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
        for (int i = 0; i < 5; i++)
            System.out.println("Hello world " + i);
    }
}
~~~

### 3.9 While Loops

~~~java
package com.ryanhe;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        String input = "";
        Scanner scanner = new Scanner(System.in);
        while(!input.equals("quit")){
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
            System.out.println(input);
        }
    }
}
~~~

### 3.10 Do..While Loops

~~~java
package com.ryanhe;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        String input = "";
        Scanner scanner = new Scanner(System.in);
        do{
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
            System.out.println(input);
        } while(!input.equals("quit"))
    }
}
~~~

### 3.11 Break and Continue

~~~java
package com.ryanhe;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        String input = "";
        Scanner scanner = new Scanner(System.in);
        while(true){
            System.out.print("Input: ");
            input = scanner.next().toLowerCase();
            if(input.equals("pass"))
                continue;
            if(input.equals("quit"))
                break;
            System.out.println(input);
        }
    }
}
~~~

### 3.12 For-Each Loop

The disadvantage of For-each loop: It cannot iterate from the end to the beginning.

### 3.13 Improve the Mortgage Calculator

#### My Answer

~~~java
package com.ryanhe;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;
        Scanner scanner = new Scanner(System.in);
        double principal;
        while(true){
            System.out.print("Principal (￥1K - ￥1M): ");
            principal = scanner.nextDouble();
            if(principal < 1000 || principal > 1000_000)
                System.out.println("Enter a value between 1,000 and 1,000,000.");
            else
                break;
        }
        double annualInterestRate;
        while (true){
            System.out.print("Annual Interest Rate: ");
            annualInterestRate = scanner.nextDouble();
            if (annualInterestRate > 0 && annualInterestRate <= 30)
                break;
            else
                System.out.println("Enter a value greater than 0 and less than or equal to 30.");
        }
        double monthlyInterestRate = annualInterestRate / MONTHS_IN_YEAR / PERCENT;
        int period;
        while (true){
            System.out.print("Period(Years): ");
            period = scanner.nextInt();
            if (period >= 1 && period <=30)
                break;
            else
                System.out.println("Enter a value between 1 and 30.");
        }
        int months = period*12;
        double mortgage = principal*monthlyInterestRate*Math.pow(1+monthlyInterestRate,
                (double)months)/(Math.pow(1+monthlyInterestRate,(double)months)-1);
        System.out.print("Mortgage: ");
        NumberFormat currency = NumberFormat.getCurrencyInstance();
        System.out.println(currency.format(mortgage));
    }
}
~~~

#### Solution

1. year is no more than 30, so we can use `byte year`

2. if  there is a `break` in the if statement, we can delete the useless `else`.

## 4 Clean Coding

### 4.1 Creating Methods

~~~java
package com.ryanhe;

public class Main {

    public static void main(String[] args) {
	    greetUser("Ryan","He");
	    greetUser("Mosh","Hamedani");
    }
    public static String greetUser(String firstName, String lastName){
        System.out.println("Hello " + firstName + " " + lastName);
        return "Hello " + firstName + " " + lastName;
    }
}
~~~

### 4.2 Refactoring

#### Refactoring

Changing the structure of the code without changing its behavior.

1. Repetitive patterns on the code
2. Lines that are highly related

### 4.3 Extracting Methods

#### The calculateMortgage

~~~java
    public static double calculateMortgage(
            int principal,
            float annualInterest,
            byte years){
        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;
        
        short numberOfPayments = (short)(years * MONTHS_IN_YEAR);
        double monthlyInterestRate = annualInterest / MONTHS_IN_YEAR / PERCENT;
        
        double mortgage = principal*monthlyInterestRate*Math.pow(1+monthlyInterestRate,
                numberOfPayments) /(Math.pow(1+monthlyInterestRate, numberOfPayments)-1);
        return mortgage;
    }
~~~

### 4.4 Refactoring Repetitive Patterns

~~~java
package com.ryanhe;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        int principal = (int)readNumber("Principal(￥1K-￥1M): ",1000,1_000_000);
        float annualInterest = (float)readNumber("Annual Interest Rate: ", 0, 30);
        byte years = (byte)readNumber("Period(Years): ", 1, 30);
        
        double mortgage = calculateMortgage(principal, annualInterest, years);
        
        NumberFormat currency = NumberFormat.getCurrencyInstance();
        System.out.println(currency.format(mortgage));
    }
    
    public static double readNumber(String prompt, double min, double max){
        Scanner scanner = new Scanner(System.in);
        double value;
        while (true){
            System.out.print(prompt);
            value = scanner.nextInt();
            if (value >= min && value <=max)
                break;
            System.out.println("Enter a value between " + min + " and " + max + ".");
        }
        return value;
    }
    
    public static double calculateMortgage(
            int principal,
            float annualInterest,
            byte years){
        final byte MONTHS_IN_YEAR = 12;
        final byte PERCENT = 100;

        short numberOfPayments = (short)(years * MONTHS_IN_YEAR);
        double monthlyInterestRate = annualInterest / MONTHS_IN_YEAR / PERCENT;

        double mortgage = principal*monthlyInterestRate*Math.pow(1+monthlyInterestRate,
                numberOfPayments) /(Math.pow(1+monthlyInterestRate, numberOfPayments)-1);
        return mortgage;
    }
}
~~~

### 4.5 Payment Schedule

#### Remainig Loan Balance Formula

Premise: the same mortgage for each month

Principal $P$ 

Monthly interest rate $r$

Period(months) $n$

Number of payments made $c$

The formula: $B=P\frac{(1+r)^n-(1+r)^c}{(1+r)^n-1}$

#### Refactoring

Main Menu -> Refactor -> Extract -> Method

#### Solution

~~~java
package com.ryanhe;

import java.text.NumberFormat;
import java.util.Scanner;

public class Main {
    final static byte MONTHS_IN_YEAR = 12;
    final static byte PERCENT = 100;
    // they are field and remember to add static
    public static void main(String[] args) {
        int principal = (int) readNumber("Principal(￥1K - ￥1M): ", 1000, 1_000_000);
        float annualInterest = (float) readNumber("Annual Interest Rate: ", 0, 30);
        byte years = (byte) readNumber("Period(Years): ", 1, 30);

        printMortgage(annualInterest, principal, years);

        printPaymentSchedule(principal, years, annualInterest);
    }

    public static void printMortgage(float annualInterest, int principal, byte years) {
        double mortgage = calculateMortgage(principal, annualInterest, years);
        NumberFormat currency = NumberFormat.getCurrencyInstance();
        System.out.println("MORTGAGE--------\nMonthly Payments:" + currency.format(mortgage));
    }

    public static void printPaymentSchedule(int principal, byte years, float annualInterest) {
        System.out.println();
        System.out.println("PAYMENT SCHEDULE\n----------------");
        for (short month = 0; month < years * MONTHS_IN_YEAR; month++) {
            System.out.println(NumberFormat.getCurrencyInstance().format(calculateBalance(principal, annualInterest,
                    years, (short) (month+1))));
        }
    }

    public static double readNumber (String prompt,double min, double max){
        Scanner scanner = new Scanner(System.in);
        double value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextInt();
            if (value >= min && value <= max)
                break;
            System.out.println("Enter a value between " + min + " and " + max + ".");
        }
        return value;
    }

    public static double calculateBalance(
            int principal,
            float annualInterest,
            byte years,
            short numberOfPaymentsMade){
        short numberOfPayments = (short) (years * MONTHS_IN_YEAR);
        double monthlyInterest = annualInterest / MONTHS_IN_YEAR / PERCENT;
        double balance =  principal * (Math.pow(1 + monthlyInterest, numberOfPayments) - Math.pow(1 + monthlyInterest,
                numberOfPaymentsMade)) / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);
        return balance;
    }

    public static double calculateMortgage (
            int principal,
            float annualInterest,
            byte years){
        short numberOfPayments = (short) (years * MONTHS_IN_YEAR);
        double monthlyInterest = annualInterest / MONTHS_IN_YEAR / PERCENT;

        double mortgage = principal * monthlyInterest * Math.pow(1 + monthlyInterest,
                numberOfPayments) / (Math.pow(1 + monthlyInterest, numberOfPayments) - 1);
        return mortgage;
    }
}
~~~

### 4.6 Summary

- Keep your methods short
  - method: 5-10 lines, no more than 20 lines.

- Extract repetitive patterns
- Extract highly related statements

## 5 Debugging and Deploying Applications

### 5.1 Types of Errors

- Compile-time Errors
  - grammar
  - syntax
- Run-time Errors
  - Debugger

### 5.2 Common Syntax Errors

- don't forget to specify the type
- semicolon

- parenthesis
- double quotes of String
- misspell (**case sensitive**)
- do not use the reserve key words 
- misuse `=` and `==`

### 5.3 Debugging Java Applications

break point: `ctrl`+`F8`

dubug: `shift`+`F9`

add watch

### 5.4 Packaging Java Applications

console or command line appilcation

JAR file (Java archieve)

File -> Program Structure -> Artifacts -> `+` -> JAR -> from modules with dependencies

Build -> Build Artifacts

Module is  another level of abstraction above package

In command line:

~~~
java -jar <jar file name>
~~~

