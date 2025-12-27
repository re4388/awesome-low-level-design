# Java 中的多型 (Polymorphism)

## 簡介

**多型 (Polymorphism)** 是物件導向程式設計 (OOP) 的四大基本原則之一。它允許單一介面用於不同類型的物件，從而實現**靈活性**、**可擴展性**和**程式碼重用**。

Java 中的多型可以分為兩種類型：
1. **編譯時多型 (方法多載 Method Overloading)**
2. **執行時多型 (方法覆寫 Method Overriding)**

## **什麼是多型？**

**多型**的意思是「多種形式」。它允許方法、函式或物件根據上下文表現出不同的行為。多型實現了**動態方法解析**和**方法靈活性**，使應用程式更容易擴展和維護。

### **多型的主要好處**
- **程式碼重用性**：編寫一個適用於多種類型的單一介面。
- **可擴展性**：以最少的程式碼更改添加新功能。
- **可維護性**：降低複雜度並提高程式碼清晰度。

---

## **1. 編譯時多型 (方法多載 Method Overloading)**

編譯時多型發生在同一個類別中的多個方法共享相同的名稱但具有**不同的方法簽章** (參數) 時。要呼叫的方法是在**編譯時**決定的。

### **方法多載的範例**

```java
class MathOperations {
    // 具有兩個參數的方法
    int add(int a, int b) {
        return a + b;
    }
    
    // 具有三個參數的方法 (多載)
    int add(int a, int b, int c) {
        return a + b + c;
    }
}

public class Main {
    public static void main(String[] args) {
        MathOperations math = new MathOperations();
        System.out.println("Sum (2 numbers): " + math.add(5, 10));
        System.out.println("Sum (3 numbers): " + math.add(5, 10, 15));
    }
}
```

### **輸出：**
```
Sum (2 numbers): 15
Sum (3 numbers): 30
```

**為什麼使用方法多載？**
- 提供更清晰、更直觀的介面。
- 透過對類似操作使用單一方法名稱來減少冗餘。

---

## **2. 執行時多型 (方法覆寫 Method Overriding)**

執行時多型發生在子類別提供其父類別中已定義方法的**特定實作**時。要呼叫的方法是在**執行時**決定的。

### **方法覆寫的範例**

```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Dog(); // 向上轉型 (Upcasting)
        myAnimal.makeSound();
        
        myAnimal = new Cat(); // 動態方法分派 (Dynamic method dispatch)
        myAnimal.makeSound();
    }
}
```

### **輸出：**
```
Dog barks
Cat meows
```

**為什麼使用方法覆寫？**
- 啟用**動態方法解析**。
- 支援**多型行為**，其中一個介面可以用於多種實作。
- 透過允許未來的修改使程式碼具有**可擴展性**。

---

## **使用介面的多型**

多型廣泛用於**介面**，允許不同的類別共享共同的契約。

```java
interface Vehicle {
    void start();
}

class Car implements Vehicle {
    public void start() {
        System.out.println("Car is starting...");
    }
}

class Bike implements Vehicle {
    public void start() {
        System.out.println("Bike is starting...");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle myVehicle = new Car();
        myVehicle.start();
        
        myVehicle = new Bike();
        myVehicle.start();
    }
}
```

### **輸出：**
```
Car is starting...
Bike is starting...
```

**為什麼使用介面的多型？**
- 促進**鬆散耦合**，使程式碼更靈活。
- 允許同一行為的多種實作。
- 啟用**依賴注入**，提高可測試性。

---

## **真實世界範例：支付系統**

多型的一個常見真實世界用例是在**支付處理**中。

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

public class Main {
    public static void main(String[] args) {
        Payment payment;
        
        payment = new CreditCardPayment();
        payment.pay(100.50);
        
        payment = new PayPalPayment();
        payment.pay(200.75);
    }
}
```

### **輸出：**
```
Paid 100.5 using Credit Card
Paid 200.75 using PayPal
```

**為什麼在支付系統中使用多型？**
- 允許添加新的支付方式而**無需修改現有程式碼**。
- 提供**靈活且可擴展**的設計。
- 提高**程式碼可讀性和可維護性**。
