# 設計航空公司管理系統

## 需求

1. 航空公司管理系統應允許使用者根據出發地、目的地和日期搜尋航班。
2. 使用者應能夠預訂航班、選擇座位並進行付款。
3. 系統應管理航班時刻表、飛機分配和機組人員分配。
4. 系統應處理乘客資訊，包括個人詳細資料和行李資訊。
5. 系統應支援不同類型的使用者，例如乘客、航空公司員工和管理員。
6. 系統應能夠處理取消、退款和航班變更。
7. 系統應確保資料一致性並處理對共享資源的並發存取。
8. 系統應具有可擴展性和可延伸性，以適應未來的增強功能和新功能。

## UML 類別圖

![](../class-diagrams/airlinemanagementsystem-class-diagram.png)

## 實作

#### [Java 實作](../solutions/java/src/airlinemanagementsystem/)

#### [Python 實作](../solutions/python/airlinemanagementsystem/)

#### [C++ 實作](../solutions/cpp/airlinemanagementsystem/)

#### [C# 實作](../solutions/csharp/airlinemanagementsystem/)

#### [Go 實作](../solutions/golang/airlinemanagementsystem/)

## 類別、介面和列舉

1. **Flight** 類別代表航空公司管理系統中的航班，具有航班號碼、出發地、目的地、出發時間、到達時間和可用座位等屬性。
2. **Aircraft** 類別代表飛機，具有機尾編號、型號和總座位數等屬性。
3. **Passenger** 類別代表乘客，具有 ID、姓名、電子郵件和電話號碼等屬性。
4. **Booking** 類別代表乘客為特定航班和座位所做的預訂，具有預訂編號、航班、乘客、座位、價格和預訂狀態等屬性。
5. **Seat** 類別代表航班上的座位，具有座位號碼、座位類型和座位狀態等屬性。
6. **Payment** 類別代表為預訂所做的付款，具有付款 ID、付款方式、金額和付款狀態等屬性。
7. **FlightSearch** 類別提供根據出發地、目的地和日期搜尋航班的功能。
8. **BookingManager** 類別管理預訂的建立和取消。它遵循單例模式以確保預訂管理員只有一個實例。
9. **PaymentProcessor** 類別處理付款的處理。它遵循單例模式以確保付款處理器只有一個實例。
10. **AirlineManagementSystem** 類別作為系統的主要入口點，結合所有組件並提供航班管理、預訂、付款處理和其他操作的方法。
