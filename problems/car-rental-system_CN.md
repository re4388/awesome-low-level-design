# 設計租車系統

## 需求
1. 租車系統應允許客戶瀏覽並預訂特定日期的可用車輛。
2. 每輛車應有詳細資訊，例如製造商、型號、年份、車牌號碼和每日租金。
3. 客戶應能夠根據各種條件搜尋車輛，例如車輛類型、價格範圍和可用性。
4. 系統應處理預訂，包括建立、修改和取消預訂。
5. 系統應追蹤車輛的可用性並相應地更新其狀態。
6. 系統應處理客戶資訊，包括姓名、聯絡方式和駕照資訊。
7. 系統應處理預訂的付款處理。
8. 系統應能夠處理並發預訂並確保資料一致性。

## UML 類別圖

![](../class-diagrams/carrentalsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/carrentalsystem/) 
#### [Python 實作](../solutions/python/carrentalsystem/)
#### [C++ 實作](../solutions/cpp/carrentalsystem/)
#### [C# 實作](../solutions/csharp/carrentalsystem/)
#### [Go 實作](../solutions/golang/carrentalsystem/)

## 類別、介面和列舉
1. **Car** 類別代表租賃系統中的車輛，具有製造商、型號、年份、車牌號碼、每日租金和可用狀態等屬性。
2. **Customer** 類別代表客戶，具有姓名、聯絡資訊和駕照號碼等屬性。
3. **Reservation** 類別代表客戶為特定車輛和日期範圍所做的預訂。它包括預訂 ID、客戶、車輛、開始日期、結束日期和總價格等屬性。
4. **PaymentProcessor** 介面定義了付款處理的契約，而 CreditCardPaymentProcessor 和 PayPalPaymentProcessor 類別是付款處理器的具體實作。
5. **RentalSystem** 類別是租車系統的核心，並遵循單例模式以確保租賃系統只有一個實例。
6. RentalSystem 類別使用並發資料結構 (ConcurrentHashMap) 來處理對車輛和預訂的並發存取。
7. **RentalSystem** 類別提供新增和移除車輛、根據條件搜尋可用車輛、進行預訂、取消預訂和處理付款的方法。
8. **CarRentalSystem** 類別作為應用程式的入口點，並示範租車系統的使用。
