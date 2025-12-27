# 設計數位錢包服務

## 需求
1. 數位錢包應允許使用者建立帳戶並管理其個人資訊。
2. 使用者應能夠新增和移除付款方式，例如信用卡或銀行帳戶。
3. 數位錢包應支援使用者之間以及向外部帳戶的資金轉帳。
4. 系統應處理交易歷史記錄並提供交易對帳單。
5. 數位錢包應支援多種貨幣並執行貨幣轉換。
6. 系統應確保使用者資訊和交易的安全。
7. 數位錢包應處理並發交易並確保資料一致性。
8. 系統應具有可擴展性，以處理大量的使用者和交易。

## UML 類別圖

![](../class-diagrams/digitalwalletservice-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/digitalwalletservice/) 
#### [Python 實作](../solutions/python/digitalwalletservice/)
#### [C++ 實作](../solutions/cpp/digitalwalletservice/)
#### [C# 實作](../solutions/csharp/digitalwalletservice/)
#### [Go 實作](../solutions/golang/digitalwalletservice/)

## 類別、介面和列舉
1. **User** 類別代表數位錢包的使用者，具有 ID、姓名、電子郵件、密碼和帳戶列表等屬性。
2. **Account** 類別代表使用者在數位錢包中的帳戶，具有 ID、使用者、帳號、貨幣、餘額和交易列表等屬性。它提供存款和提款的方法。
3. **Transaction** 類別代表兩個帳戶之間的金融交易，包含 ID、來源帳戶、目的地帳戶、金額、貨幣和時間戳記等屬性。
4. **PaymentMethod** 類別是不同付款方式 (例如信用卡和銀行帳戶) 的抽象基礎類別。它定義了處理付款的共同屬性和方法。
5. **CreditCard** 和 **BankAccount** 類別是 PaymentMethod 類別的具體實作，代表特定的付款方式。
6. **Currency** 列舉代表數位錢包支援的不同貨幣。
7. **CurrencyConverter** 類別提供一個靜態方法，根據預定義的匯率在不同貨幣之間轉換金額。
8. **DigitalWallet** 類別是數位錢包系統的核心組件。它遵循單例模式以確保數位錢包只有一個實例存在。它提供建立使用者、帳戶、新增付款方式、轉帳資金和檢索交易歷史記錄的方法。它使用同步處理對共享資源的並發存取。
9. **DigitalWalletDemo** 類別透過建立使用者、帳戶、新增付款方式、存入資金、轉帳資金和檢索交易歷史記錄來示範數位錢包系統的使用。
