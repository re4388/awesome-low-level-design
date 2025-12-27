# 電影票預訂系統 (LLD)

## 問題陳述

設計並實作一個電影票預訂系統，允許使用者預訂電影票、選擇座位並管理場次。系統應處理電影時間表、戲院管理和座位預訂。

---

## 需求

1. **電影管理：**
   - 儲存電影資訊 (標題、時長、語言)
   - 管理電影時間表和場次
   - 追蹤電影可用性

2. **戲院管理：**
   - 管理戲院資訊
   - 處理每間戲院的多個場次
   - 追蹤戲院容量

3. **場次管理：**
   - 安排電影場次
   - 管理場次時間
   - 處理場次可用性

4. **座位管理：**
   - 追蹤座位可用性
   - 處理座位選擇
   - 管理不同的座位類型

5. **預訂管理：**
   - 處理電影票預訂
   - 處理預訂取消
   - 管理預訂狀態

---

## 核心實體

### 1. MovieTicketBookingSystem
- **欄位：** List<Movie> movies, List<Theater> theaters, List<Show> shows
- **方法：** 
  - addMovie()
  - addTheater()
  - addShow()
  - bookTicket()
  - cancelBooking()
  - getAvailableShows()

### 2. Movie
- **欄位：** String id, String title, int duration, String language
- **方法：** 
  - getShows()
  - isAvailable()

### 3. Theater
- **欄位：** String id, String name, String location
- **方法：** 
  - addShow()
  - getShows()
  - getCapacity()

### 4. Show
- **欄位：** String id, Movie movie, Theater theater, Date showTime, List<Seat> seats
- **方法：** 
  - getAvailableSeats()
  - bookSeat()
  - cancelSeat()

### 5. User
- **欄位：** String id, String name, String email
- **方法：** 
  - getBookings()
  - updateProfile()

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/MovieTicketBookingSystem-class-diagram.png)
---

## 範例用法

```java
MovieTicketBookingSystem system = new MovieTicketBookingSystem();

// 新增電影
Movie movie = system.addMovie("Inception", 150, "English");

// 新增戲院
Theater theater = system.addTheater("Cineplex", "Downtown");

// 新增場次
Show show = system.addShow(movie, theater, showTime);

// 預訂電影票
User user = new User("John Doe", "john@example.com");
Booking booking = system.bookTicket(user, show, seats);
```

---

## 演示

請參閱 `MovieTicketBookingDemo.java` 以獲取電影票預訂系統的範例用法和模擬。

---

## 擴展框架

- **新增付款處理：** 整合付款閘道以購買電影票
- **新增座位選擇 UI：** 實作互動式座位選擇介面
- **新增定價層級：** 支援不同座位類型的不同定價
- **新增場次排程：** 實作進階場次排程演算法
- **新增通知系統：** 發送預訂確認和提醒
- **新增使用者評論：** 允許使用者對電影進行評分和評論

---

## 使用的設計模式

- **單例模式 (Singleton Pattern)：** 用於預訂系統實例
- **工廠模式 (Factory Pattern)：** 用於建立不同類型的座位
- **觀察者模式 (Observer Pattern)：** 用於座位可用性更新
- **策略模式 (Strategy Pattern)：** 用於不同的定價策略

---

## 異常處理

- **SeatNotAvailableException：** 當嘗試預訂不可用的座位時拋出
- **InvalidShowException：** 當場次詳細資訊無效時拋出
- **BookingFailedException：** 當預訂流程失敗時拋出
- **CancellationFailedException：** 當取消流程失敗時拋出

---
