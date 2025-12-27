# 演唱會門票預訂系統 (LLD)

## 問題陳述

設計並實作一個演唱會門票預訂系統，允許使用者預訂演唱會座位。系統應管理演唱會詳細資訊、座位可用性，並透過適當的驗證處理預訂。

---

## 需求

- **演唱會管理：** 系統管理演唱會詳細資訊，包括名稱、日期、場地和可用座位。
- **座位管理：** 系統追蹤不同類型的座位 (VIP、標準、經濟) 及其可用性。
- **預訂管理：** 使用者可以預訂座位，系統處理預訂狀態 (已確認、已取消)。
- **使用者管理：** 系統維護預訂的使用者資訊。
- **驗證：** 系統防止重複預訂並處理座位可用性檢查。

---

## 核心實體

- **ConcertTicketBookingSystem：** 管理演唱會、預訂和座位分配的主要類別。
- **Concert：** 代表一場演唱會及其詳細資訊和座位管理。
- **Seat：** 代表一個座位及其類型、狀態和預訂資訊。
- **User：** 代表可以預訂門票的使用者。
- **Booking：** 代表一個預訂及其狀態和相關詳細資訊。
- **SeatType：** 不同座位類別的列舉 (VIP、STANDARD、ECONOMY)。
- **SeatStatus：** 座位狀態的列舉 (AVAILABLE、BOOKED)。
- **BookingStatus：** 預訂狀態的列舉 (CONFIRMED、CANCELLED)。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/concertticketbookingsystem-class-diagram.png)

### 1. ConcertTicketBookingSystem
- **欄位：** List<Concert> concerts, List<Booking> bookings
- **方法：** addConcert(), bookSeat(), cancelBooking(), getAvailableSeats() 等。

### 2. Concert
- **欄位：** String name, String date, String venue, List<Seat> seats
- **方法：** addSeat(), getAvailableSeats(), bookSeat() 等。

### 3. Seat
- **欄位：** String seatNumber, SeatType type, SeatStatus status, Booking booking
- **方法：** isAvailable(), book(), cancel() 等。

### 4. User
- **欄位：** String name, String email

### 5. Booking
- **欄位：** String bookingId, User user, Concert concert, Seat seat, BookingStatus status
- **方法：** confirm(), cancel() 等。

### 6. 列舉
- **SeatType：** VIP, STANDARD, ECONOMY
- **SeatStatus：** AVAILABLE, BOOKED
- **BookingStatus：** CONFIRMED, CANCELLED

---

## 範例用法

```java
ConcertTicketBookingSystem system = new ConcertTicketBookingSystem();

// 新增演唱會
Concert concert = system.addConcert("Rock Concert", "2024-12-31", "Stadium");

// 預訂座位
User user = new User("John Doe", "john@example.com");
Booking booking = system.bookSeat(concert, "A1", user);

// 取消預訂
system.cancelBooking(booking);
```

---

## 演示

請參閱 `ConcertTicketBookingSystemDemo.java` 以獲取預訂系統的範例用法和模擬。

---

## 擴展框架

- **新增付款處理：** 整合付款閘道以購買門票
- **新增候補名單功能：** 當座位訂滿時處理候補名單
- **新增折扣管理：** 支援不同的定價層級和折扣
- **新增通知系統：** 發送預訂確認和更新

---

## 使用的設計模式

- **單例模式 (Singleton Pattern)：** 用於管理預訂系統實例
- **工廠模式 (Factory Pattern)：** 用於建立不同類型的座位
- **觀察者模式 (Observer Pattern)：** 用於通知使用者有關預訂狀態的變更

---
