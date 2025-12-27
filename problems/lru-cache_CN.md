# 設計 LRU 快取

## 需求
1. LRU 快取應支援以下操作：
- put(key, value)：將鍵值對插入快取中。如果快取已滿，則在插入新項目之前移除最近最少使用的項目。
- get(key)：取得與給定鍵關聯的值。如果鍵存在於快取中，將其移至快取的前端 (最近使用) 並傳回其值。如果鍵不存在，則傳回 -1。
2. 快取應具有固定容量，在初始化期間指定。
3. 快取應是執行緒安全的，允許來自多個執行緒的並發存取。
4. 快取在 put 和 get 操作的時間複雜度方面應是高效的，理想情況下為 O(1)。

## UML 類別圖

![](../class-diagrams/lrucache-class-diagram.png)

## 實作
#### [Java 實作](../solutions/java/src/lrucache/) 
#### [Python 實作](../solutions/python/lrucache/)
#### [C++ 實作](../solutions/cpp/lrucache/)
#### [C# 實作](../solutions/csharp/lrucache/)
#### [Go 實作](../solutions/golang/lrucache/)

## 類別、介面和列舉
1. **Node** 類別代表雙向連結串列中的節點，包含鍵、值以及對前一個和下一個節點的參考。
2. **LRUCache** 類別使用雜湊表 (快取) 和雙向連結串列 (頭和尾) 的組合來實作 LRU 快取功能。
3. get 方法檢索與給定鍵關聯的值。如果鍵存在於快取中，它將被移至連結串列的頭部 (最近使用) 並傳回其值。如果鍵不存在，則傳回 null。
4. put 方法將鍵值對插入快取中。如果鍵已經存在，則更新其值，並將節點移至連結串列的頭部。如果鍵不存在且快取已滿，則移除最近最少使用的項目 (位於連結串列的尾部)，並將新項目插入頭部。
5. addToHead、removeNode、moveToHead 和 removeTail 方法是用於操作雙向連結串列的輔助方法。
6. synchronized 關鍵字用於 get 和 put 方法以確保執行緒安全，允許來自多個執行緒的並發存取。
7. **LRUCacheDemo** 類別透過建立一個容量為 3 的 LRUCache 實例，執行各種 put 和 get 操作並列印結果，來示範 LRU 快取的使用。
