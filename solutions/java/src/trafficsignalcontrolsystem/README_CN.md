# 交通號誌系統 (LLD)

## 問題陳述

設計並實作一個交通號誌系統來管理交叉口的交通燈。系統應支援每個方向和狀態的可配置號誌持續時間，使用狀態設計模式自動循環號誌，並能夠根據需要手動覆蓋號誌。

---

## 需求

- **多個方向：** 交叉口支援多個方向 (例如：北、南、東、西)。
- **交通燈狀態：** 每個方向都有一個交通燈，狀態為：綠燈、黃燈、紅燈。
- **可配置持續時間：** 每個方向和狀態都可以有自己的可配置持續時間。
- **自動循環：** 系統以輪詢方式自動循環每個方向的狀態。
- **手動覆蓋：** 系統允許手動覆蓋以隨時將特定方向設定為綠燈。
- **可擴展性：** 如果需要，易於新增新的方向或狀態。
- **狀態模式：** 使用狀態設計模式來封裝特定於狀態的行為和轉換。

---

## 核心實體

- **Direction：** 代表交叉口方向的列舉 (NORTH, SOUTH, EAST, WEST)。
- **SignalState (介面)：** 代表交通燈的狀態 (GREEN, YELLOW, RED)，具有特定於狀態的行為。
- **GreenState, YellowState, RedState：** 每個燈號狀態的 `SignalState` 具體實作。
- **TrafficLight：** 代表一個方向的交通燈，維護其當前狀態並將行為委派給狀態。
- **Intersection：** 代表交叉口，持有所有交通燈及其配置，並暴露手動覆蓋功能。
- **TrafficSignalController：** 控制交通號誌的循環和覆蓋，使用排程器管理時間和轉換。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/trafficsignalsystem-class-diagram.png)

### 1. Direction
- 列舉：NORTH, SOUTH, EAST, WEST

### 2. SignalState (介面)
- **方法：** `void handle(TrafficLight, TrafficSignalController, Direction)`, `String getName()`

### 3. GreenState, YellowState, RedState
- 實作 `SignalState`
- 每個狀態處理自己的轉換邏輯和持續時間

### 4. TrafficLight
- **欄位：** currentState, direction
- **方法：** setState(SignalState), getState(), getDirection(), handle(TrafficSignalController)

### 5. Intersection
- **欄位：** id, Map<Direction, TrafficLight> signals, Map<Direction, Map<String, Integer>> signalDurations, TrafficSignalController controller
- **方法：** start(Direction), manualOverride(Direction), getSignal(Direction)

### 6. TrafficSignalController
- **欄位：** Map<Direction, TrafficLight> signals, Map<Direction, Map<String, Integer>> signalDurations, scheduler
- **方法：** start(Direction), scheduleStateChange(...), getSignalDuration(...), getNextDirection(...), getTrafficLight(...), manualOverride(Direction)

---

## 使用的設計模式

- **狀態模式 (State Pattern)：** 每個號誌狀態 (GREEN, YELLOW, RED) 封裝其自己的行為和轉換邏輯。
- **排程器/計時器 (Scheduler/Timer)：** 用於處理狀態之間的定時轉換。
- **策略模式 (Strategy Pattern)：** (概念上) 用於支援每個方向/狀態的不同計時策略。

---

## 範例用法

```java
// 配置每個方向和狀態的持續時間
Map<Direction, Map<String, Integer>> signalDurations = new EnumMap<>(Direction.class);
signalDurations.put(Direction.NORTH, Map.of("GREEN", 4, "YELLOW", 2, "RED", 3));
signalDurations.put(Direction.SOUTH, Map.of("GREEN", 3, "YELLOW", 2, "RED", 4));
signalDurations.put(Direction.EAST, Map.of("GREEN", 5, "YELLOW", 2, "RED", 3));
signalDurations.put(Direction.WEST, Map.of("GREEN", 2, "YELLOW", 2, "RED", 5));

// 初始化交通燈
Map<Direction, TrafficLight> signals = new EnumMap<>(Direction.class);
for (Direction direction : Direction.values()) {
    signals.put(direction, new TrafficLight(direction));
}

// 建立並啟動交叉口
Intersection intersection = new Intersection("1", signals, signalDurations);
intersection.start(Direction.NORTH);

// 手動覆蓋範例
intersection.manualOverride(Direction.EAST);
```

---

## 演示

請參閱 `TrafficSignalSystemDemo.java` 以獲取交通號誌系統的範例用法和模擬。

---

## 擴展框架

- **新增新的方向：** 新增至 `Direction` 列舉並更新配置。
- **新增新的狀態：** 新增至 `SignalState` 介面並實作新的狀態類別。
- **自訂計時策略：** 為特殊交叉口或自適應號誌實作新策略。

---
