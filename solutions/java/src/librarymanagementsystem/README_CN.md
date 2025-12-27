# 圖書館管理系統 (LLD)

## 問題陳述

設計並實作一個圖書館管理系統，允許會員借閱和歸還書籍，管理書籍庫存，追蹤借閱記錄，並支援目錄搜尋。

---

## 需求

- **書籍管理：** 系統管理書籍目錄，每本書都有多個副本。
- **會員管理：** 系統管理可以借閱和歸還書籍的圖書館會員。
- **借閱管理：** 系統追蹤哪個會員借閱了哪本書的副本以及何時借閱。
- **借閱和歸還：** 會員可以借閱可用的書籍副本並歸還它們。
- **目錄搜尋：** 會員可以按標題、作者或 ISBN 搜尋書籍。
- **可擴展性：** 易於新增功能，例如預約、罰款或通知。

---

## 核心實體

- **LibraryManagementSystem：** 管理書籍、會員、借閱和目錄的主要類別。
- **Book：** 代表一本書，包含標題、作者、ISBN 和其他元數據。
- **BookCopy：** 代表書籍的實體副本，具有唯一的副本 ID 和可用性狀態。
- **Member：** 代表具有唯一 ID 和姓名的圖書館會員。
- **Loan：** 代表會員借閱書籍副本的借閱記錄。
- **Catalog：** 管理書籍收藏並支援搜尋功能。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/LibraryManagementSystem-class-diagram.png)

### 1. LibraryManagementSystem
- **欄位：** List<Book> books, List<Member> members, List<Loan> loans, Catalog catalog
- **方法：** addBook(Book), addMember(Member), borrowBook(Member, Book), returnBook(Member, BookCopy), getLoans(Member), searchBooks(String query) 等。

### 2. Book
- **欄位：** String title, String author, String isbn, List<BookCopy> copies

### 3. BookCopy
- **欄位：** int copyId, Book book, boolean isAvailable

### 4. Member
- **欄位：** int id, String name, List<Loan> loans

### 5. Loan
- **欄位：** int id, Member member, BookCopy bookCopy, Date loanDate, Date returnDate

### 6. Catalog
- **欄位：** List<Book> books
- **方法：** searchByTitle(String), searchByAuthor(String), searchByISBN(String)

---

## 範例用法

```java
LibraryManagementSystem system = new LibraryManagementSystem();
Book book = new Book("Effective Java", "Joshua Bloch", "978-0134685991");
system.addBook(book);

Member alice = new Member(1, "Alice");
system.addMember(alice);

system.borrowBook(alice, book);
system.returnBook(alice, book.getCopies().get(0));
```

---

## 演示

請參閱 `LibraryManagementSystemDemo.java` 以獲取圖書館管理系統的範例用法和模擬。

---

## 擴展框架

- **新增預約：** 允許會員預約目前已借出的書籍。
- **新增罰款：** 追蹤逾期書籍並計算罰款。
- **新增通知：** 通知會員有關到期日、預約或新書上架的資訊。

---
