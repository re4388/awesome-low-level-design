# 線上購物服務 (LLD)

## 問題陳述

設計並實作一個線上購物服務，允許使用者瀏覽產品、將商品新增至購物車、下訂單、付款並追蹤訂單狀態。

---

## 需求

- **使用者管理：** 使用者可以註冊、登入並管理其個人資料。
- **產品目錄：** 系統管理包含詳細資訊和價格的產品目錄。
- **購物車管理：** 使用者可以新增、更新或移除購物車中的產品。
- **下訂單：** 使用者可以為購物車中的產品下訂單。
- **訂單追蹤：** 系統追蹤每個訂單的狀態 (例如：已下單、已出貨、已送達、已取消)。
- **付款處理：** 使用者可以使用不同的付款方式為訂單付款。
- **可擴展性：** 易於新增功能，例如折扣、評論或願望清單。

---

## 核心實體

- **OnlineShoppingService：** 管理使用者、產品、購物車、訂單和付款的主要類別。
- **User：** 代表具有唯一 ID、姓名和購物車的使用者。
- **Product：** 代表具有 ID、名稱、描述和價格的產品。
- **Cart：** 代表使用者的購物車，包含訂單項目。
- **Order：** 代表使用者下的訂單，包括項目、狀態和付款。
- **OrderItem：** 代表訂單或購物車中的項目。
- **OrderStatus：** 訂單狀態的列舉 (PLACED, SHIPPED, DELIVERED, CANCELLED)。
- **Payment (在 payment/ 中)：** 代表訂單的付款交易。
- **PaymentProcessor (在 payment/ 中)：** 處理付款邏輯和驗證。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/OnlineShoppingService-class-diagram.png)

### 1. OnlineShoppingService
- **欄位：** List<User> users, List<Product> products, List<Order> orders, PaymentProcessor paymentProcessor
- **方法：** registerUser(User), addProduct(Product), addToCart(User, Product, int quantity), placeOrder(User), processPayment(Order, Payment), updateOrderStatus(Order, OrderStatus) 等。

### 2. User
- **欄位：** int id, String name, Cart cart

### 3. Product
- **欄位：** int id, String name, String description, double price

### 4. Cart
- **欄位：** List<OrderItem> items
- **方法：** addItem(Product, int quantity), removeItem(Product), updateQuantity(Product, int quantity), getItems()

### 5. Order
- **欄位：** int id, User user, List<OrderItem> items, OrderStatus status, Payment payment

### 6. OrderItem
- **欄位：** Product product, int quantity

### 7. OrderStatus (列舉)
- 值：PLACED, SHIPPED, DELIVERED, CANCELLED

### 8. Payment (在 payment/ 中)
- **欄位：** int id, double amount, String method, PaymentStatus status

### 9. PaymentProcessor (在 payment/ 中)
- **方法：** process(Payment), validate(Payment)

---

## 範例用法

```java
OnlineShoppingService service = new OnlineShoppingService();
User alice = new User(1, "Alice");
Product phone = new Product(1, "Smartphone", "Latest model", 699.0);

service.registerUser(alice);
service.addProduct(phone);
service.addToCart(alice, phone, 1);

Order order = service.placeOrder(alice);
Payment payment = new Payment(1, 699.0, "CREDIT_CARD");
service.processPayment(order, payment);
```

---

## 演示

請參閱 `OnlineShoppingServiceDemo.java` 以獲取線上購物服務的範例用法和模擬。

---

## 擴展框架

- **新增折扣或優惠券：** 支援促銷定價。
- **新增產品評論：** 允許使用者對產品進行評論和評分。
- **新增願望清單：** 允許使用者儲存產品以供日後使用。

---
