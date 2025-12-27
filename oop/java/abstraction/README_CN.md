# Java 中的抽象 (Abstraction)

## 簡介

**抽象 (Abstraction)** 是物件導向程式設計 (OOP) 的四大基本原則之一。它允許你隱藏**實作細節**，只暴露物件的必要部分。這有助於降低複雜度並提高可維護性。

在 Java 中，抽象主要透過以下方式實現：
1. **抽象類別 (Abstract Classes)**
2. **介面 (Interfaces)**

---

## **什麼是抽象？**

**抽象**意味著只顯示**必要的細節**並隱藏**實作**。它允許程式設計師專注於**物件做什麼**，而不是**它如何做**。

### **抽象的主要好處**
- **降低複雜度**：隱藏不必要的實作細節。
- **提高程式碼重用性**：鼓勵重用抽象邏輯。
- **增強安全性**：保護內部物件細節免受意外修改。
- **提高可維護性**：使程式碼更易於管理和更新。

---

## **1. 使用抽象類別實現抽象**

Java 中的**抽象類別**是一個不能被實例化的類別。它用於定義多個子類別應該實作的共同行為。

### **範例：Java 中的抽象類別**

```java
// 抽象類別
abstract class Vehicle {
    String brand;
    
    // 建構子
    Vehicle(String brand) {
        this.brand = brand;
    }
    
    // 抽象方法 (必須由子類別實作)
    abstract void start();
    
    // 具體方法 (可以被繼承)
    void displayBrand() {
        System.out.println("Brand: " + brand);
    }
}

// 實作抽象方法的子類別
class Car extends Vehicle {
    Car(String brand) {
        super(brand);
    }
    
    @Override
    void start() {
        System.out.println("Car is starting...");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle myCar = new Car("Toyota");
        myCar.displayBrand();
        myCar.start();
    }
}
```

### **輸出：**
```
Brand: Toyota
Car is starting...
```

**為什麼使用抽象類別？**
- 允許定義子類別必須實作的共同行為。
- 啟用部分抽象 (可以同時擁有抽象方法和具體方法)。
- 防止直接實例化基礎類別。

---

## **2. 使用介面實現抽象**

Java 中的**介面 (Interface)** 是一個藍圖，定義了類別必須遵循的契約。它包含**僅抽象方法** (直到 Java 8 引入了預設方法和靜態方法)。

### **範例：Java 中的介面**

```java
// 定義介面
interface Animal {
    void makeSound(); // 抽象方法
}

// 在 Dog 類別中實作介面
class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Dog barks");
    }
}

// 在 Cat 類別中實作介面
class Cat implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.makeSound();
        
        Animal myCat = new Cat();
        myCat.makeSound();
    }
}
```

### **輸出：**
```
Dog barks
Cat meows
```

**為什麼使用介面？**
- 促進**完全抽象** (隱藏所有實作細節)。
- 支援 Java 中的**多重繼承** (一個類別可以實作多個介面)。
- 提供不同類別實作行為的標準方式。

---

## **抽象類別 vs 介面：主要差異**

| 特性                   | 抽象類別 (Abstract Class)                           | 介面 (Interface)                               |
|------------------------|----------------------------------------------------|-----------------------------------------------|
| **繼承**               | 一個類別只能**繼承 (extends)** **一個**抽象類別    | 一個類別可以**實作 (implements)** **多個**介面 |
| **方法**               | 可以有**抽象 + 具體**方法                          | 只有抽象方法 (Java 8 之前)                    |
| **預設方法**           | 具體方法不需要 `default` 關鍵字                    | 支援 `default` 方法 (Java 8+)                 |
| **靜態方法**           | 可以有靜態方法                                     | 支援靜態方法 (Java 8+)                        |
| **欄位**               | 可以有**實例變數** (非 final)                      | 只有 **public static final** (常數)           |
| **建構子**             | 可以有建構子                                       | **不允許**有建構子                            |
| **多重繼承**           | 不支援 (僅**單一**繼承)                            | 支援**多重**繼承                              |
| **存取修飾符**         | 方法/欄位可以是 `public`, `protected`, `private` 或預設 | 方法預設為 `public`                           |
| **目的**               | **部分實作** (程式碼重用)                          | **完全抽象** (定義契約)                       |
| **物件建立**           | 不能直接實例化                                     | 不能直接實例化                                |
| **`super` 關鍵字**     | 可以使用 `super()` 呼叫父類別建構子                | 沒有 `super()` (沒有建構子)                   |
| **私有方法**           | 支援 `private` 方法 (Java 9+)                      | 支援 `private` 方法 (Java 9+)                 |
| **`final` 方法**       | 可以有 `final` 方法                                | 不能有 `final` 方法                           |

---

## **真實世界範例：支付系統**

抽象廣泛應用於真實世界的應用程式中，例如支付處理。

### **範例：使用抽象的支付系統**

```java
// Payment 的抽象類別
abstract class Payment {
    double amount;
    
    Payment(double amount) {
        this.amount = amount;
    }
    
    abstract void pay(); // 抽象方法
}

// 實作支付方法
class CreditCardPayment extends Payment {
    CreditCardPayment(double amount) {
        super(amount);
    }
    
    @Override
    void pay() {
        System.out.println("Paid " + amount + " using Credit Card");
    }
}

class PayPalPayment extends Payment {
    PayPalPayment(double amount) {
        super(amount);
    }
    
    @Override
    void pay() {
        System.out.println("Paid " + amount + " using PayPal");
    }
}

public class Main {
    public static void main(String[] args) {
        Payment payment;
        
        payment = new CreditCardPayment(150.75);
        payment.pay();
        
        payment = new PayPalPayment(200.50);
        payment.pay();
    }
}
```

### **輸出：**
```
Paid 150.75 using Credit Card
Paid 200.50 using PayPal
```

**為什麼在支付系統中使用抽象？**
- 允許在不修改現有程式碼的情況下增加多種支付方式。
- 提高可維護性和可擴展性。
- 為不同的支付類型提供**共同契約**。
