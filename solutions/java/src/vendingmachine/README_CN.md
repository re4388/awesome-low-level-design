# 自動販賣機 (LLD)

## 問題陳述

設計並實作一個自動販賣機系統，允許使用者選擇產品、投入硬幣/紙鈔、分發產品並找零。系統應管理庫存、處理付款，並使用狀態設計模式進行操作。

---

## 需求

- **產品管理：** 系統管理產品目錄，每個產品都有價格和可用數量。
- **庫存管理：** 系統追蹤每個項目的數量，並在缺貨時防止分發。
- **付款處理：** 系統接受硬幣和紙鈔，追蹤總付款，並在必要時找零。
- **狀態管理：** 系統使用狀態設計模式來管理其操作狀態 (閒置、準備就緒、分發、找零)。
- **使用者互動：** 使用者可以選擇產品、投入硬幣/紙鈔，並接收產品和零錢。
- **可擴展性：** 易於新增新的項目類型、付款方式或狀態。

---

## 核心實體

- **VendingMachine：** 管理庫存、狀態轉換、項目選擇和付款的主要類別。
- **Product：** 代表具有名稱和價格的項目。
- **Inventory：** 管理產品庫存。
- **Coin / Note：** 代表接受的付款面額。
- **VendingMachineState (介面)：** 不同機器狀態的介面。
- **IdleState, ReadyState, DispenseState, ReturnChangeState：** 實作 VendingMachineState 的具體狀態。
- **單例模式：** VendingMachine 被實作為單例。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/vendingmachine-class-diagram.png)

### 1. VendingMachine
- **欄位：** Inventory inventory, VendingMachineState idleState, readyState, dispenseState, returnChangeState, currentState, Product selectedProduct, double totalPayment
- **方法：** addProduct(String, double, int), selectProduct(Product), insertCoin(Coin), insertNote(Note), dispenseProduct(), returnChange(), setState(VendingMachineState), getInstance() 等。

### 2. Product
- **欄位：** String name, double price

### 3. Inventory
- **欄位：** Map<Product, Integer> productQuantities
- **方法：** addProduct(Product, int), getQuantity(Product), reduceQuantity(Product), isAvailable(Product)

### 4. Coin / Note
- **欄位：** double value
- **方法：** getValue()

### 5. VendingMachineState (介面)
- **方法：** selectProduct(Product), insertCoin(Coin), insertNote(Note), dispenseProduct(), returnChange()

### 6. IdleState, ReadyState, DispenseState, ReturnChangeState
- **實作：** VendingMachineState
- **行為：** 每個狀態處理允許的操作和轉換。

---

## 範例用法

```java
VendingMachine machine = VendingMachine.getInstance();
Product chips = machine.addProduct("Chips", 1.5, 10);
machine.selectProduct(chips);
machine.insertCoin(new Coin(1.0));
machine.insertCoin(new Coin(0.5));
machine.dispenseProduct();
machine.returnChange();
```

---

## 演示

請參閱您的主要或演示類別以獲取自動販賣機的範例用法和模擬。

---

## 擴展框架

- **新增新的付款方式：** 支援卡片、行動支付等。
- **新增新的狀態：** 維護中、故障等。
- **新增項目類別：** 零食、飲料等。

---

## 使用的設計模式

- **狀態模式 (State Pattern)：** 用於管理機器狀態和轉換。
- **單例模式 (Singleton Pattern)：** 用於確保 VendingMachine 的單一實例。

---
