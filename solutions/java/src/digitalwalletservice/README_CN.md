# 數位錢包服務 (LLD)

## 問題陳述

設計並實作一個數位錢包服務，允許使用者管理他們的數位貨幣、進行交易並連結多種付款方式。系統應處理貨幣轉換、追蹤交易並管理不同類型的帳戶。

---

## 需求

1. **帳戶管理：**
   - 建立和管理使用者帳戶
   - 支援多種付款方式 (銀行帳戶、信用卡)
   - 處理帳戶餘額和交易

2. **交易管理：**
   - 處理轉帳
   - 追蹤交易歷史記錄
   - 處理交易狀態和類型

3. **付款方式：**
   - 支援銀行帳戶整合
   - 支援信用卡整合
   - 允許新增/移除付款方式

4. **貨幣支援：**
   - 處理多種貨幣
   - 提供貨幣轉換
   - 維護匯率

5. **安全和驗證：**
   - 驗證交易
   - 處理資金不足
   - 確保資料一致性

---

## 核心實體

### 1. DigitalWallet
- **欄位：** String id, User user, double balance, List<PaymentMethod> paymentMethods, List<Transaction> transactions
- **方法：** addMoney(), sendMoney(), getBalance(), addPaymentMethod(), removePaymentMethod()

### 2. User
- **欄位：** String id, String name, String email, String phoneNumber
- **方法：** updateProfile(), getWallet()

### 3. Account
- **欄位：** String id, User user, double balance, Currency currency
- **方法：** deposit(), withdraw(), getBalance()

### 4. PaymentMethod
- **欄位：** String id, User user, PaymentMethodType type
- **方法：** validate(), processPayment()

### 5. BankAccount
- **欄位：** String accountNumber, String bankName, String ifscCode
- **方法：** transfer(), validate()

### 6. CreditCard
- **欄位：** String cardNumber, String expiryDate, String cvv
- **方法：** charge(), validate()

### 7. Transaction
- **欄位：** String id, Account from, Account to, double amount, Currency currency, TransactionStatus status
- **方法：** process(), cancel(), getStatus()

### 8. Currency
- **欄位：** String code, String symbol
- **方法：** getExchangeRate()

### 9. CurrencyConverter
- **方法：** convert(double amount, Currency from, Currency to)

---

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/digitalwalletservice-class-diagram.png)

## 範例用法

```java
// 建立新使用者
User user = new User("John Doe", "john@example.com", "1234567890");

// 建立數位錢包
DigitalWallet wallet = new DigitalWallet(user);

// 新增銀行帳戶
BankAccount bankAccount = new BankAccount("1234567890", "HDFC Bank", "HDFC0001234");
wallet.addPaymentMethod(bankAccount);

// 新增資金到錢包
wallet.addMoney(1000.0, Currency.USD);

// 轉帳給另一位使用者
User recipient = new User("Jane Doe", "jane@example.com", "9876543210");
wallet.sendMoney(recipient.getWallet(), 500.0, Currency.USD);
```

---

## 演示

請參閱 `DigitalWalletDemo.java` 以獲取數位錢包系統的範例用法和模擬。

---

## 擴展框架

- **新增驗證：** 實作使用者驗證和授權
- **新增交易限制：** 設定並強制執行交易限制
- **新增獎勵系統：** 實作現金回饋和獎勵
- **新增帳單支付：** 支援公用事業帳單支付
- **新增投資選項：** 支援投資各種工具
- **新增通知系統：** 發送交易提醒和更新

---

## 使用的設計模式

- **工廠模式 (Factory Pattern)：** 用於建立不同類型的付款方式
- **策略模式 (Strategy Pattern)：** 用於不同的付款處理策略
- **觀察者模式 (Observer Pattern)：** 用於交易通知
- **單例模式 (Singleton Pattern)：** 用於貨幣轉換服務

---

## 異常處理

- **InsufficientFundsException：** 當交易資金不足時拋出
- **InvalidPaymentMethodException：** 當付款方式驗證失敗時拋出
- **TransactionFailedException：** 當交易處理失敗時拋出

---
