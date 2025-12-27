# 餐飲外送服務 (LLD)

## 問題陳述

設計並實作一個餐飲外送服務系統，允許顧客從餐廳下訂單，管理菜單項目，分配外送員，並追蹤訂單從下單到送達的狀態。

---

## 需求

- **顧客註冊：** 顧客可以註冊並下訂單。
- **餐廳管理：** 系統管理多間餐廳，每間餐廳都有自己的菜單。
- **菜單管理：** 餐廳可以新增和更新菜單項目。
- **下訂單：** 顧客可以從餐廳訂購菜單項目。
- **訂單追蹤：** 系統追蹤每個訂單的狀態 (例如：已下單、準備中、外送中、已送達)。
- **外送分配：** 訂單被分配給可用的外送員。
- **外送員管理：** 系統管理外送員及其可用性。
- **可擴展性：** 易於新增功能，例如評分、評論或付款整合。

---

## 核心實體

- **FoodDeliveryService：** 管理顧客、餐廳、訂單和外送員的主要類別。
- **Customer：** 代表可以下訂單的顧客。
- **Restaurant：** 代表擁有菜單項目的餐廳。
- **MenuItem：** 代表餐廳菜單上的一個項目。
- **Order：** 代表顧客的訂單，包括項目、狀態和分配的外送員。
- **DeliveryAgent：** 代表負責運送訂單的外送員。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/fooddeliveryservice-class-diagram.png)

### 1. FoodDeliveryService
- **欄位：** List<Customer> customers, List<Restaurant> restaurants, List<DeliveryAgent> agents, List<Order> orders
- **方法：** registerCustomer(Customer), addRestaurant(Restaurant), addMenuItem(Restaurant, MenuItem), placeOrder(Customer, Restaurant, List<MenuItem>), assignDeliveryAgent(Order), updateOrderStatus(Order, Status) 等。

### 2. Customer
- **欄位：** int id, String name, List<Order> orders

### 3. Restaurant
- **欄位：** int id, String name, List<MenuItem> menu

### 4. MenuItem
- **欄位：** int id, String name, double price

### 5. Order
- **欄位：** int id, Customer customer, Restaurant restaurantManagementSystem, List<MenuItem> items, OrderStatus status, DeliveryAgent agent

### 6. DeliveryAgent
- **欄位：** int id, String name, boolean available, List<Order> assignedOrders

---

## 範例用法

```java
FoodDeliveryService service = new FoodDeliveryService();
Customer alice = new Customer(1, "Alice");
Restaurant pizzaPlace = new Restaurant(1, "Pizza Place");
MenuItem pizza = new MenuItem(1, "Margherita Pizza", 10.0);

service.registerCustomer(alice);
service.addRestaurant(pizzaPlace);
service.addMenuItem(pizzaPlace, pizza);

service.placeOrder(alice, pizzaPlace, List.of(pizza));
```

---

## 演示

請參閱 `FoodDeliveryServiceDemo.java` 以獲取餐飲外送服務的範例用法和模擬。

---

## 擴展框架

- **新增評分和評論：** 允許顧客對餐廳和外送員進行評分。
- **新增付款整合：** 支援線上付款。
- **新增訂單取消或修改：** 允許顧客在送達前取消或修改訂單。

---
