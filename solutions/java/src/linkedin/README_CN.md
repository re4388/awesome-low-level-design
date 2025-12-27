# LinkedIn (LLD)

## 問題陳述

設計並實作一個類似 LinkedIn 的專業社群網路平台，允許使用者建立個人資料、與他人連結、發布工作、發送訊息和接收通知。

---

## 需求

- **使用者管理：** 使用者可以註冊、登入並管理其個人資料。
- **個人資料管理：** 使用者可以將教育、經歷和技能新增至其個人資料。
- **連結：** 使用者可以發送和接受連結請求。
- **工作發布：** 使用者 (或公司) 可以發布職缺。
- **訊息傳遞：** 使用者可以向其連結發送直接訊息。
- **通知：** 系統通知使用者有關連結請求、工作配對、訊息和其他事件。
- **可擴展性：** 易於新增功能，例如認可、推薦或公司頁面。

---

## 核心實體

- **LinkedInService：** 管理使用者、連結、工作發布、訊息和通知的主要類別。
- **User：** 代表具有個人資料、連結、訊息和通知的使用者。
- **Profile：** 代表使用者的專業個人資料，包括教育、經歷和技能。
- **Connection：** 代表兩個使用者之間的連結。
- **JobPosting：** 代表使用者或公司發布的工作。
- **Message：** 代表使用者之間的直接訊息。
- **Notification：** 代表發送給使用者的通知。
- **NotificationType (列舉)：** 通知的類型 (例如：CONNECTION_REQUEST, JOB_MATCH, MESSAGE)。
- **Skill：** 代表使用者個人資料中的技能。
- **Education：** 代表使用者個人資料中的教育項目。
- **Experience：** 代表使用者個人資料中的工作經歷項目。

---

## 類別設計

## UML 類別圖

![](../../../../uml-diagrams/class-diagrams/linkedin-class-diagram.png)

### 1. LinkedInService
- **欄位：** List<User> users, List<JobPosting> jobPostings, List<Connection> connections, List<Notification> notifications
- **方法：** registerUser(User), addConnection(User, User), postJob(JobPosting), sendMessage(User, User, String), sendNotification(Notification), searchUsers(String), searchJobs(String) 等。

### 2. User
- **欄位：** int id, String name, Profile profile, List<Connection> connections, List<Message> messages, List<Notification> notifications
- **方法：** sendConnectionRequest(User), acceptConnection(Connection), sendMessage(User, String), addSkill(Skill), addEducation(Education), addExperience(Experience) 等。

### 3. Profile
- **欄位：** List<Skill> skills, List<Education> education, List<Experience> experience

### 4. Connection
- **欄位：** int id, User user1, User user2, boolean isAccepted

### 5. JobPosting
- **欄位：** int id, String title, String description, User postedBy

### 6. Message
- **欄位：** int id, User sender, User receiver, String content

### 7. Notification
- **欄位：** int id, User recipient, String message, NotificationType type

### 8. NotificationType (列舉)
- 值：CONNECTION_REQUEST, JOB_MATCH, MESSAGE 等。

### 9. Skill
- **欄位：** String name

### 10. Education
- **欄位：** String institution, String degree, String fieldOfStudy, int startYear, int endYear

### 11. Experience
- **欄位：** String company, String title, int startYear, int endYear

---

## 範例用法

```java
LinkedInService service = new LinkedInService();
User alice = new User(1, "Alice");
User bob = new User(2, "Bob");
service.registerUser(alice);
service.registerUser(bob);

alice.sendConnectionRequest(bob);
service.addConnection(alice, bob);

Profile profile = alice.getProfile();
profile.addSkill(new Skill("Java"));
profile.addEducation(new Education("MIT", "BSc", "CS", 2010, 2014));
profile.addExperience(new Experience("Google", "Software Engineer", 2014, 2018));

JobPosting job = new JobPosting(1, "Backend Developer", "Work on scalable systems", alice);
service.postJob(job);

service.sendMessage(alice, bob, "Hi Bob, let's connect!");
```

---

## 演示

請參閱 `LinkedInDemo.java` 以獲取 LinkedIn 系統的範例用法和模擬。

---

## 擴展框架

- **新增認可：** 允許使用者認可彼此的技能。
- **新增推薦：** 支援為使用者撰寫推薦。
- **新增公司頁面：** 允許公司建立和管理自己的頁面。

---
