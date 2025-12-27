# 飯店管理系統 (LLD)

## 問題陳述

設計並實作一個飯店管理系統，用於管理飯店房間、預訂和房客資訊。系統應處理房間預訂、入住、退房，並維護房間狀態。

---

## 需求

1. **房間管理：**
   - 追蹤不同類型的房間 (標準、豪華、套房)
   - 管理房間可用性和狀態
   - 處理房間定價和功能

2. **預訂管理：**
   - 建立和管理預訂
   - 處理入住和退房流程
   - 追蹤預訂狀態 (已確認、已取消、已入住、已退房)

3. **房客管理：**
   - 儲存房客資訊
   - 追蹤房客歷史記錄
   - 處理房客偏好

4. **房間狀態追蹤：**
   - 監控房間可用性 (可用、已佔用、維護中)
   - 根據預訂更新房間狀態
   - 處理房間維護請求

5. **付款整合：**
   - 處理房間付款
   - 處理不同的付款方式
   - 產生發票

---

## 核心實體

### 1. HotelManagementSystem
- **欄位：** List<Room> rooms, List<Reservation> reservations, List<Guest> guests
- **方法：** 
  - addRoom()
  - makeReservation()
  - checkIn()
  - checkOut()
  - getAvailableRooms()
  - cancelReservation()

### 2. Room
- **欄位：** String roomNumber, RoomType type, double price, RoomStatus status
- **方法：** 
  - isAvailable()
  - updateStatus()
  - getPrice()

### 3. Guest
- **欄位：** String id, String name, String email, String phoneNumber
- **方法：** 
  - updateProfile()
  - getReservations()

### 4. Reservation
- **欄位：** String id, Guest guest, Room room, Date checkInDate, Date checkOutDate, ReservationStatus status
- **方法：** 
  - confirm()
  - cancel()
  - checkIn()
  - checkOut()

### 5. RoomType (列舉)
- **值：** STANDARD, DELUXE, SUITE

### 6. RoomStatus (列舉)
- **值：** AVAILABLE, OCCUPIED, MAINTENANCE

### 7. ReservationStatus (列舉)
- **值：** CONFIRMED, CANCELLED, CHECKED_IN, CHECKED_OUT

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/HotelManagementSystem-class-diagram.png)

---

## 範例用法

```java
HotelManagementSystem system = new HotelManagementSystem();

// 新增房間
Room room = system.addRoom("101", RoomType.DELUXE, 150.0);

// 建立房客
Guest guest = new Guest("John Doe", "john@example.com", "1234567890");

// 進行預訂
Reservation reservation = system.makeReservation(guest, room, checkInDate, checkOutDate);

// 入住
system.checkIn(reservation);

// 退房
system.checkOut(reservation);
```

---

## 演示

請參閱 `HotelManagementSystemDemo.java` 以獲取飯店管理系統的範例用法和模擬。

---

## 擴展框架

- **新增客房服務：** 追蹤客房服務請求和交付
- **新增家政服務：** 管理家政排程和任務
- **新增忠誠度計劃：** 實作房客忠誠度積分和獎勵
- **新增庫存管理：** 追蹤飯店用品和設施
- **新增報告系統：** 產生入住率和收入報告
- **新增通知系統：** 發送預訂確認和提醒

---

## 使用的設計模式

- **單例模式 (Singleton Pattern)：** 用於飯店管理系統實例
- **工廠模式 (Factory Pattern)：** 用於建立不同類型的房間
- **觀察者模式 (Observer Pattern)：** 用於房間狀態更新和通知
- **策略模式 (Strategy Pattern)：** 用於不同的定價策略

---

## 異常處理

- **RoomNotAvailableException：** 當嘗試預訂不可用的房間時拋出
- **InvalidReservationException：** 當預訂詳細資訊無效時拋出
- **CheckInException：** 當入住流程失敗時拋出
- **CheckOutException：** 當退房流程失敗時拋出

---
