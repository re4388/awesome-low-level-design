# Java 中的聚合 (Aggregation)

## 簡介

聚合是物件導向程式設計 (OOP) 中的一個關鍵概念，代表兩個類別之間的「擁有 (has-a)」關係，但有一個關鍵區別：被包含物件的生命週期獨立於容器物件。這意味著雖然一個類別包含另一個類別，但被包含的物件可以獨立於容器存在。

聚合允許更好的模組化、程式碼重用和可維護性。它與組合 (Composition) 不同，在組合中，被包含的物件如果沒有容器就無法存在。

---

## 什麼是聚合？

聚合是 OOP 中關聯的一種形式，其中一個類別的物件包含對另一個類別物件的參考。然而，被包含的物件可以獨立於容器存在。這意味著即使容器物件被銷毀，被包含的物件仍然可以在應用程式的其他地方使用。

### 聚合的主要特徵：
- 代表 **has-a** (擁有) 關係。
- 被包含的物件**可以獨立存在**於容器之外。
- 使用物件的參考 (指標) 來實作。
- 促進物件之間的**鬆散耦合**。

### 範例：大學與教授

考慮一個場景，一所 `University` (大學) 包含多位 `Professor` (教授)。然而，一位 `Professor` 可以獨立於任何大學存在。這就是聚合的一個例子。

```java
class Professor {
    private String name;
    private String subject;
    
    public Professor(String name, String subject) {
        this.name = name;
        this.subject = subject;
    }
    
    public void teach() {
        System.out.println(name + " is teaching " + subject);
    }
}

class University {
    private String universityName;
    private List<Professor> professors;
    
    public University(String universityName) {
        this.universityName = universityName;
        this.professors = new ArrayList<>();
    }
    
    public void addProfessor(Professor professor) {
        professors.add(professor);
    }
    
    public void showProfessors() {
        System.out.println("Professors at " + universityName + ":");
        for (Professor professor : professors) {
            System.out.println(" - " + professor.name);
        }
    }
}

import java.util.*;

public class AggregationExample {
    public static void main(String[] args) {
        Professor prof1 = new Professor("Dr. Smith", "Computer Science");
        Professor prof2 = new Professor("Dr. Johnson", "Mathematics");
        
        University university = new University("Harvard University");
        university.addProfessor(prof1);
        university.addProfessor(prof2);
        
        university.showProfessors();
        
        // 教授可以獨立存在
        prof1.teach();
        prof2.teach();
    }
}
```

### 輸出：
```
Professors at Harvard University:
 - Dr. Smith
 - Dr. Johnson
Dr. Smith is teaching Computer Science
Dr. Johnson is teaching Mathematics
```

---

## 聚合 vs 組合

| 特性         | 聚合 (Aggregation) | 組合 (Composition) |
|--------------|-------------------|--------------------|
| 關係         | "Has-a" (擁有)    | "Has-a" (擁有)     |
| 所有權       | 被包含物件**可以獨立存在** | 被包含物件**無法在沒有容器的情況下存在** |
| 生命週期     | 被包含物件**比容器活得久** | 被包含物件**隨容器一起銷毀** |
| 範例         | 大學與教授        | 汽車與引擎         |

---

## 為什麼使用聚合？

### 1. **促進程式碼重用性**
   - 聚合的物件可以在多個地方使用，而不需要與單個容器類別緊密耦合。

### 2. **鼓勵鬆散耦合**
   - 聚合允許物件互動，而不依賴於彼此的生命週期。

### 3. **更好的可維護性**
   - 一個類別的變更不會嚴重影響另一個類別，使程式碼庫更容易修改和擴展。

### 4. **真實世界的適用性**
   - 許多真實世界的關係，如學校與教師、公司與員工，自然符合聚合模型。

---

## 使用介面的聚合

使用介面，我們可以進一步增強聚合的靈活性。

```java
interface Teachable {
    void teach();
}

class Professor implements Teachable {
    private String name;
    private String subject;
    
    public Professor(String name, String subject) {
        this.name = name;
        this.subject = subject;
    }
    
    public void teach() {
        System.out.println(name + " is teaching " + subject);
    }
}

class University {
    private String universityName;
    private List<Teachable> professors;
    
    public University(String universityName) {
        this.universityName = universityName;
        this.professors = new ArrayList<>();
    }
    
    public void addProfessor(Teachable professor) {
        professors.add(professor);
    }
    
    public void showProfessors() {
        System.out.println("Professors at " + universityName + ":");
        for (Teachable professor : professors) {
            professor.teach();
        }
    }
}

import java.util.*;

public class InterfaceAggregationExample {
    public static void main(String[] args) {
        Professor prof1 = new Professor("Dr. Adams", "Physics");
        Professor prof2 = new Professor("Dr. Lee", "Chemistry");
        
        University university = new University("MIT");
        university.addProfessor(prof1);
        university.addProfessor(prof2);
        
        university.showProfessors();
    }
}
```

### 輸出：
```
Professors at MIT:
Dr. Adams is teaching Physics
Dr. Lee is teaching Chemistry
```

---

## 何時使用聚合？

- 當一個物件**可以獨立存在**於容器之外時。
- 當設計**鬆散耦合**的系統時。
- 當不同的物件需要在多個容器之間**共享**時。
- 當遵循 **SOLID 原則**，特別是 **依賴反轉原則 (DIP)** 時。
