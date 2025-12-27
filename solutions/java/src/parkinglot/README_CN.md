# 停車場系統 (LLD)

## 問題陳述

設計並實作一個停車場管理系統，支援車輛的停車和取車、票券產生、費用計算，以及多樓層和車位類型的管理。

---

## 需求

- **多樓層：** 停車場可以有多個樓層。
- **停車位：** 每個樓層有多個不同類型的停車位 (例如：汽車、機車、卡車)。
- **車輛類型：** 支援不同的車輛類型 (參見 `vehicletype/`)。
- **票務：** 當車輛停放時產生票券。
- **取車：** 允許車輛取車並計算停車費。
- **費用計算：** 支援不同的費用策略 (參見 `fee/`)。
- **車位分配：** 分配正確類型的最近可用車位。
- **可擴展性：** 易於新增新的車輛類型、車位類型或費用策略。

---

## 核心實體

- **ParkingLot：** 管理整個停車場、樓層和整體運作的主要類別。
- **ParkingFloor：** 代表停車場中的單一樓層，管理其車位。
- **ParkingSpot：** 代表單個停車位，知道其類型和佔用情況。
- **Ticket：** 代表車輛停放時發行的停車票券。
- **VehicleType (在 `vehicletype/` 中)：** 不同車輛類型的列舉或類別。
- **費用計算 (在 `fee/` 中)：** 根據持續時間和車輛類型計算停車費的類別。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/parkinglot-class-diagram.png)

### 1. ParkingLot
- **方法：**
  - `parkVehicle(Vehicle vehicle)`
  - `unparkVehicle(String ticketId)`
  - `addFloor(ParkingFloor floor)`
  - `getAvailableSpots()`
- **欄位：** 樓層列表、票券映射等。

### 2. ParkingFloor
- **方法：**
  - `getAvailableSpot(VehicleType type)`
  - `parkVehicle(Vehicle vehicle)`
  - `unparkVehicle(String spotId)`
- **欄位：** 車位列表、樓層編號。

### 3. ParkingSpot
- **方法：**
  - `isAvailable()`
  - `assignVehicle(Vehicle vehicle)`
  - `removeVehicle()`
- **欄位：** 車位 ID、類型、當前車輛。

### 4. Ticket
- **欄位：** 票券 ID、車輛資訊、進入時間、車位資訊。

### 5. VehicleType (在 `vehicletype/` 中)
- 車輛類型的列舉或類別 (汽車、機車、卡車等)

### 6. 費用計算 (在 `fee/` 中)
- **方法：** `calculateFee(Ticket parkingTicket, Date exitTime)`
- **可擴展：** 新增費用計算的新策略。

---

## 使用的設計模式

- **策略模式 (Strategy Pattern)：** 用於費用計算策略。
- **工廠模式 (Factory Pattern)：** (如果使用) 用於建立車輛或車位。
- **單例模式 (Singleton Pattern)：** (如果使用) 用於 ParkingLot 實例。

---

## 範例用法

```java
ParkingLot lot = new ParkingLot();
lot.addFloor(new ParkingFloor(...));
Ticket parkingTicket = lot.parkVehicle(new Car("KA-01-1234"));
lot.unparkVehicle(parkingTicket.getId());
```

---

## 演示

請參閱 `ParkingLotDemo.java` 以獲取停車場系統的範例用法。

---

## 擴展框架

- **新增新的車輛類型：** 更新或新增至 `vehicletype/`。
- **新增新的費用策略：** 在 `fee/` 中實作新類別。
- **新增新的車位類型或樓層：** 擴展 `ParkingSpot` 或 `ParkingFloor`。

---
