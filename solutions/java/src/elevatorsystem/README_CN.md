# 電梯系統 (LLD)

## 問題陳述

設計並實作一個電梯系統，可以處理多個請求、在樓層之間移動，並有效地管理方向和狀態。

---

## 需求

- **多部電梯：** 系統管理多部電梯。
- **請求處理：** 系統可以處理以給定方向 (上/下) 移動到特定樓層的請求。
- **方向管理：** 電梯維護並更新其當前方向 (上、下、閒置)。
- **狀態管理：** 電梯追蹤其當前樓層、方向和待處理的請求。
- **高效移動：** 電梯以高效的順序處理請求 (例如，所有向上請求，然後所有向下請求)。
- **可擴展性：** 易於新增更多電梯或進階排程演算法。

---

## 核心實體

- **Elevator：** 代表電梯，管理其狀態、方向和請求佇列。
- **ElevatorController：** 處理傳入的請求並將其委派給電梯。
- **Request：** 代表以給定方向移動到特定樓層的請求。
- **Direction (列舉)：** UP (上), DOWN (下), IDLE (閒置)。

---

## 類別設計

### 1. Elevator
- **欄位：** currentFloor, direction, List<Request> requests, isMoving 等。
- **方法：** addRequest(Request), move(), openDoor(), closeDoor(), processNextRequest(), getCurrentFloor(), getDirection() 等。

### 2. ElevatorController
- **欄位：** Elevator elevator
- **方法：** requestElevator(int floor, Direction direction), step() 等。

### 3. Request
- **欄位：** int floor, Direction direction

### 4. Direction (列舉)
- 值：UP, DOWN, IDLE

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/elevatorsystem-class-diagram.png)

---

## 範例用法

```java
ElevatorController controller = new ElevatorController();
controller.requestElevator(5, Direction.UP);
controller.requestElevator(2, Direction.DOWN);

// 模擬電梯步驟
for (int i = 0; i < 10; i++) {
    controller.step();
}
```

---

## 演示

請參閱 `ElevatorSystemDemo.java` 以獲取電梯系統的範例用法和模擬。

---

## 擴展框架

- **新增多部電梯：** 建立 `Elevator` 物件列表並更新控制器邏輯。
- **進階排程：** 實作最佳電梯分配演算法。
- **新增功能：** 例如維護模式、緊急停止或樓層顯示。

---
