# 發布/訂閱系統 (LLD)

## 問題陳述

設計並實作一個發布-訂閱 (Pub/Sub) 系統，允許發布者向主題發送訊息，而訂閱者可以從他們感興趣的主題接收訊息。系統應支援多個主題、每個主題多個訂閱者以及非同步訊息傳遞。

---

## 需求

- **主題：** 系統支援多個主題。
- **發布者：** 發布者可以向任何主題發布訊息。
- **訂閱者：** 訂閱者可以訂閱一個或多個主題並接收發布到這些主題的訊息。
- **多個訂閱者：** 每個主題可以有多個訂閱者。
- **非同步傳遞：** 訊息以非同步方式傳遞給訂閱者。
- **取消訂閱：** 訂閱者可以取消訂閱主題。
- **可擴展性：** 易於新增新的訂閱者類型或訊息處理邏輯。

---

## 核心實體

- **Broker：** 管理主題、訂閱和訊息傳遞。
- **Topic：** 代表一個主題，訊息可以發布到該主題，訂閱者可以訂閱該主題。
- **Publisher：** 透過 pubSubService 向主題發布訊息。
- **Subscriber (介面)：** 所有訂閱者的介面，定義了 `consume(Message)` 方法。
- **PrintSubscriber：** 一個將接收到的訊息列印到控制台的訂閱者。
- **LoggingSubscriber：** 一個記錄接收到的訊息的訂閱者。
- **Message：** 代表具有有效負載的訊息。
- **Dispatcher：** 處理訊息向訂閱者的非同步傳遞。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/pubsubsystem-class-diagram.png)

### 1. Broker
- **欄位：** Map<String, Topic> topics
- **方法：** createTopic(String), subscribe(String, Subscriber), unsubscribe(String, Subscriber), publish(String, Message)

### 2. Topic
- **欄位：** String name, List<Subscriber> subscribers
- **方法：** addSubscriber(Subscriber), removeSubscriber(Subscriber), publish(Message)

### 3. Publisher
- **欄位：** String name, Broker pubSubService
- **方法：** publish(String topic, String payload)

### 4. Subscriber (介面)
- **方法：** consume(Message)

### 5. PrintSubscriber
- **實作：** Subscriber
- **行為：** 將接收到的訊息列印到控制台

### 6. LoggingSubscriber
- **實作：** Subscriber
- **行為：** 記錄接收到的訊息 (列印帶有日誌前綴的訊息)

### 7. Message
- **欄位：** String payload
- **方法：** getPayload()

### 8. Dispatcher
- **方法：** dispatch(Subscriber, Message), shutdown()

---

## 使用的設計模式

- **觀察者模式 (Observer Pattern)：** Pub/Sub 系統是觀察者模式的具體實作。主題 (主體) 維護訂閱者 (觀察者) 列表，並在發布新訊息時非同步通知他們。
## 範例用法

```java
Broker pubSubService = new Broker();
pubSubService.createTopic("topic1");
pubSubService.createTopic("topic2");

Publisher publisher1 = new Publisher("publisher1", pubSubService);
Subscriber subscriber1 = new PrintSubscriber("PrintSubscriber1");
Subscriber subscriber2 = new LoggingSubscriber("LoggingSubscriber2");

pubSubService.subscribe("topic1", subscriber1);
pubSubService.subscribe("topic2", subscriber2);

publisher1.publish("topic1", "Hello Topic1!");
publisher1.publish("topic2", "Hello Topic2!");
```

---

## 演示

請參閱 `PubSubSystemDemo.java` 以獲取 pub/sub 系統的範例用法和模擬。

---

## 擴展設計

- **新增新的訂閱者類型：** 實作 `Subscriber` 介面以進行自訂處理。
- **新增新的訊息類型：** 擴展 `Message` 類別以獲得更豐富的有效負載。
- **新增過濾或轉換：** 增強 pubSubService 或主題以支援訊息過濾或轉換。

---
