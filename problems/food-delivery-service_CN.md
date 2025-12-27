# 設計像 Swiggy 這樣的線上食品外送服務

## 需求
1. 食品外送服務應允許客戶瀏覽餐廳、查看菜單並下訂單。
2. 餐廳應能夠管理其菜單、價格和可用性。
3. 外送員應能夠接受並完成訂單。
4. 系統應處理訂單追蹤和狀態更新。
5. 系統應支援多種付款方式。
6. 系統應處理並發訂單並確保資料一致性。
7. 系統應具有可擴展性並處理大量訂單。
8. 系統應向客戶、餐廳和外送員提供即時通知。

## UML 類別圖

![](../class-diagrams/fooddeliveryservice-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/fooddeliveryservice/) 
#### [Python 實作](../solutions/python/fooddeliveryservice/)
#### [C++ 實作](../solutions/cpp/fooddeliveryservice/)
#### [C# 實作](../solutions/csharp/fooddeliveryservice/)
#### [Go 實作](../solutions/golang/fooddeliveryservice/)

## 類別、介面和列舉
1. **Customer** 類別代表可以下訂單的客戶。它包含客戶詳細資訊，例如 ID、姓名、電子郵件和電話號碼。
2. **Restaurant** 類別代表提供菜單項目的餐廳。它包含餐廳詳細資訊，例如 ID、名稱、地址和菜單項目列表。它提供新增和移除菜單項目的方法。
3. **MenuItem** 類別代表餐廳菜單上的項目。它包含詳細資訊，例如 ID、名稱、描述、價格和可用狀態。
4. **Order** 類別代表客戶下的訂單。它包含訂單詳細資訊，例如 ID、客戶、餐廳、訂單項目列表、狀態和分配的外送員。它提供新增和移除訂單項目、更新訂單狀態和分配外送員的方法。
5. **OrderItem** 類別代表訂單中的項目。它包含選定的菜單項目和訂購數量。
6. **OrderStatus** 列舉代表訂單可能具有的不同狀態，例如 PENDING (待處理)、CONFIRMED (已確認)、PREPARING (準備中)、OUT_FOR_DELIVERY (外送中)、DELIVERED (已送達) 和 CANCELLED (已取消)。
7. **DeliveryAgent** 類別代表完成訂單的外送員。它包含詳細資訊，例如 ID、姓名、電話號碼和可用狀態。
8. **FoodDeliveryService** 類別是管理食品外送服務的主要類別。它遵循單例模式以確保服務只有一個實例存在。它提供註冊客戶、餐廳和外送員、檢索可用餐廳和菜單、下訂單、更新訂單狀態、取消訂單以及將外送員分配給訂單的方法。它還處理向客戶、餐廳和外送員發送通知。
