# 日誌框架 (LLD)

## 問題陳述

設計並實作一個靈活且可擴展的日誌框架，供應用程式用於記錄不同層級 (INFO、DEBUG、ERROR 等) 的訊息，支援多種輸出目的地 (控制台、檔案等)，並允許自訂日誌訊息格式。

---

## 需求

- **日誌層級：** 支援多種日誌層級 (INFO、DEBUG、ERROR 等)。
- **多個 Appender：** 能夠記錄到不同的目的地 (控制台、檔案等)。
- **自訂格式化：** 支援自訂日誌訊息格式化。
- **配置：** 能夠配置記錄器和 Appender。
- **執行緒安全：** 應為並發日誌記錄提供執行緒安全。
- **可擴展性：** 易於新增新的日誌層級、Appender 或格式化器。

---

## 核心實體

- **Logger：** 客戶端用於記錄訊息的主要類別。
- **LogLevel：** 代表不同日誌層級的列舉。
- **LogMessage：** 封裝日誌事件的詳細資訊。
- **LogFormatter：** 用於格式化日誌訊息的介面。
- **DefaultFormatter：** `LogFormatter` 的預設實作。
- **LoggerConfig：** 保存記錄器的配置 (Appender、格式化器等)。
- **LogAppender (在 `logappender/` 中)：** 輸出目的地的介面和實作 (例如：ConsoleAppender、FileAppender)。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/loggingframework-class-diagram.png)

### 1. Logger
- **方法：**
  - `log(LogLevel level, String message)`
  - `info(String message)`
  - `debug(String message)`
  - `error(String message)`
  - `setConfig(LoggerConfig config)`

### 2. LogLevel
- 日誌層級的列舉 (INFO、DEBUG、ERROR 等)

### 3. LogMessage
- 欄位：`level`、`message`、`timestamp` 等。

### 4. LogFormatter (介面)
- `String format(LogMessage message)`

### 5. DefaultFormatter
- 使用預設格式實作 `LogFormatter`。

### 6. LoggerConfig
- 保存記錄器的配置 (Appender、格式化器、日誌層級)。

### 7. LogAppender (在 `logappender/` 中)
- Appender 的介面。
- 實作：`ConsoleAppender`、`FileAppender` 等。

---

## 使用的設計模式

- **策略模式 (Strategy Pattern)：** 用於可互換的日誌格式化器和 Appender。
- **單例模式 (Singleton Pattern)：** (如果使用) 用於全域記錄器實例。
- **工廠模式 (Factory Pattern)：** (可選) 用於根據配置建立 Appender/格式化器。
- **觀察者模式 (Observer Pattern)：** (概念上，用於通知多個 Appender。)

---

## 範例用法

```java
Logger logger = new Logger();
logger.setConfig(new LoggerConfig(...));
logger.info("Application started");
logger.error("An error occurred");
```

---

## 演示

請參閱 `LoggingFrameworkDemo.java` 以獲取日誌框架的範例用法。

---

## 擴展框架

- **新增新的日誌層級：** 更新 `LogLevel.java`。
- **新增新的 Appender：** 在 `logappender/` 中實作 `LogAppender` 介面。
- **新增新的格式化器：** 實作 `LogFormatter` 介面。

---
