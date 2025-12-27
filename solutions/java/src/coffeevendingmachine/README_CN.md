# 咖啡自動販賣機 (LLD)

## 問題陳述

設計並實作一個咖啡自動販賣機系統，可以提供不同類型的咖啡，管理食材庫存，處理付款，並處理使用者互動，例如選擇咖啡和補充食材。

---

## 需求

- **多種咖啡類型：** 機器應支援多種咖啡配方 (例如：濃縮咖啡、拿鐵、卡布奇諾)。
- **食材管理：** 機器應追蹤和管理食材存量，並在食材不足時防止分發。
- **付款處理：** 機器應在分發咖啡前處理付款。
- **補充食材：** 機器應允許補充食材。
- **可擴展性：** 易於新增新的咖啡類型或付款方式。

---

## 核心實體

- **CoffeeVendingMachine：** 管理整體運作、使用者互動並協調其他組件的主要類別。
- **CoffeeRecipe：** 代表咖啡配方，包括所需的食材及其數量。
- **IngredientStore：** 管理食材庫存，支援檢查和補充。
- **Dispenser：** 在成功付款和檢查食材後處理咖啡的分發。
- **PaymentProcessor：** 處理付款邏輯和驗證。
- **Payment：** 代表付款交易。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/coffeevendingmachine-class-diagram.png)

### 1. CoffeeVendingMachine
- **欄位：** ingredientStore, paymentProcessor, Map<String, CoffeeRecipe> recipes, Dispenser
- **方法：** selectCoffee(String), makeCoffee(String, Payment), refillIngredient(String, int), addRecipe(CoffeeRecipe) 等。

### 2. CoffeeRecipe
- **欄位：** name, Map<String, Integer> ingredients
- **方法：** getName(), getIngredients()

### 3. IngredientStore
- **欄位：** Map<String, Integer> ingredientLevels
- **方法：** hasIngredients(Map<String, Integer>), useIngredients(Map<String, Integer>), refill(String, int), getLevel(String)

### 4. Dispenser
- **方法：** dispense(String)

### 5. PaymentProcessor
- **方法：** processPayment(Payment)

### 6. Payment
- **欄位：** amount, paymentType 等。

---

## 使用的設計模式

- **策略模式 (Strategy Pattern)：** (概念上) 用於支援不同的付款方式或咖啡配方。
- **關注點分離 (Separation of Concerns)：** 每個類別都有單一職責 (庫存、付款、分發等)。

---

## 範例用法

```java
CoffeeVendingMachine machine = new CoffeeVendingMachine();
machine.addRecipe(new CoffeeRecipe("Espresso", Map.of("CoffeeBeans", 10, "Water", 30)));
machine.refillIngredient("CoffeeBeans", 100);
machine.refillIngredient("Water", 200);

Payment payment = new Payment(50, "CASH");
machine.makeCoffee("Espresso", payment);
```

---

## 演示

請參閱 `CoffeeVendingMachineDemo.java` 以獲取咖啡自動販賣機的範例用法和模擬。

---

## 擴展框架

- **新增新的咖啡類型：** 建立新的 `CoffeeRecipe` 實例並將其新增至機器。
- **新增新的付款方式：** 擴展 `PaymentProcessor` 以支援新的付款類型。
- **新增新的食材：** 根據需要更新 `IngredientStore` 和配方。

---
