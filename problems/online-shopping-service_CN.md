# 設計像 Amazon 這樣的線上購物系統

## 需求
1. 線上購物服務應允許使用者瀏覽產品、將其新增至購物車並下訂單。
2. 系統應支援多種產品類別並提供搜尋功能。
3. 使用者應能夠管理其個人檔案、查看訂單歷史記錄並追蹤訂單狀態。
4. 系統應處理庫存管理並相應地更新產品可用性。
5. 系統應支援多種付款方式並確保交易安全。
6. 系統應處理並發使用者請求並確保資料一致性。
7. 系統應具有可擴展性，以處理大量的產品和使用者。
8. 系統應提供使用者友善的介面，以實現無縫的購物體驗。

## UML 類別圖

![](../class-diagrams/onlineshoppingservice-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/onlineshoppingservice/)
#### [Python 實作](../solutions/python/onlineshoppingservice/)
#### [C++ 實作](../solutions/cpp/onlineshoppingservice/)
#### [C# 實作](../solutions/csharp/onlineshoppingservice/)
#### [Go 實作](../solutions/golang/onlineshoppingservice/)

## 類別、介面和列舉
1. **User** 類別代表線上購物服務中的使用者，具有 ID、姓名、電子郵件、密碼和訂單列表等屬性。
2. **Product** 類別代表可供購買的產品，具有 ID、名稱、描述、價格和數量等屬性。它提供更新數量和檢查產品可用性的方法。
3. **Order** 類別代表使用者下的訂單，包含 ID、使用者、訂單項目、總金額和訂單狀態等屬性。它根據訂單項目計算總金額。
4. **OrderItem** 類別代表訂單中的項目，由產品和訂購數量組成。
5. **OrderStatus** 列舉代表訂單可能具有的不同狀態，例如待處理、處理中、已發貨、已送達或已取消。
6. **ShoppingCart** 類別代表使用者的購物車，允許他們新增、移除和更新項目數量。它維護產品 ID 和訂單項目的對應關係。
7. **Payment** 介面定義了處理付款的契約，並具有具體實作 CreditCardPayment。
8. **OnlineShoppingService** 類別是線上購物服務的核心組件。它遵循單例模式以確保服務只有一個實例存在。它提供註冊使用者、新增產品、搜尋產品、下訂單和檢索訂單資訊的方法。它使用同步處理對共享資源的並發存取。
9. **OnlineShoppingServiceDemo** 類別透過註冊使用者、新增產品、搜尋產品、下訂單和查看訂單歷史記錄來示範線上購物服務的使用。
