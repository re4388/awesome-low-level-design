# 設計餐廳管理系統 (Restaurant Management System)

## 需求
1. 餐廳管理系統應允許顧客下訂單、查看菜單和進行預訂。
2. 系統應管理餐廳的庫存，包括食材和菜單項目。
3. 系統應處理訂單處理，包括訂單準備、計費和付款。
4. 系統應支援多種付款方式，例如現金、信用卡和行動支付。
5. 系統應管理員工資訊，包括職位、排班和績效追蹤。
6. 系統應為管理層產生報告和分析，例如銷售報告和庫存分析。
7. 系統應處理並發存取並確保資料一致性。

## UML 類別圖

![](../class-diagrams/restaurantmanagementsystem-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/restaurantmanagementsystem/) 
#### [Python 實作](../solutions/python/restaurantmanagementsystem/)
#### [C++ 實作](../solutions/cpp/restaurantmanagementsystem/)
#### [C# 實作](../solutions/csharp/restaurantmanagementsystem/)
#### [Go 實作](../solutions/golang/restaurantmanagementsystem/)

## 類別、介面和列舉
1. **MenuItem** 類別代表餐廳中的菜單項目，具有 ID、名稱、描述、價格和供應情況等屬性。
2. **Order** 類別代表顧客下的訂單，具有 ID、菜單項目列表、總金額、訂單狀態和時間戳記等屬性。
3. **OrderStatus** 列舉代表訂單可能具有的不同狀態，例如待處理、準備中、準備就緒、已完成或已取消。
4. **Reservation** 類別代表顧客進行的預訂，具有 ID、顧客姓名、聯絡電話、人數和預訂時間等屬性。
5. **Payment** 類別代表為訂單進行的付款，具有 ID、金額、付款方式和付款狀態等屬性。
6. **PaymentMethod** 列舉代表餐廳支援的不同付款方式，例如現金、信用卡或行動支付。
7. **PaymentStatus** 列舉代表付款的狀態，可以是待處理、已完成或失敗。
8. **Staff** 類別代表餐廳的員工，具有 ID、姓名、職位和聯絡電話等屬性。
9. **Restaurant** 類別是管理餐廳營運的主要類別。它遵循單例模式 (Singleton pattern)，以確保餐廳只有一個實例存在。
10. Restaurant 類別提供管理菜單項目、下訂單、更新訂單狀態、進行預訂、處理付款和管理員工的方法。
11. 使用並發資料結構 (ConcurrentHashMap 和 CopyOnWriteArrayList) 實作多執行緒，以處理對共享資料 (如訂單和預訂) 的並發存取。
12. notifyKitchen 和 notifyStaff 方法是用於通知相關員工有關訂單更新和狀態變更的佔位符。
13. **RestaurantManagementDemo** 類別透過新增菜單項目、下訂單、進行預訂、處理付款、更新訂單狀態、新增員工和檢索菜單來演示餐廳管理系統的使用。
