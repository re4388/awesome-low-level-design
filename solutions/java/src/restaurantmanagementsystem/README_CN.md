# 餐廳管理系統 (LLD)

## 問題陳述

設計並實作一個餐廳管理系統，允許顧客進行預訂、下訂單、管理桌位、產生帳單和處理付款。系統還應支援員工管理和菜單管理。

---

## 需求

- **桌位管理：** 系統管理桌位、其可用性和分配。
- **預訂管理：** 顧客可以提前預訂桌位。
- **菜單管理：** 系統管理菜單項目，包括價格和描述。
- **下訂單：** 顧客可以訂購菜單項目。
- **訂單追蹤：** 系統追蹤每個訂單的狀態 (例如：已下單、準備中、已上菜、已完成)。
- **計費：** 系統為已完成的訂單產生帳單。
- **付款處理：** 系統處理帳單的付款。
- **員工管理：** 系統管理員工分配 (例如：服務生、廚師)。
- **可擴展性：** 易於新增功能，例如顧客回饋、忠誠度計劃或線上訂購。

---

## 核心實體

- **RestaurantManagementSystem：** 管理桌位、預訂、訂單、菜單、員工和付款的主要類別。
- **Table：** 代表餐廳中的桌位，具有桌號、容量和可用性。
- **Reservation：** 代表顧客對桌位的預訂。
- **MenuItem：** 代表菜單上的一個項目，具有名稱、描述和價格。
- **Order：** 代表顧客的訂單，包括項目、狀態和關聯的桌位。
- **OrderItem：** 代表訂單中的一個項目。
- **OrderStatus：** 訂單狀態的列舉 (PLACED, PREPARING, SERVED, COMPLETED)。
- **Bill：** 代表訂單的帳單，包括總金額和付款狀態。
- **Payment (在 payment/ 中)：** 代表帳單的付款交易。
- **Staff：** 代表員工 (例如：服務生、廚師)。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/RestaurantManagementSystem-class-diagram.png)

### 1. RestaurantManagementSystem
- **欄位：** List<Table> tables, List<Reservation> reservations, List<MenuItem> menu, List<Order> orders, List<Bill> bills, List<Staff> staff, PaymentProcessor paymentProcessor
- **方法：** addTable(Table), addMenuItem(MenuItem), makeReservation(Reservation), placeOrder(Order), updateOrderStatus(Order, OrderStatus), generateBill(Order), processPayment(Bill, Payment), addStaff(Staff) 等。

### 2. Table
- **欄位：** int tableNumber, int capacity, boolean isAvailable

### 3. Reservation
- **欄位：** int id, Table table, String customerName, Date reservationTime

### 4. MenuItem
- **欄位：** int id, String name, String description, double price

### 5. Order
- **欄位：** int id, Table table, List<OrderItem> items, OrderStatus status

### 6. OrderItem
- **欄位：** MenuItem menuItem, int quantity

### 7. OrderStatus (列舉)
- 值：PLACED, PREPARING, SERVED, COMPLETED

### 8. Bill
- **欄位：** int id, Order order, double totalAmount, boolean isPaid

### 9. Payment (在 payment/ 中)
- **欄位：** int id, double amount, String method, PaymentStatus status

### 10. Staff
- **欄位：** int id, String name, String role

### 11. PaymentProcessor (在 payment/ 中)
- **方法：** process(Payment), validate(Payment)

---

## 範例用法

```java
RestaurantManagementSystem system = new RestaurantManagementSystem();
Table table = new Table(1, 4, true);
system.addTable(table);

MenuItem pizza = new MenuItem(1, "Pizza", "Cheese Pizza", 12.0);
system.addMenuItem(pizza);

Reservation reservation = new Reservation(1, table, "Alice", new Date());
system.makeReservation(reservation);

Order order = new Order(1, table, List.of(new OrderItem(pizza, 2)), OrderStatus.PLACED);
system.placeOrder(order);

Bill bill = system.generateBill(order);
Payment payment = new Payment(1, bill.getTotalAmount(), "CREDIT_CARD");
system.processPayment(bill, payment);
```

---

## 演示

請參閱 `RestaurantManagementSystemDemo.java` 以獲取餐廳管理系統的範例用法和模擬。

---

## 擴展設計

- **新增顧客回饋：** 允許顧客對他們的體驗進行評分。
- **新增忠誠度計劃：** 追蹤並獎勵回頭客。
- **新增線上訂購：** 支援線上預訂和訂購。

---
