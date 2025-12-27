# Java 中的封裝 (Encapsulation)

## 簡介

**封裝 (Encapsulation)** 是物件導向程式設計 (OOP) 的四大基本原則之一。它是將**資料 (變數) 和操作該資料的方法**捆綁到一個單元 (類別) 中，同時限制對內部細節的直接存取的做法。

在 Java 中，封裝主要透過以下方式實現：
1. **存取修飾符 (Access Modifiers)** (`private`, `protected`, `public`)
2. **Getter 和 Setter 方法**
3. **資料隱藏 (Data Hiding)**

封裝有助於程式碼的**資料保護、模組化和可維護性**。

---

## **什麼是封裝？**

封裝意味著將資料 (變數) 和程式碼 (方法) **包裝**在一起成為一個單元 (類別)。它限制了對物件某些組件的直接存取，這有助於保護資料完整性並防止意外修改。

### **封裝的主要好處**
- **資料隱藏**：防止直接存取敏感資料。
- **增加安全性**：控制資料的存取和修改方式。
- **提高程式碼可維護性**：允許在不影響程式碼其他部分的情況下進行更改。
- **更好的模組化**：將程式碼組織成邏輯組件。

---

## **使用存取修飾符實現封裝**

Java 提供**存取修飾符**來強制執行封裝：
- **`private`**：僅在同一個類別內可存取。
- **`protected`**：在同一個套件和子類別內可存取。
- **`public`**：從任何地方都可存取。

### **範例：使用私有變數的封裝**

```java
// 具有封裝資料的類別
class BankAccount {
    private String accountHolder;
    private double balance;

    // 建構子
    public BankAccount(String accountHolder, double balance) {
        this.accountHolder = accountHolder;
        this.balance = balance;
    }

    // 存取餘額的 Getter 方法
    public double getBalance() {
        return balance;
    }

    // 修改餘額的 Setter 方法
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        } else {
            System.out.println("Invalid deposit amount");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("Alice", 1000);
        System.out.println("Current Balance: " + account.getBalance());
        account.deposit(500);
        System.out.println("Updated Balance: " + account.getBalance());
    }
}
```

### **輸出：**
```
Current Balance: 1000.0
Deposited: 500.0
Updated Balance: 1500.0
```

**為什麼使用封裝？**
- 防止未經授權存取資料。
- 允許透過方法進行受控修改。

---

## **使用 Getter 和 Setter 實現封裝**

封裝確保**資料不能被直接存取**，而必須透過方法檢索或修改。

### **範例：Java 中的 Getter 和 Setter**

```java
class Employee {
    private String name;
    private int age;

    // Getter 方法
    public String getName() {
        return name;
    }

    // Setter 方法
    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age > 18) {
            this.age = age;
        } else {
            System.out.println("Age must be greater than 18");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee();
        emp.setName("John Doe");
        emp.setAge(25);
        System.out.println("Employee Name: " + emp.getName());
        System.out.println("Employee Age: " + emp.getAge());
    }
}
```

### **輸出：**
```
Employee Name: John Doe
Employee Age: 25
```

---

## **封裝與資料隱藏**

封裝有助於**隱藏實作細節**，同時只暴露必要的方法。

### **範例：隱藏實作細節**

```java
class Account {
    private double balance;

    public Account(double initialBalance) {
        this.balance = initialBalance;
    }

    private boolean validateWithdrawal(double amount) {
        return amount > 0 && amount <= balance;
    }

    public void withdraw(double amount) {
        if (validateWithdrawal(amount)) {
            balance -= amount;
            System.out.println("Withdrawal Successful: " + amount);
        } else {
            System.out.println("Insufficient balance or invalid amount");
        }
    }

    public double getBalance() {
        return balance;
    }
}

public class Main {
    public static void main(String[] args) {
        Account myAccount = new Account(1000);
        myAccount.withdraw(300);
        System.out.println("Remaining Balance: " + myAccount.getBalance());
    }
}
```

### **輸出：**
```
Withdrawal Successful: 300.0
Remaining Balance: 700.0
```

**為什麼隱藏資料？**
- 防止直接修改重要欄位。
- 透過驗證輸入確保資料完整性。

---

## **真實世界應用中的封裝**

封裝用於許多真實世界的應用程式，例如：
1. **銀行系統** - 確保帳戶詳細資訊是私有的。
2. **醫療保健應用程式** - 保護病患記錄。
3. **電子商務平台** - 隱藏支付處理細節。

### **範例：支付處理中的封裝**

```java
class PaymentProcessor {
    private String cardNumber;
    private double amount;

    public PaymentProcessor(String cardNumber, double amount) {
        this.cardNumber = maskCardNumber(cardNumber);
        this.amount = amount;
    }

    private String maskCardNumber(String cardNumber) {
        return "****-****-****-" + cardNumber.substring(cardNumber.length() - 4);
    }

    public void processPayment() {
        System.out.println("Processing payment of " + amount + " for card " + cardNumber);
    }
}

public class Main {
    public static void main(String[] args) {
        PaymentProcessor payment = new PaymentProcessor("1234567812345678", 250.00);
        payment.processPayment();
    }
}
```

### **輸出：**
```
Processing payment of 250.0 for card ****-****-****-5678
```

**為什麼在支付處理中使用封裝？**
- 保護敏感資料 (例如信用卡號碼)。
- 向使用者隱藏不必要的細節。
- 確保交易安全。
