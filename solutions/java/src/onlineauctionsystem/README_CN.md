# 線上拍賣系統 (LLD)

## 問題陳述

設計並實作一個線上拍賣系統，允許使用者建立拍賣、對物品出價、追蹤拍賣狀態並確定獲勝者。

---

## 需求

- **使用者管理：** 使用者可以註冊並參與拍賣。
- **物品管理：** 系統管理可以拍賣的物品。
- **拍賣建立：** 使用者可以為物品建立拍賣，指定開始和結束時間。
- **出價：** 使用者可以對進行中的拍賣出價。
- **拍賣狀態追蹤：** 系統追蹤每個拍賣的狀態 (例如：進行中、已結束)。
- **獲勝者確定：** 當拍賣結束時，系統確定獲勝的出價和使用者。
- **可擴展性：** 易於新增功能，例如保留價格、立即購買選項或通知。

---

## 核心實體

- **AuctionSystem：** 管理使用者、物品、拍賣和出價的主要類別。
- **User：** 代表可以建立拍賣和出價的使用者。
- **Item：** 代表要拍賣的物品。
- **Auction：** 代表物品的拍賣，包括出價、狀態和獲勝者。
- **Bid：** 代表使用者對拍賣的出價。
- **AuctionStatus：** 拍賣狀態的列舉 (ACTIVE, ENDED)。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/onlineauctionsystem-class-diagram.png)

### 1. AuctionSystem
- **欄位：** List<User> users, List<Item> items, List<Auction> auctions
- **方法：** registerUser(User), addItem(Item), createAuction(Item, User, Date startTime, Date endTime), placeBid(Auction, User, double amount), endAuction(Auction), getActiveAuctions(), getEndedAuctions() 等。

### 2. User
- **欄位：** int id, String name

### 3. Item
- **欄位：** int id, String name, String description

### 4. Auction
- **欄位：** int id, Item item, User seller, List<Bid> bids, AuctionStatus status, User winner, Date startTime, Date endTime
- **方法：** addBid(Bid), endAuction(), getHighestBid(), getWinner()

### 5. Bid
- **欄位：** int id, User bidder, double amount, Date bidTime

### 6. AuctionStatus (列舉)
- 值：ACTIVE, ENDED

---

## 範例用法

```java
AuctionSystem system = new AuctionSystem();
User alice = new User(1, "Alice");
User bob = new User(2, "Bob");
system.registerUser(alice);
system.registerUser(bob);

Item painting = new Item(1, "Painting", "Beautiful landscape painting");
system.addItem(painting);

Auction auction = system.createAuction(painting, alice, new Date(), new Date(System.currentTimeMillis() + 3600000));
system.placeBid(auction, bob, 100.0);
system.placeBid(auction, alice, 120.0);

system.endAuction(auction);
User winner = auction.getWinner();
System.out.println("Winner: " + (winner != null ? winner.getName() : "No winner"));
```

---

## 演示

請參閱 `AuctionSystemDemo.java` 以獲取線上拍賣系統的範例用法和模擬。

---

## 擴展框架

- **新增保留價格：** 僅在最高出價達到最低價格時出售。
- **新增立即購買選項：** 允許以設定價格立即購買。
- **新增通知：** 通知使用者有關拍賣事件或出價被超越的資訊。

---
