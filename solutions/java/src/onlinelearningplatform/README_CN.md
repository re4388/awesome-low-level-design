# 線上學習平台 (LLD)

## 問題陳述

設計並實作一個線上學習平台，允許使用者註冊課程、觀看課程內容、參加測驗並追蹤進度。

---

## 需求

- **使用者管理：** 使用者可以註冊、登入並管理其個人資料。
- **課程管理：** 講師可以建立和管理課程，包括影片、閱讀材料和測驗。
- **註冊：** 學生可以註冊課程。
- **內容傳遞：** 學生可以存取課程內容 (影片、文字)。
- **評估：** 學生可以參加測驗並獲得分數。
- **進度追蹤：** 系統追蹤學生在每門課程中的進度。
- **可擴展性：** 易於新增功能，例如證書、討論區或直播課程。

---

## 核心實體

- **LearningPlatform：** 管理使用者、課程、註冊和進度的主要類別。
- **User：** 代表使用者 (學生或講師)。
- **Course：** 代表一門課程，包含模組和內容。
- **Module：** 代表課程的一個部分。
- **Content：** 代表學習材料 (影片、文字)。
- **Quiz：** 代表包含問題的評估。
- **Enrollment：** 代表學生在課程中的註冊。
- **Progress：** 追蹤學生在課程中的完成狀態。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/onlinelearningplatform-class-diagram.png)

### 1. LearningPlatform
- **欄位：** List<User> users, List<Course> courses, List<Enrollment> enrollments
- **方法：** registerUser(User), createCourse(Course), enrollStudent(User, Course), getStudentProgress(User, Course) 等。

### 2. User
- **欄位：** int id, String name, String email, UserRole role

### 3. Course
- **欄位：** int id, String title, String description, User instructor, List<Module> modules

### 4. Module
- **欄位：** int id, String title, List<Content> contents, Quiz quiz

### 5. Content
- **欄位：** int id, String title, String type, String url/text

### 6. Quiz
- **欄位：** int id, List<Question> questions

### 7. Enrollment
- **欄位：** User student, Course course, Date enrollmentDate

### 8. Progress
- **欄位：** Enrollment enrollment, Map<Content, Boolean> completedContents, Map<Quiz, Integer> quizScores

---

## 範例用法

```java
LearningPlatform platform = new LearningPlatform();
User instructor = new User(1, "Dr. Smith", "smith@example.com", UserRole.INSTRUCTOR);
User student = new User(2, "Alice", "alice@example.com", UserRole.STUDENT);

platform.registerUser(instructor);
platform.registerUser(student);

Course course = new Course(1, "Java Programming", "Learn Java from scratch", instructor);
platform.createCourse(course);

platform.enrollStudent(student, course);
```

---

## 演示

請參閱 `OnlineLearningPlatformDemo.java` 以獲取線上學習平台的範例用法和模擬。

---

## 擴展框架

- **新增證書：** 完成課程後產生證書。
- **新增討論區：** 允許學生和講師互動。
- **新增直播課程：** 支援即時視訊串流課程。

---
