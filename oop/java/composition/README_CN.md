# Java 中的組合 (Composition)

## 簡介

組合是物件導向程式設計 (OOP) 的基本原則之一。它允許使用其他物件來構建物件，促進程式碼重用、靈活性和更好的可維護性。與建立「is-a」(是一個) 關係的繼承不同，組合代表「has-a」(擁有) 關係。

## 什麼是組合？

組合是 OOP 中的一種設計原則，其中一個類別包含另一個類別的實例 (或多個實例) 作為欄位。被包含的類別通常稱為組件 (component)，而包含的類別稱為複合類別 (composite class)。這有助於透過組合更簡單的物件來構建複雜的系統。

### 範例：汽車及其組件

考慮一輛 `Car` (汽車)，它由多個組件組成，如 `Engine` (引擎)、`Wheel` (車輪) 和 `Transmission` (變速箱)。`Car` 物件不是繼承這些組件，而是將它們作為欄位包含在內。

```java
class Engine {
    private int horsepower;

    public Engine(int horsepower) {
        this.horsepower = horsepower;
    }

    public void start() {
        System.out.println("Engine started with " + horsepower + " HP.");
    }
}

class Wheel {
    private String type;

    public Wheel(String type) {
        this.type = type;
    }

    public void rotate() {
        System.out.println("The " + type + " wheel is rotating.");
    }
}

class Transmission {
    private String type;

    public Transmission(String type) {
        this.type = type;
    }

    public void shiftGear() {
        System.out.println("Transmission shifted: " + type);
    }
}

class Car {
    private Engine engine;
    private Wheel wheel;
    private Transmission transmission;

    public Car(Engine engine, Wheel wheel, Transmission transmission) {
        this.engine = engine;
        this.wheel = wheel;
        this.transmission = transmission;
    }

    public void drive() {
        engine.start();
        wheel.rotate();
        transmission.shiftGear();
        System.out.println("Car is moving!");
    }
}

public class CompositionExample {
    public static void main(String[] args) {        
        Car car = new Car(new Engine(150), new Wheel("Alloy"), new Transmission("Automatic"));
        car.drive();
    }
}
```

### 輸出：
```
Engine started with 150 HP.
The Alloy wheel is rotating.
Transmission shifted: Automatic
Car is moving!
```

---

## 為什麼優先選擇組合而不是繼承？

### 1. **封裝與靈活性**
   - 組合允許我們透過在執行時替換組件來動態改變物件的行為。
   - 繼承使得在不破壞現有程式碼的情況下修改現有類別階層變得困難。

### 2. **更好的程式碼重用性**
   - 組合促進可重用的組件。`Engine`、`Wheel` 和 `Transmission` 類別可以用於多種類型的車輛 (汽車、自行車、卡車)，而無需修改。

### 3. **避免繼承陷阱**
   - 繼承可能導致深層的類別階層，使維護變得困難。
   - 它強制執行嚴格的父子關係，這對於某些設計來說可能過於僵化。

### 4. **支援基於介面的設計**
   - 組合可以與介面結合使用，以實現強大的解耦。

---

## 使用介面的組合

將介面與組合一起使用可以實現更大的靈活性和鬆散耦合。

```java
interface Engine {
    void start();
}

class PetrolEngine implements Engine {
    public void start() {
        System.out.println("Petrol Engine started.");
    }
}

class DieselEngine implements Engine {
    public void start() {
        System.out.println("Diesel Engine started.");
    }
}

class Car {
    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }

    public void startCar() {
        engine.start();
        System.out.println("Car is ready to go!");
    }
}

public class InterfaceCompositionExample {
    public static void main(String[] args) {
        Car petrolCar = new Car(new PetrolEngine());
        petrolCar.startCar();
        
        Car dieselCar = new Car(new DieselEngine());
        dieselCar.startCar();
    }
}
```

### 輸出：
```
Petrol Engine started.
Car is ready to go!
Diesel Engine started.
Car is ready to go!
```

---

## 何時使用組合？

- 當構建由多個組件組成的複雜物件時。
- 當你想要實現**程式碼重用性**而不需要僵化的繼承階層時。
- 當需要動態交換不同的行為時 (例如，在車輛中使用不同類型的引擎)。
- 當遵循**優先使用組合而非繼承**原則時。
