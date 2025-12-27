# 設計像 BookMyShow 這樣的電影票預訂系統

## 需求
1. 系統應允許使用者查看不同電影院正在上映的電影列表。
2. 使用者應能夠選擇電影、電影院和放映時間來預訂門票。
3. 系統應顯示所選場次的座位安排，並允許使用者選擇座位。
4. 使用者應能夠進行付款並確認其預訂。
5. 系統應處理並發預訂並確保即時更新座位可用性。
6. 系統應支援不同類型的座位 (例如普通、高級) 和定價。
7. 系統應允許電影院管理員新增、更新和移除電影、場次和座位安排。
8. 系統應具有可擴展性，以處理大量並發使用者和預訂。

## UML 類別圖

![](../class-diagrams/movieticketbookingsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/movieticketbookingsystem/) 
#### [Python 實作](../solutions/python/movieticketbookingsystem/)
#### [C++ 實作](../solutions/cpp/movieticketbookingsystem/)
#### [C# 實作](../solutions/csharp/movieticketbookingsystem/)
#### [Go 實作](../solutions/golang/movieticketbookingsystem/)

## 類別、介面和列舉
1. **Movie** 類別代表電影，具有 ID、標題、描述和持續時間等屬性。
2. **Theater** 類別代表電影院，具有 ID、名稱、地點和場次列表等屬性。
3. **Show** 類別代表電影院中的電影場次，具有 ID、電影、電影院、開始時間、結束時間和座位圖等屬性。
4. **Seat** 類別代表場次中的座位，具有 ID、排、列、類型、價格和狀態等屬性。
5. **SeatType** 列舉定義了不同類型的座位 (普通或高級)。
6. **SeatStatus** 列舉定義了座位的不同狀態 (可用或已預訂)。
7. **Booking** 類別代表使用者所做的預訂，具有 ID、使用者、場次、選定座位、總價格和狀態等屬性。
8. **BookingStatus** 列舉定義了預訂的不同狀態 (待處理、已確認或已取消)。
9. **User** 類別代表預訂系統的使用者，具有 ID、姓名和電子郵件等屬性。
10. **MovieTicketBookingSystem** 類別是管理電影票預訂系統的主要類別。它遵循單例模式以確保系統只有一個實例存在。
11. MovieTicketBookingSystem 類別提供新增電影、電影院和場次，以及預訂門票、確認預訂和取消預訂的方法。
12. 多執行緒是使用並發資料結構 (例如 ConcurrentHashMap) 實現的，以處理對共享資源 (例如場次和預訂) 的並發存取。
13. **MovieTicketBookingDemo** 類別透過新增電影、電影院、場次、預訂門票以及確認或取消預訂來示範電影票預訂系統的使用。
