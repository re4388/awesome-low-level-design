# 共乘服務 (LLD)

## 問題陳述

設計並實作一個共乘服務，允許乘客請求乘車，司機接受行程，並由系統管理行程分配、付款和行程狀態。

---

## 需求

- **使用者管理：** 系統管理乘客和司機。
- **位置管理：** 系統追蹤司機和乘客的當前位置。
- **行程請求：** 乘客可以透過指定上車和下車地點來請求乘車。
- **司機分配：** 系統根據距離和可用性將可用的司機分配給乘車請求。
- **行程管理：** 系統追蹤每個行程的狀態 (例如：已請求、進行中、已完成、已取消)。
- **付款處理：** 系統處理已完成行程的付款。
- **司機狀態：** 系統追蹤司機的可用性 (例如：可用、行程中、離線)。
- **可擴展性：** 易於新增功能，例如評分、共乘或動態定價。

---

## 核心實體

- **RideSharingService：** 管理乘客、司機、行程和付款的主要類別。
- **Rider：** 代表可以請求行程的乘客。
- **Driver：** 代表具有當前狀態和位置的司機。
- **Trip：** 代表一次乘車，包括乘客、司機、位置、狀態和付款。
- **Location：** 代表地理位置 (緯度、經度)。
- **TripStatus (列舉)：** REQUESTED, ONGOING, COMPLETED, CANCELLED。
- **DriverStatus (列舉)：** AVAILABLE, ON_TRIP, OFFLINE。
- **Payment (在 payment/ 中)：** 代表行程的付款交易。
- **User：** Rider 和 Driver 的基礎類別 (如果適用)。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/RideSharingService-class-diagram.png)

### 1. RideSharingService
- **欄位：** List<Rider> riders, List<Driver> drivers, List<Trip> trips, PaymentProcessor paymentProcessor
- **方法：** registerRider(Rider), registerDriver(Driver), requestTrip(Rider, Location, Location), assignDriver(Trip), startTrip(Trip), completeTrip(Trip), processPayment(Trip, Payment), updateDriverStatus(Driver, DriverStatus) 等。

### 2. Rider
- **欄位：** int id, String name, Location currentLocation

### 3. Driver
- **欄位：** int id, String name, Location currentLocation, DriverStatus status

### 4. Trip
- **欄位：** int id, Rider rider, Driver driver, Location pickup, Location dropoff, TripStatus status, Payment payment

### 5. Location
- **欄位：** double latitude, double longitude

### 6. TripStatus (列舉)
- 值：REQUESTED, ONGOING, COMPLETED, CANCELLED

### 7. DriverStatus (列舉)
- 值：AVAILABLE, ON_TRIP, OFFLINE

### 8. Payment (在 payment/ 中)
- **欄位：** int id, double amount, String method, PaymentStatus status

### 9. PaymentProcessor (在 payment/ 中)
- **方法：** process(Payment), validate(Payment)

### 10. User
- **欄位：** int id, String name

---

## 範例用法

```java
RideSharingService service = new RideSharingService();
Rider alice = new Rider(1, "Alice", new Location(12.9716, 77.5946));
Driver bob = new Driver(2, "Bob", new Location(12.9718, 77.5940), DriverStatus.AVAILABLE);

service.registerRider(alice);
service.registerDriver(bob);

Trip trip = service.requestTrip(alice, alice.getCurrentLocation(), new Location(12.9352, 77.6245));
service.assignDriver(trip);
service.startTrip(trip);
// ... 行程完成後
Payment payment = new Payment(1, 250.0, "CREDIT_CARD");
service.completeTrip(trip);
service.processPayment(trip, payment);
```

---

## 演示

請參閱 `RideSharingServiceDemo.java` 以獲取共乘服務的範例用法和模擬。

---

## 擴展框架

- **新增評分和評論：** 允許乘客和司機互相評分。
- **新增共乘：** 支援多個乘客共享行程。
- **新增動態定價：** 根據需求和供應調整定價。

---
