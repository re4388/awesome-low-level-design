# Splitwise 系統 (LLD)

## 問題陳述

設計並實作一個 Splitwise 系統，允許使用者在群組和個人之間分攤費用。系統應處理費用追蹤、餘額計算以及使用者之間的債務結算。

---

## 需求

1. **使用者管理：**
   - 建立和管理使用者個人資料
   - 追蹤使用者餘額
   - 處理使用者關係

2. **群組管理：**
   - 建立和管理群組
   - 新增/移除成員
   - 追蹤群組費用

3. **費用管理：**
   - 新增費用到群組或個人
   - 支援不同的分攤類型 (均分、精確、百分比)
   - 追蹤費用歷史記錄

4. **餘額管理：**
   - 計算使用者之間的餘額
   - 追蹤誰欠誰錢
   - 處理結算

5. **交易管理：**
   - 記錄交易
   - 追蹤付款狀態
   - 產生餘額報告

---

## 核心實體

### 1. SplitwiseService
- **欄位：** List<User> users, List<Group> groups, List<Expense> expenses
- **方法：** 
  - addUser()
  - createGroup()
  - addExpense()
  - getBalance()
  - settleExpense()

### 2. User
- **欄位：** String id, String name, String email, Map<User, Double> balances
- **方法：** 
  - updateProfile()
  - getBalance()
  - addBalance()
  - subtractBalance()

### 3. Group
- **欄位：** String id, String name, List<User> members, List<Expense> expenses
- **方法：** 
  - addMember()
  - removeMember()
  - addExpense()
  - getBalances()

### 4. Expense
- **欄位：** String id, String description, double amount, User paidBy, List<User> paidFor, SplitType splitType
- **方法：** 
  - calculateSplits()
  - getAmount()
  - getPaidBy()

### 5. Transaction
- **欄位：** String id, User from, User to, double amount
- **方法：** 
  - execute()
  - getStatus()

### 6. SplitType (列舉)
- **值：** EQUAL, EXACT, PERCENTAGE

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/splitwise-class-diagram.png)

---

## 範例用法

```java
SplitwiseService service = new SplitwiseService();

// 建立使用者
User user1 = service.addUser("John", "john@example.com");
User user2 = service.addUser("Jane", "jane@example.com");

// 建立群組
Group group = service.createGroup("Trip to Paris");
group.addMember(user1);
group.addMember(user2);

// 新增費用
Expense expense = service.addExpense(
    "Dinner", 
    100.0, 
    user1, 
    Arrays.asList(user1, user2), 
    SplitType.EQUAL
);

// 獲取餘額
double balance = service.getBalance(user1, user2);

// 結算費用
service.settleExpense(user2, user1, 50.0);
```

---

## 演示

請參閱 `SplitwiseDemo.java` 以獲取 Splitwise 系統的範例用法和模擬。

---

## 擴展框架

- **新增費用類別：** 對費用進行分類 (食物、旅行等)
- **新增定期費用：** 支援定期付款
- **新增費用評論：** 允許使用者為費用新增備註
- **新增費用附件：** 支援收據和文件
- **新增付款整合：** 與付款閘道整合
- **新增通知系統：** 發送待處理付款的提醒

---

## 使用的設計模式

- **單例模式 (Singleton Pattern)：** 用於 Splitwise 服務實例
- **工廠模式 (Factory Pattern)：** 用於建立不同類型的分攤
- **策略模式 (Strategy Pattern)：** 用於不同的費用分攤策略
- **觀察者模式 (Observer Pattern)：** 用於餘額更新和通知

---

## 異常處理

- **InvalidAmountException：** 當費用金額無效時拋出
- **InvalidSplitException：** 當分攤詳細資訊無效時拋出
- **UserNotFoundException：** 當找不到使用者時拋出
- **GroupNotFoundException：** 當找不到群組時拋出
- **InsufficientBalanceException：** 當使用者餘額不足時拋出

---
