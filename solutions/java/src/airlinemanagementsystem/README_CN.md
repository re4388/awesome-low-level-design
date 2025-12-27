# 航空公司管理系統 (LLD)

## 問題陳述

設計並實作一個航空公司管理系統，允許使用者預訂航班、管理乘客、處理座位分配、處理付款以及追蹤預訂和航班。

---

## 需求

- **航班管理：** 系統管理航班，每個航班都有唯一的航班號碼、飛機、出發地、目的地和時間表。
- **飛機管理：** 每個航班都與一架飛機相關聯，飛機具有型號和一組座位。
- **座位管理：** 系統管理每個航班的座位分配和可用性。
- **乘客管理：** 可以新增、更新乘客並將其與預訂相關聯。
- **預訂管理：** 使用者可以預訂航班，系統追蹤預訂、分配的座位和乘客。
- **付款處理：** 系統處理預訂的付款。
- **可擴展性：** 易於新增功能，例如忠誠度計劃、餐點選擇或多段旅程。

---

## 核心實體

- **AirlineManagementSystem：** 管理航班、預訂、乘客和付款的主要類別。
- **Flight：** 代表一個航班，包含航班號碼、飛機、出發地、目的地、時間表和座位。
- **Aircraft：** 代表一架飛機，包含型號和一組座位。
- **Seat：** 代表飛機上的一個座位，包含座位號碼、艙等和可用性。
- **Passenger：** 代表一位使用者，包含 ID、姓名和聯絡方式。
- **Booking：** 代表一個預訂，包含使用者、航班、座位和付款。
- **Payment (在 payment/ 中)：** 代表預訂的付款交易。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/airlinemanagementsystem-class-diagram.png)

### 1. AirlineManagementSystem

- **欄位：** List<Flight> flights, List<Booking> bookings, List<Passenger> passengers, PaymentProcessor paymentProcessor
- **方法：** addFlight(Flight), addPassenger(Passenger), bookFlight(Passenger, Flight, Seat, Payment), getAvailableSeats(Flight), getBookings(Passenger) 等。

### 2. Flight (在 flight/ 中)

- **欄位：** String flightNumber, Aircraft aircraft, String source, String destination, Date schedule, List<Seat> seats

### 3. Aircraft

- **欄位：** String model, List<Seat> seats

### 4. Seat (在 seat/ 中)

- **欄位：** String seatNumber, String seatClass, boolean isAvailable

### 5. Passenger

- **欄位：** int id, String name, String contactInfo

### 6. Booking (在 booking/ 中)

- **欄位：** int id, Passenger user, Flight flight, List<Seat> seats, Payment payment

### 7. Payment (在 payment/ 中)

- **欄位：** int id, double amount, String method, PaymentStatus status

### 8. PaymentProcessor (在 payment/ 中)

- **方法：** process(Payment), validate(Payment)

---

## 範例用法

```java
AirlineManagementSystem system = new AirlineManagementSystem();
Aircraft aircraft = new Aircraft("Boeing 737", seatList);
Flight flight = new Flight("AI101", aircraft, "DEL", "BOM", new Date(), seatList);
system.addFlight(flight);

Passenger alice = new Passenger(1, "Alice", "alice@email.com");
system.addPassenger(alice);

Seat seat = flight.getAvailableSeats().get(0);
Payment payment = new Payment(1, 5000.0, "CREDIT_CARD");
system.bookFlight(alice, flight, seat, payment);
```

---

## 演示

請參閱 `AirlineManagementSystemDemo.java` 以獲取航空公司管理系統的範例用法和模擬。

---

## 擴展框架

- **新增忠誠度計劃：** 追蹤常客積分和獎勵。
- **新增餐點選擇：** 允許乘客在預訂時選擇餐點。
- **新增多段旅程：** 支援包含多個轉機航班的預訂。

---
