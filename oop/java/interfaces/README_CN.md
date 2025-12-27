# 介面 (Interfaces)

## 簡介

在物件導向程式設計 (OOP) 中，**介面 (Interface)** 是一個關鍵概念，它定義了類別必須遵循的契約。它允許不同的類別共享共同的結構，同時強制執行特定的行為。介面廣泛用於 Java 和其他 OOP 語言中，以實現**抽象、多型和鬆散耦合**。

## 什麼是介面？

Java 中的**介面**是抽象方法 (沒有實作的方法) 的集合，類別可以實作這些方法。它定義了實作類別必須遵守的契約。

### **介面的主要特徵**
- 定義了實作類別必須遵循的**契約**。
- 不能有實例變數 (只有 `public static final` 常數)。
- 所有方法**隱式地是公開且抽象的** (除非它們有預設或靜態實作)。
- 支援**多重繼承**，這與類別不同。
- 提高**程式碼靈活性和可測試性**。

---

## **在 Java 中定義和實作介面**

### **步驟 1：定義介面**
要定義介面，請使用 `interface` 關鍵字。

```java
// 定義介面
public interface Vehicle {
    void start(); // 抽象方法 (無實作)
    void stop();  // 抽象方法 (無實作)
}
```

### **步驟 2：實作介面**
類別使用 `implements` 關鍵字來實作介面。

```java
// 在 Car 類別中實作 Vehicle 介面
public class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car is starting...");
    }
    
    @Override
    public void stop() {
        System.out.println("Car is stopping...");
    }
}
```

### **步驟 3：使用實作的類別**
現在，讓我們建立物件並呼叫方法。

```java
public class Main {
    public static void main(String[] args) {
        Vehicle myCar = new Car(); // 多型：介面參考
        myCar.start();
        myCar.stop();
    }
}
```

### **輸出：**
```
Car is starting...
Car is stopping...
```

---

## **介面的多重繼承**

與 C++ 不同，Java **不支援類別的多重繼承**，但它支援**介面的多重繼承**。

```java
// 第一個介面
interface Flyable {
    void fly();
}

// 第二個介面
interface Drivable {
    void drive();
}

// 實作多個介面
public class FlyingCar implements Flyable, Drivable {
    @Override
    public void fly() {
        System.out.println("FlyingCar is flying...");
    }
    
    @Override
    public void drive() {
        System.out.println("FlyingCar is driving...");
    }
}
```

### **用法**
```java
public class Main {
    public static void main(String[] args) {
        FlyingCar myVehicle = new FlyingCar();
        myVehicle.fly();
        myVehicle.drive();
    }
}
```

### **輸出：**
```
FlyingCar is flying...
FlyingCar is driving...
```

---

## **介面中的預設和靜態方法**

### **預設方法 (Default Methods)**
Java 8 在介面中引入了**預設方法**，允許方法擁有主體。

```java
interface Animal {
    void sound();
    
    // 具有實作的預設方法
    default void sleep() {
        System.out.println("Sleeping...");
    }
}

class Dog implements Animal {
    @Override
    public void sound() {
        System.out.println("Dog barks");
    }
}
```

### **用法**
```java
public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.sound();
        myDog.sleep(); // 呼叫預設方法
    }
}
```

### **輸出：**
```
Dog barks
Sleeping...
```

### **靜態方法 (Static Methods)**
介面也可以有**靜態方法**。

```java
interface MathOperations {
    static int add(int a, int b) {
        return a + b;
    }
}
```

### **用法**
```java
public class Main {
    public static void main(String[] args) {
        int result = MathOperations.add(5, 10);
        System.out.println("Sum: " + result);
    }
}
```

### **輸出：**
```
Sum: 15
```

---

## **真實世界範例：支付系統**

```java
interface Payment {
    void pay(double amount);
}

class CreditCardPayment implements Payment {
    @Override
    public void pay(double amount) {
        System.out.println("Paid " + amount + " using Credit Card");
    }
}

class PayPalPayment implements Payment {
    @Override
    public void pay(double amount) {
        System.out.println("Paid " + amount + " using PayPal");
    }
}
```

### **用法**
```java
public class Main {
    public static void main(String[] args) {
        Payment payment1 = new CreditCardPayment();
        payment1.pay(100.50);
        
        Payment payment2 = new PayPalPayment();
        payment2.pay(200.75);
    }
}
```

### **輸出：**
```
Paid 100.5 using Credit Card
Paid 200.75 using PayPal
```
