# LRU 快取 (LLD)

## 問題陳述

設計並實作一個具有固定容量的 LRU (最近最少使用) 快取。快取應支援快速檢索和插入，並在超過容量時自動驅逐最近最少使用的項目。

---

## 需求

- **固定容量：** 快取具有最大大小。當滿時，插入時會驅逐最近最少使用的項目。
- **快速操作：** `get(key)` 和 `put(key, value)` 操作都應為 O(1)。
- **驅逐策略：** 當快取超過其容量時，移除最近最少使用的項目。
- **可擴展性：** 易於更改驅逐策略或底層資料結構。

---

## 核心實體

- **LRUCache：** 實作快取邏輯的主要類別，管理儲存和驅逐。
- **Node：** 代表雙向鏈結串列節點，用於快速移除和插入。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/lrucache-class-diagram.png)

### 1. LRUCache
- **欄位：** capacity, Map<K, Node<K, V>>, 雙向鏈結串列的 head/tail 指標
- **方法：**
  - `get(K key)`：如果存在，則傳回鍵的值，否則傳回 -1/null。將節點移動到前端 (最近使用)。
  - `put(K key, V value)`：插入或更新鍵的值。將節點移動到前端。如果快取超過容量，則驅逐最近最少使用的節點。
  - `removeNode(Node)`, `addToFront(Node)`, `moveToFront(Node)`, `evictLRU()`：用於列表管理的輔助方法。

### 2. Node
- **欄位：** key, value, prev, next

---

## 使用的設計模式

- **雙向鏈結串列 (Doubly Linked List)：** 用於 O(1) 的節點移除和插入。
- **雜湊映射 (Hash Map)：** 用於 O(1) 的按鍵存取節點。
- **關注點分離 (Separation of Concerns)：** 節點和快取邏輯是分離的。

---

## 範例用法

```java
LRUCache cache = new LRUCache(2);
cache.put(1, 1); // cache: {1=1}
cache.put(2, 2); // cache: {1=1, 2=2}
cache.get(1);    // 傳回 1, cache: {2=2, 1=1}
cache.put(3, 3); // 驅逐鍵 2, cache: {1=1, 3=3}
cache.get(2);    // 傳回 -1 (未找到)
```

---

## 演示

請參閱 `LRUCacheDemo.java` 以獲取 LRU 快取的範例用法和模擬。

---

## 擴展框架

- **更改驅逐策略：** 透過修改驅逐邏輯來實作不同的策略 (例如：LFU)。
- **更改資料結構：** 使用其他結構以獲得不同的效能特徵。

---
