# 線上股票經紀系統 (LLD)

## 問題陳述

設計並實作一個線上股票經紀系統，允許使用者買賣股票、管理其投資組合並追蹤其投資。系統應處理訂單處理、帳戶管理和股票交易。

---

## 需求

1. **帳戶管理：**
   - 建立和管理使用者帳戶
   - 追蹤帳戶餘額
   - 處理資金存款和提款

2. **股票管理：**
   - 追蹤可用股票
   - 維護股票價格
   - 處理股票資訊

3. **訂單管理：**
   - 處理買入和賣出訂單
   - 追蹤訂單狀態
   - 處理訂單執行

4. **投資組合管理：**
   - 追蹤使用者的股票持有量
   - 計算投資組合價值
   - 監控投資績效

5. **交易規則：**
   - 驗證訂單金額
   - 檢查資金是否充足
   - 驗證股票可用性

---

## 核心實體

### 1. StockBroker
- **欄位：** List<Account> accounts, List<Stock> stocks, List<Order> orders
- **方法：** 
  - createAccount()
  - placeBuyOrder()
  - placeSellOrder()
  - getPortfolio()
  - getStockPrice()

### 2. Account
- **欄位：** String id, User user, double balance, Portfolio portfolio
- **方法：** 
  - deposit()
  - withdraw()
  - getBalance()
  - getPortfolio()

### 3. User
- **欄位：** String id, String name, String email
- **方法：** 
  - getAccount()
  - updateProfile()

### 4. Stock
- **欄位：** String symbol, String name, double currentPrice
- **方法：** 
  - updatePrice()
  - getPrice()

### 5. Order
- **欄位：** String id, Account account, Stock stock, int quantity, OrderStatus status
- **方法：** 
  - execute()
  - cancel()
  - getStatus()

### 6. BuyOrder
- **欄位：** double price
- **方法：** 
  - validateFunds()
  - execute()

### 7. SellOrder
- **欄位：** double price
- **方法：** 
  - validateStocks()
  - execute()

### 8. Portfolio
- **欄位：** Map<Stock, Integer> holdings
- **方法：** 
  - addStock()
  - removeStock()
  - getValue()

### 9. OrderStatus (列舉)
- **值：** PENDING, EXECUTED, CANCELLED, FAILED

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/onlineStockBrokerageSystem-class-diagram.png)
---

## 範例用法

```java
StockBroker pubSubService = new StockBroker();

// 建立使用者帳戶
User user = new User("John Doe", "john@example.com");
Account account = pubSubService.createAccount(user);

// 存入資金
account.deposit(10000.0);

// 下買入訂單
Stock stock = pubSubService.getStock("AAPL");
BuyOrder buyOrder = pubSubService.placeBuyOrder(account, stock, 10);

// 下賣出訂單
SellOrder sellOrder = pubSubService.placeSellOrder(account, stock, 5);

// 獲取投資組合
Portfolio portfolio = account.getPortfolio();
```

---

## 演示

請參閱 `StockBrokerageSystemDemo.java` 以獲取股票經紀系統的範例用法和模擬。

---

## 擴展框架

- **新增即時市場數據：** 與市場數據提供商整合
- **新增訂單類型：** 支援限價單、止損單
- **新增交易策略：** 實作自動交易策略
- **新增交易歷史記錄：** 追蹤所有交易活動
- **新增報告系統：** 產生投資報告
- **新增通知系統：** 發送價格提醒和訂單更新

---

## 使用的設計模式

- **單例模式 (Singleton Pattern)：** 用於股票經紀服務實例
- **工廠模式 (Factory Pattern)：** 用於建立不同類型的訂單
- **觀察者模式 (Observer Pattern)：** 用於股票價格更新
- **策略模式 (Strategy Pattern)：** 用於不同的訂單執行策略

---

## 異常處理

- **InsufficientFundsException：** 當帳戶資金不足時拋出
- **InsufficientStockException：** 當投資組合股票不足時拋出
- **InvalidOrderException：** 當訂單詳細資訊無效時拋出
- **OrderExecutionException：** 當訂單執行失敗時拋出

---
