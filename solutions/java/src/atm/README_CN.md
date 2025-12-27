# ATM 系統 (LLD)

## 問題陳述

設計並實作一個 ATM (自動櫃員機) 系統，允許使用者執行基本的銀行操作，如餘額查詢、提款和存款，並具有安全的驗證和適當的現金管理。

---

## 需求

- **使用者驗證：** 使用者必須使用卡片和 PIN 碼進行驗證。
- **餘額查詢：** 使用者可以檢查他們的帳戶餘額。
- **提款：** 如果餘額和現金充足，使用者可以提取現金。
- **存款：** 使用者可以將現金存入他們的帳戶。
- **交易管理：** 系統記錄並處理交易 (提款、存款)。
- **銀行服務整合：** ATM 與後端銀行服務互動以驗證帳戶並執行交易。
- **現金分配器：** ATM 管理自己的現金庫存並安全地分配現金。
- **並發性和一致性：** 系統處理並發存取並確保資料一致性。
- **使用者介面：** ATM 提供使用者友好的操作介面。
- **可擴展性：** 易於新增功能，例如迷你對帳單、資金轉帳或多幣種支援。

---

## 核心實體

- **ATM：** ATM 操作的主要類別；與 `BankingService` 和 `CashDispenser` 互動。
- **Card：** 代表具有卡號和 PIN 碼的 ATM 卡。
- **Account：** 代表具有帳號和餘額的銀行帳戶；支援借記和貸記操作。
- **Transaction (抽象)：** 交易的基礎類別；由 `WithdrawalTransaction` 和 `DepositTransaction` 繼承。
- **WithdrawalTransaction / DepositTransaction：** 用於提款和存款的具體交易類型。
- **BankingService：** 管理銀行帳戶並處理交易；使用執行緒安全的資料結構。
- **CashDispenser：** 管理 ATM 的現金庫存並處理分配；確保執行緒安全。
- **ATMDemo：** 使用範例帳戶和操作演示 ATM 系統的使用。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/atmSystem-class-diagram.png)

### 1. ATM
- **欄位：** BankingService bankService, CashDispenser cashDispenser
- **方法：** authenticateUser(Card), checkBalance(String accountNumber), withdrawCash(String accountNumber, double amount), depositCash(String accountNumber, double amount)

### 2. Card
- **欄位：** String cardNumber, String pin

### 3. Account
- **欄位：** String accountNumber, double balance
- **方法：** debit(double), credit(double), getBalance()

### 4. Transaction (抽象)
- **欄位：** String accountNumber, double amount, Date date
- **方法：** process()

### 5. WithdrawalTransaction / DepositTransaction
- **繼承：** Transaction
- **方法：** process()

### 6. BankingService
- **欄位：** Map<String, Account> accounts
- **方法：** createAccount(String, double), getAccount(String), processTransaction(Transaction)

### 7. CashDispenser
- **欄位：** double cashAvailable
- **方法：** dispenseCash(double), addCash(double), getCashAvailable()

### 8. ATMDemo
- **方法：** run() — 演示範例 ATM 操作

---

## 範例用法

```java
BankingService bankService = new BankingService();
CashDispenser cashDispenser = new CashDispenser(10000);
ATM atmSystem = new ATM(bankService, cashDispenser);

bankService.createAccount("1234567890", 1000.0);
Card card = new Card("1234567890", "1234");
atmSystem.authenticateUser(card);

double balance = atmSystem.checkBalance("1234567890");
atmSystem.withdrawCash("1234567890", 500.0);
atmSystem.depositCash("1234567890", 200.0);
```

---

## 演示

請參閱 `ATMDemo.java` 以獲取 ATM 系統的範例用法和模擬。

---

## 擴展框架

- **新增迷你對帳單：** 顯示最近的交易。
- **新增資金轉帳：** 允許帳戶之間的轉帳。
- **新增多幣種支援：** 處理不同的貨幣和轉換。

---
