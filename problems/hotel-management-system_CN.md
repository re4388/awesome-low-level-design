# 設計飯店管理系統

## 需求
1. 飯店管理系統應允許客人預訂房間、辦理入住和退房。
2. 系統應管理不同類型的房間，例如單人房、雙人房、豪華房和套房。
3. 系統應處理房間可用性和預訂狀態。
4. 系統應允許飯店員工管理客人資訊、房間分配和帳單。
5. 系統應支援多種付款方式，例如現金、信用卡和線上支付。
6. 系統應處理並發預訂並確保資料一致性。
7. 系統應為飯店管理提供報告和分析功能。
8. 系統應具有可擴展性，並處理大量的房間和客人。

## UML 類別圖

![](../class-diagrams/hotelmanagementsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/hotelmanagementsystem/) 
#### [Python 實作](../solutions/python/hotelmanagementsystem/)
#### [C++ 實作](../solutions/cpp/hotelmanagementsystem/)
#### [C# 實作](../solutions/csharp/hotelmanagementsystem/)
#### [Go 實作](../solutions/golang/hotelmanagementsystem/)

## 類別、介面和列舉
1. **Guest** 類別代表飯店的客人，具有 ID、姓名、電子郵件和電話號碼等屬性。
2. **Room** 類別代表飯店中的房間，具有 ID、房間類型、價格和狀態等屬性。它提供預訂、入住和退房的方法。
3. **RoomType** 列舉代表飯店中可用的不同類型房間。
4. **RoomStatus** 列舉代表房間的狀態，可以是可用、已預訂或已佔用。
5. **Reservation** 類別代表客人為特定房間和日期範圍所做的預訂。它包含 ID、客人、房間、入住日期、退房日期和狀態等屬性。它提供取消預訂的方法。
6. **ReservationStatus** 列舉代表預訂的狀態，可以是已確認或已取消。
7. **Payment** 介面定義了處理付款的契約。它由具體的付款類別 (如 CashPayment 和 CreditCardPayment) 實作。
8. **HotelManagementSystem** 類別是飯店管理系統的核心組件。它遵循單例模式以確保系統只有一個實例存在。它提供新增客人和房間、預訂房間、取消預訂、入住、退房和處理付款的方法。它還使用同步處理對共享資源的並發存取。
9. **HotelManagementSystemDemo** 類別透過建立客人、房間、預訂房間、入住、退房和取消預訂來示範飯店管理系統的使用。
