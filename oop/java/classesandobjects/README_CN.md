# 類別與物件 (Classes and Objects)

類別與物件構成了物件導向程式設計 (OOP) 的基礎。

## 什麼是類別 (Class)？

類別是一個藍圖或模板。它定義了物件的屬性 (欄位) 和行為 (方法)。

### 在 Java 中定義類別

要在 Java 中定義類別，你需要使用 `class` 關鍵字，後面跟著類別名稱。

這是一個簡單的範例：

```java
public class Car {
    // 屬性 (Attributes)
    private String color;
    private String make;
    private String model;
    private int year;

    // 建構子 (Constructor)
    public Car(String color, String make, String model, int year) {
        this.color = color;
        this.make = make;
        this.model = model;
        this.year = year;
    }

    // 顯示汽車詳細資訊的方法
    public void displayInfo() {
        System.out.println("Car Make: " + make);
        System.out.println("Car Model: " + model);
        System.out.println("Car Year: " + year);
        System.out.println("Car Color: " + color);
    }
}
```
- **屬性 (Attributes)**：`Car` 類別有四個描述其狀態的屬性：`color` (顏色)、`make` (製造商)、`model` (型號) 和 `year` (年份)。
- **建構子 (Constructor)**：建構子 `Car(String color, String make, String model, int year)` 初始化類別的新物件。
- **方法 (Methods)**：`displayInfo` 方法負責展示汽車的詳細資訊。

## 什麼是物件 (Object)？

物件是類別的實例 (Instance)。當你建立一個物件時，你將類別的藍圖變為現實。它包含由類別定義的狀態和行為，每個物件都持有自己的一份資料副本。

### 在 Java 中建立物件

要建立物件，你需要使用 `new` 關鍵字，後面跟著類別建構子。

以下是如何從 `Car` 類別實例化物件：

```java
public class Main {
    public static void main(String[] args) {
        // 建立 Car 類別的物件
        Car car1 = new Car("Red", "Toyota", "Corolla", 2020);
        Car car2 = new Car("Blue", "Ford", "Mustang", 2021);

        // 顯示每輛車的資訊
        car1.displayInfo();
        System.out.println("-----------------");
        car2.displayInfo();
    }
}
```

1. **實例化 (Instantiation)**：`new` 關鍵字用於建立物件，並為其分配記憶體。
2. **初始化 (Initialization)**：建構子 (`Car`) 使用給定的參數初始化物件狀態。
3. **參考 (Reference)**：物件透過變數 (`car1`, `car2`) 進行參考，該變數指向其記憶體位置。
