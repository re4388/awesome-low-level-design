# 設計線上股票經紀系統

## 需求
1. 線上股票經紀系統應允許使用者建立和管理其交易帳戶。
2. 使用者應能夠買賣股票，以及查看其投資組合和交易歷史記錄。
3. 系統應向使用者提供即時股票報價和市場資料。
4. 系統應處理下單、執行和結算流程。
5. 系統應強制執行各種業務規則和驗證，例如檢查帳戶餘額和股票可用性。
6. 系統應處理並發使用者請求並確保資料一致性和完整性。
7. 系統應具有可擴展性，並能夠處理大量的使用者和交易。
8. 系統應安全並保護敏感的使用者資訊。

## UML 類別圖

![](../class-diagrams/onlinestockbrokeragesystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/onlinestockbrokeragesystem/) 
#### [Python 實作](../solutions/python/onlinestockbrokeragesystem/)
#### [C++ 實作](../solutions/cpp/onlinestockbrokeragesystem/)
#### [C# 實作](../solutions/csharp/onlinestockbrokeragesystem/)
#### [Go 實作](../solutions/golang/onlinestockbrokeragesystem/)

## 類別、介面和列舉
1. **User** 類別代表股票經紀系統的使用者，具有使用者 ID、姓名和電子郵件等屬性。
2. **Account** 類別代表使用者的交易帳戶，具有帳戶 ID、關聯使用者和餘額等屬性。它提供存款和提款的方法。
3. **Stock** 類別代表可以交易的股票，具有代碼、名稱和價格等屬性。它提供更新股票價格的方法。
4. **Order** 類別是代表使用者下單的抽象基礎類別。它包含共同屬性，例如訂單 ID、關聯帳戶、股票、數量、價格和訂單狀態。execute() 方法宣告為抽象的，由具體訂單類別實作。
5. **BuyOrder** 和 **SellOrder** 類別是 Order 類別的具體實作，分別代表買入和賣出訂單。它們提供特定於每種訂單類型的 execute() 方法實作。
6. **OrderStatus** 列舉代表訂單的可能狀態，例如 PENDING (待處理)、EXECUTED (已執行) 或 REJECTED (已拒絕)。
7. **Portfolio** 類別代表使用者的投資組合，其中持有使用者擁有的股票。它提供從投資組合中新增和移除股票的方法。
8. **StockBroker** 類別是股票經紀系統的核心組件。它遵循單例模式以確保股票經紀人只有一個實例。它管理使用者帳戶、股票和訂單處理。它提供建立帳戶、新增股票、下單和處理訂單的方法。
9. **InsufficientFundsException** 和 **InsufficientStockException** 類別是自訂例外，分別用於處理資金不足和股票不足的情況。
10. **StockBrokerageSystem** 類別作為應用程式的入口點，並示範股票經紀系統的使用。
