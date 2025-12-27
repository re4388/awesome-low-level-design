# 物件導向程式設計 (OOP) 中的繼承 (Inheritance)

## 簡介

**繼承 (Inheritance)** 是物件導向程式設計 (OOP) 的核心原則之一。它允許一個類別 (子類別或衍生類別) 獲取另一個類別 (父類別或基礎類別) 的屬性和行為。這促進了**程式碼重用**、**可擴展性**和**可維護性**。

## **什麼是繼承？**

**繼承**是一種機制，子類別從父類別衍生屬性和行為。子類別可以：

- 使用父類別的欄位和方法
- 覆寫 (Override) 父類別方法以提供特定實作
- 增加自己額外的屬性和方法

### **繼承的主要好處**

- **程式碼重用性**：透過重用父類別的欄位和方法來避免程式碼重複。
- **提高可維護性**：減少冗餘，使程式碼更易於管理。
- **增強可擴展性**：可以輕鬆添加新功能，而無需修改現有程式碼。

---

## **如何在 Java 中實作繼承**

### **步驟 1：建立父類別**

父類別包含共同的欄位和方法。

```java
// 父類別
public class Animal {
    String name;

    void eat() {
        System.out.println(name + " is eating...");
    }
}
```

### **步驟 2：使用 `extends` 建立子類別**

子類別繼承父類別的屬性和方法。

```java
// 子類別
public class Dog extends Animal {
    void bark() {
        System.out.println(name + " is barking...");
    }
}
```

### **步驟 3：使用子類別**

現在，讓我們建立一個物件並使用繼承的方法。

```java
public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.name = "Buddy";
        myDog.eat(); // 繼承自 Animal 類別
        myDog.bark(); // 定義在 Dog 類別
    }
}
```

### **輸出：**

```
Buddy is eating...
Buddy is barking...
```

---

## **Java 中的繼承類型**

Java 支援不同類型的繼承：

### **1. 單一繼承 (Single Inheritance)**

一個子類別繼承自一個父類別。

```java
class Parent {
    void show() {
        System.out.println("This is the parent class");
    }
}

class Child extends Parent {
    void display() {
        System.out.println("This is the child class");
    }
}
```

### **2. 多層繼承 (Multilevel Inheritance)**

一個子類別繼承自另一個子類別，形成一個鏈。

```java
class Grandparent {
    void show() {
        System.out.println("Grandparent class");
    }
}

class Parent extends Grandparent {
    void display() {
        System.out.println("Parent class");
    }
}

class Child extends Parent {
    void print() {
        System.out.println("Child class");
    }
}
```

### **3. 階層繼承 (Hierarchical Inheritance)**

一個父類別有多個子類別。

```java
class Parent {
    void show() {
        System.out.println("Parent class");
    }
}

class Child1 extends Parent {
    void display() {
        System.out.println("Child1 class");
    }
}

class Child2 extends Parent {
    void print() {
        System.out.println("Child2 class");
    }
}
```

**注意：** 由於歧義問題，Java **不支援多重繼承** (即一個子類別繼承自多個父類別)。

---

## **繼承中的方法覆寫 (Method Overriding)**

方法覆寫允許子類別**重新定義**父類別的方法。

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
```

### **用法**

```java
public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Dog(); // 多型
        myAnimal.makeSound();
    }
}
```

### **輸出：**

```
Dog barks
```

---

## **繼承中的 `super` 關鍵字**

`super` 關鍵字用於**參考父類別**。它有助於：

1. 呼叫父類別建構子。
2. 存取父類別方法。
3. 存取父類別欄位。

```java
class Animal {
    Animal() {
        System.out.println("Animal Constructor");
    }
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    Dog() {
        super(); // 呼叫父類別建構子
        System.out.println("Dog Constructor");
    }
    void makeSound() {
        super.makeSound(); // 呼叫父類別方法
        System.out.println("Dog barks");
    }
}
```

### **用法**

```java
public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.makeSound();
    }
}
```

### **輸出：**

```
Animal Constructor
Dog Constructor
Animal makes a sound
Dog barks
```
