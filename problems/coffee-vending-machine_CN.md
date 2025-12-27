# 設計咖啡販賣機

## 需求
1. 咖啡販賣機應支援不同類型的咖啡，例如濃縮咖啡、卡布奇諾和拿鐵。
2. 每種類型的咖啡應有特定的價格和配方 (成分及其數量)。
3. 機器應有一個選單來顯示可用的咖啡選項及其價格。
4. 使用者應能夠選擇咖啡類型並進行付款。
5. 機器應分發選定的咖啡並在必要時找零。
6. 機器應追蹤成分的庫存並在庫存不足時發出通知。
7. 機器應並發處理多個使用者請求並確保執行緒安全。

## UML 類別圖

![](../class-diagrams/coffeevendingmachine-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/coffeevendingmachine/) 
#### [Python 實作](../solutions/python/coffeevendingmachine/)
#### [C++ 實作](../solutions/cpp/coffeevendingmachine/)
#### [C# 實作](../solutions/csharp/coffeevendingmachine/)
#### [Go 實作](../solutions/golang/coffeevendingmachine/)
#### [TypeScript 實作](../solutions/typescript/src/CoffeeVendingMachine/)

## 類別、介面和列舉
1. **Coffee** 類別代表一種咖啡類型，具有名稱、價格和配方 (成分及其數量)。
2. **Ingredient** 類別代表製作咖啡所使用的成分，具有名稱和數量。它提供一個同步方法來更新數量。
3. **Payment** 類別代表使用者所做的付款，具有支付金額。
4. **CoffeeMachine** 類別是管理咖啡販賣機的主要類別。它遵循單例模式以確保機器只有一個實例。
5. **CoffeeMachine** 類別在其建構子中初始化咖啡選單和成分。它提供顯示選單、選擇咖啡、分發咖啡和更新成分數量的方法。
6. hasEnoughIngredients 方法檢查是否有足夠的成分來製作選定的咖啡，而 updateIngredients 方法在分發咖啡後更新成分數量。
7. **CoffeeVendingMachine** 類別是應用程式的入口點，並示範咖啡販賣機的使用。它建立機器的實例，顯示選單，並使用 ExecutorService 模擬並發使用者請求。
