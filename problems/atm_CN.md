# 設計 ATM 系統

## 需求
1. ATM 系統應支援基本操作，例如餘額查詢、提款和存款。
2. 使用者應能夠使用卡片和 PIN (個人識別碼) 進行身分驗證。
3. 系統應與銀行的後端系統互動，以驗證使用者帳戶並執行交易。
4. ATM 應具有出鈔機以向使用者發放現金。
5. 系統應處理並發存取並確保資料一致性。
6. ATM 應具有使用者友善的介面供使用者互動。

## UML 類別圖

![](../class-diagrams/atm-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/atm/) 
#### [Python 實作](../solutions/python/atm/)
#### [C++ 實作](../solutions/cpp/atm/)
#### [C# 實作](../solutions/csharp/atm/)
#### [Go 實作](../solutions/golang/atm/)

## 類別、介面和列舉
1. **Card** 類別代表具有卡號和 PIN 的 ATM 卡。
2. **Account** 類別代表具有帳號和餘額的銀行帳戶。它提供扣款和入帳的方法。
3. **Transaction** 類別是不同類型交易 (例如提款和存款) 的抽象基礎類別。它由 WithdrawalTransaction 和 DepositTransaction 類別繼承。
4. **BankingService** 類別管理銀行帳戶並處理交易。它使用執行緒安全的 ConcurrentHashMap 來儲存和檢索帳戶資訊。
5. **CashDispenser** 類別代表 ATM 的出鈔機並處理現金的發放。它使用同步來確保發放現金時的執行緒安全。
6. **ATM** 類別作為 ATM 操作的主要介面。它與 BankingService 和 CashDispenser 互動以執行使用者身分驗證、餘額查詢、提款和存款。
7. **ATMDriver** 類別透過建立範例帳戶並執行 ATM 操作來示範 ATM 系統的使用。
