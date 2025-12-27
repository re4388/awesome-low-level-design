# 設計自動販賣機 (Vending Machine)

## 需求
1. 自動販賣機應支援多種不同價格和數量的產品。
2. 機器應接受不同面額的硬幣和紙鈔。
3. 機器應分發選定的產品，並在必要時找零。
4. 機器應追蹤可用產品及其數量。
5. 機器應並發處理多個交易並確保資料一致性。
6. 機器應提供補貨和收款的介面。
7. 機器應處理異常情況，例如資金不足或產品缺貨。

## UML 類別圖

![](../class-diagrams/vendingmachine-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/vendingmachine/) 
#### [Python 實作](../solutions/python/vendingmachine/)
#### [C++ 實作](../solutions/cpp/vendingmachine/)
#### [C# 實作](../solutions/csharp/vendingmachine/)
#### [Go 實作](../solutions/golang/vending_machine/)
#### [TypeScript 實作](../solutions/typescript/src/VendingMachine/)

## 類別、介面和列舉
1. **Product** 類別代表自動販賣機中的產品，具有名稱和價格等屬性。
2. **Coin** 和 **Note** 列舉代表自動販賣機接受的不同面額的硬幣和紙鈔。
3. **Inventory** 類別管理自動販賣機中可用的產品及其數量。它使用並發雜湊映射 (concurrent hash map) 來確保執行緒安全。
4. **VendingMachineState** 介面定義了自動販賣機在不同狀態下的行為，例如閒置、準備就緒和分發。
5. **IdleState**、**ReadyState** 和 **DispenseState** 類別實作了 VendingMachineState 介面，並定義了每個狀態的特定行為。
6. **VendingMachine** 類別是代表自動販賣機的主要類別。它遵循單例模式 (Singleton pattern)，以確保自動販賣機只有一個實例存在。
7. VendingMachine 類別維護當前狀態、選定的產品、總付款，並提供狀態轉換和付款處理的方法。
8. **VendingMachineDemo** 類別透過將產品新增至庫存、選擇產品、投入硬幣和紙鈔、分發產品和找零來演示自動販賣機的使用。
