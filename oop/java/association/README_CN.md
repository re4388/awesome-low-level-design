# 物件導向程式設計 (OOP) 中的關聯 (Association)

## 簡介

關聯是物件導向程式設計 (OOP) 中的一個基本概念，定義了兩個或多個物件之間的關係。它代表了物件如何在保持獨立性的同時彼此互動。

關聯**不是繼承**——相反，它是物件之間的關係，允許通訊並確保它們保持鬆散耦合。

## 什麼是關聯？

關聯定義了兩個類別之間的連接，其中一個類別與另一個類別相連。關聯可以是**一對一**、**一對多**、**多對一**或**多對多**。關聯中的物件可以彼此獨立存在。

### 關聯的主要特徵：
- 代表 **uses-a** (使用) 或 **knows-a** (知道) 關係。
- 關聯中的物件**可以獨立存在**。
- 可以是**單向**或**雙向**的。
- 促進**模組化**和**程式碼重用性**。

### 範例：學生與老師

一個 `Student` (學生) 可以與多位 `Teacher` (老師) 物件關聯，而一位 `Teacher` 可以擁有多位 `Student` 物件。這代表了**多對多**關聯。

```java
import java.util.*;

class Teacher {
    private String name;
    private List<Student> students;
    
    public Teacher(String name) {
        this.name = name;
        this.students = new ArrayList<>();
    }
    
    public void addStudent(Student student) {
        students.add(student);
    }
    
    public void showStudents() {
        System.out.println(name + " teaches:");
        for (Student student : students) {
            System.out.println(" - " + student.getName());
        }
    }
    
    public String getName() {
        return name;
    }
}

class Student {
    private String name;
    
    public Student(String name) {
        this.name = name;
    }
    
    public String getName() {
        return name;
    }
}

public class AssociationExample {
    public static void main(String[] args) {
        Teacher teacher1 = new Teacher("Mr. Smith");
        Teacher teacher2 = new Teacher("Mrs. Johnson");
        
        Student student1 = new Student("Alice");
        Student student2 = new Student("Bob");
        
        teacher1.addStudent(student1);
        teacher1.addStudent(student2);
        teacher2.addStudent(student2);
        
        teacher1.showStudents();
        teacher2.showStudents();
    }
}
```

### 輸出：
```
Mr. Smith teaches:
 - Alice
 - Bob
Mrs. Johnson teaches:
 - Bob
```

---

## 關聯的類型

### 1. **一對一關聯 (One-to-One Association)**
   - 類別 A 的每個物件與類別 B 的一個物件關聯。
   - 範例：一個人 (`Person`) 擁有一本護照 (`Passport`)。

### 2. **一對多關聯 (One-to-Many Association)**
   - 類別 A 的一個物件可以與類別 B 的多個物件關聯。
   - 範例：一位老師 (`Teacher`) 教導多位學生 (`Students`)。

### 3. **多對一關聯 (Many-to-One Association)**
   - 類別 A 的多個物件可以與類別 B 的一個物件關聯。
   - 範例：多位學生 (`Students`) 屬於一所學校 (`School`)。

### 4. **多對多關聯 (Many-to-Many Association)**
   - 類別 A 的多個物件可以與類別 B 的多個物件關聯。
   - 範例：老師 (`Teachers`) 與學生 (`Students`) (一位學生可以有多位老師，一位老師可以有多位學生)。

---

## 為什麼使用關聯？

### 1. **促進程式碼重用性**
   - 物件可以在多個關聯中重用，而無需重複。

### 2. **鼓勵鬆散耦合**
   - 物件互動時不依賴於彼此的內部實作。

### 3. **提高可維護性**
   - 更改一個物件不會嚴重影響其他物件，使程式碼更易於管理。

### 4. **更好的系統設計**
   - 允許有效地建模實體之間的真實世界關係。

---

## 關聯 vs 聚合 vs 組合

| 特性         | 關聯 (Association) | 聚合 (Aggregation) | 組合 (Composition) |
|--------------|-------------------|-------------------|--------------------|
| 關係         | "Knows-a" (知道)  | "Has-a" (擁有)    | "Has-a" (擁有)     |
| 物件獨立性   | 物件是獨立的      | 被包含物件**可以獨立存在** | 被包含物件**無法在沒有容器的情況下存在** |
| 生命週期     | 物件分開存在      | 被包含物件**比容器活得久** | 被包含物件**隨容器一起銷毀** |
| 範例         | 老師與學生        | 大學與教授        | 汽車與引擎         |

---

## 雙向關聯

關聯可以是**單向** (一個物件知道另一個) 或**雙向** (兩個物件彼此知道)。

### 範例：圖書館與書籍 (雙向關聯)

```java
import java.util.*;

class Book {
    private String title;
    private Library library;
    
    public Book(String title, Library library) {
        this.title = title;
        this.library = library;
    }
    
    public void showLibrary() {
        System.out.println(title + " is in " + library.getName());
    }
    
    public String getTitle() {
        return title;
    }
}

class Library {
    private String name;
    private List<Book> books;
    
    public Library(String name) {
        this.name = name;
        this.books = new ArrayList<>();
    }
    
    public void addBook(Book book) {
        books.add(book);
    }
    
    public String getName() {
        return name;
    }
    
    public void showBooks() {
        System.out.println("Books in " + name + ":");
        for (Book book : books) {
            System.out.println(" - " + book.getTitle());
        }
    }
}

public class BidirectionalAssociationExample {
    public static void main(String[] args) {
        Library library = new Library("City Library");
        Book book1 = new Book("1984", library);
        Book book2 = new Book("Brave New World", library);
        
        library.addBook(book1);
        library.addBook(book2);
        
        library.showBooks();
        book1.showLibrary();
        book2.showLibrary();
    }
}
```

### 輸出：
```
Books in City Library:
 - 1984
 - Brave New World
1984 is in City Library
Brave New World is in City Library
```
