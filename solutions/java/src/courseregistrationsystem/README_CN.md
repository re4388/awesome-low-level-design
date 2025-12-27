# 課程註冊系統 (LLD)

## 問題陳述

設計並實作一個課程註冊系統，允許學生註冊課程，管理課程容量，並追蹤學生選課情況。

---

## 需求

- **學生註冊：** 學生可以註冊課程。
- **課程管理：** 系統管理課程，每個課程都有唯一的代碼、名稱和容量。
- **容量強制執行：** 如果課程已滿，學生無法註冊該課程。
- **防止重複：** 學生不能重複註冊同一門課程。
- **選課追蹤：** 系統追蹤哪些學生註冊了哪些課程。
- **可擴展性：** 易於新增功能，例如課程先修條件、候補名單或退選功能。

---

## 核心實體

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/CourseRegistrationSystem-class-diagram.png)

- **CourseRegistrationSystem：** 管理學生、課程和註冊的主要類別。
- **Student：** 代表具有唯一 ID 和姓名的學生。
- **Course：** 代表具有唯一代碼、名稱和容量的課程。
- **Registration：** 代表學生在課程中的註冊記錄。

---

## 類別設計

### 1. CourseRegistrationSystem
- **欄位：** Map<String, Course> courses, Map<Integer, Student> students, List<Registration> registrations
- **方法：** registerStudent(Student), addCourse(Course), register(int studentId, String courseCode), getStudentCourses(int studentId), getCourseStudents(String courseCode) 等。

### 2. Student
- **欄位：** int id, String name

### 3. Course
- **欄位：** String code, String name, int capacity, List<Student> enrolledStudents
- **方法：** enrollStudent(Student), isFull(), getEnrolledStudents()

### 4. Registration
- **欄位：** Student student, Course course

---

## 範例用法

```java
CourseRegistrationSystem system = new CourseRegistrationSystem();
system.registerStudent(new Student(1, "Alice"));
system.registerStudent(new Student(2, "Bob"));
system.addCourse(new Course("CS101", "Intro to CS", 2));
system.addCourse(new Course("MATH101", "Calculus I", 1));

system.register(1, "CS101"); // Alice 註冊 CS101
system.register(2, "CS101"); // Bob 註冊 CS101
system.register(1, "MATH101"); // Alice 註冊 MATH101

// 列出 Alice 的課程
List<Course> aliceCourses = system.getStudentCourses(1);
// 列出 CS101 的學生
List<Student> cs101Students = system.getCourseStudents("CS101");
```

---

## 演示

請參閱 `CourseRegistrationSystemDemo.java` 以獲取課程註冊系統的範例用法和模擬。

---

## 擴展框架

- **新增課程先修條件：** 追蹤並強制執行課程註冊的先修條件。
- **新增候補名單：** 如果課程已滿，允許學生加入候補名單。
- **新增退選功能：** 允許學生退選課程。

---
