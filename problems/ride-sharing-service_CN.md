# 設計共乘服務 (Ride-Sharing Service) 類似 Uber

## 需求
1. 共乘服務應允許乘客請求乘車，並允許司機接受和完成這些乘車請求。
2. 乘客應能夠指定他們的上車地點、目的地和所需的乘車類型 (例如：普通、豪華)。
3. 司機應能夠查看可用的乘車請求並選擇接受或拒絕。
4. 系統應根據距離和其他因素將乘車請求與可用的司機進行配對。
5. 系統應根據距離、時間和乘車類型計算每次乘車的費用。
6. 系統應處理付款並處理乘客和司機之間的交易。
7. 系統應提供正在進行的乘車的即時追蹤，並通知乘客和司機有關乘車狀態的更新。
8. 系統應處理並發請求並確保資料一致性。

## UML 類別圖

![](../class-diagrams/ridesharingservice-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/ridesharingservice/) 
#### [Python 實作](../solutions/python/ridesharingservice/)
#### [C++ 實作](../solutions/cpp/ridesharingservice/)
#### [C# 實作](../solutions/csharp/ridesharingservice/)
#### [Go 實作](../solutions/golang/ridesharingservice/)

## 類別、介面和列舉
1. **Passenger** 類別代表共乘服務中的乘客，具有 ID、姓名、聯絡資訊和位置等屬性。
2. **Driver** 類別代表共乘服務中的司機，具有 ID、姓名、聯絡資訊、車牌、位置和狀態 (可用或忙碌) 等屬性。
3. **Ride** 類別代表乘客請求並由司機接受的乘車，具有 ID、乘客、司機、出發地點、目的地點、狀態和費用等屬性。
4. **Location** 類別代表具有緯度和經度座標的地理位置。
5. **Payment** 類別代表為乘車進行的付款，具有 ID、乘車資訊、金額和付款狀態等屬性。
6. **RideService** 類別是管理共乘服務的主要類別。它遵循單例模式 (Singleton pattern)，以確保服務只有一個實例存在。
7. RideService 類別提供新增乘客和司機、請求乘車、接受乘車、開始乘車、完成乘車和取消乘車的方法。
8. 使用並發資料結構 (ConcurrentHashMap 和 ConcurrentLinkedQueue) 實作多執行緒，以處理對共享資料 (如乘車請求和司機可用性) 的並發存取。
9. notifyDrivers、notifyPassenger 和 notifyDriver 方法是用於通知相關方有關乘車狀態更新的佔位符。
10. calculateFare 和 processPayment 方法分別是用於計算乘車費用和處理付款的佔位符。
11. **RideSharingDemo** 類別透過建立乘客和司機、請求乘車、接受乘車、開始乘車、完成乘車和取消乘車來演示共乘服務的使用。
