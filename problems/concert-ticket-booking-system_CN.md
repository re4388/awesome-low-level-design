# 設計演唱會門票預訂系統

## 需求
1. 演唱會門票預訂系統應允許使用者查看可用的演唱會及其座位安排。
2. 使用者應能夠根據各種條件 (例如藝人、場地、日期和時間) 搜尋演唱會。
3. 使用者應能夠選擇座位並購買特定演唱會的門票。
4. 系統應處理並發預訂請求，以避免座位重複預訂。
5. 系統應確保所有使用者有公平的預訂機會。
6. 系統應安全地處理付款處理。
7. 系統應產生預訂確認並透過電子郵件或簡訊發送給使用者。
8. 系統應為已售罄的演唱會提供候補名單功能。

## UML 類別圖

![](../class-diagrams/concertticketbookingsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/concertticketbookingsystem/) 
#### [Python 實作](../solutions/python/concertticketbookingsystem/)
#### [C++ 實作](../solutions/cpp/concertticketbookingsystem/)
#### [C# 實作](../solutions/csharp/concertticketbookingsystem/)
#### [Go 實作](../solutions/golang/concertticketbookingsystem/)

## 類別、介面和列舉
1. **Concert** 類別代表演唱會活動，具有 ID、藝人、場地、日期和時間以及座位列表等屬性。
2. **Seat** 類別代表演唱會中的座位，具有 ID、座位號碼、座位類型、價格和狀態等屬性。它提供預訂和釋放座位的方法。
3. **SeatType** 列舉代表可用的不同類型座位，例如普通、高級和 VIP。
4. **SeatStatus** 列舉代表座位的狀態，可以是可用、已預訂或已保留。
5. **Booking** 類別代表使用者為特定演唱會和座位所做的預訂。它包含 ID、使用者、演唱會、座位、總價格和狀態等屬性。它提供確認和取消預訂的方法。
6. **BookingStatus** 列舉代表預訂的狀態，可以是待處理、已確認或已取消。
7. **User** 類別代表演唱會門票預訂系統的使用者，具有 ID、姓名和電子郵件等屬性。
8. **ConcertTicketBookingSystem** 類別是系統的核心組件。它遵循單例模式以確保系統只有一個實例。它管理演唱會、預訂，並提供新增演唱會、搜尋演唱會、預訂門票和取消預訂的方法。
9. **SeatNotAvailableException** 是一個自訂例外，用於處理座位無法預訂的情況。
