# 🎓 Full Assignment: **Build the `focus-guardian` App**

### *(A Real-Life Inspired Project to Beat Social Media Addiction)*

---

## 🌍 **Story Background: A Mom and Her Son**

Meet **Sarah**, a single mom of two, who works full-time and studies part-time. Her 14-year-old son, **Liam**, used to be a bright and curious kid. But lately, he’s been glued to his phone — spending hours scrolling on TikTok, chatting on WhatsApp, and watching endless YouTube shorts. His grades are slipping, he’s skipping meals, and he’s losing sleep.

Sarah wants to help Liam — not by banning phones — but by teaching him **digital discipline**. She decides to build a simple app with her son. Every time he **resists the urge to scroll**, he can record a success. He can write **why** he stayed focused, and the app will record it for him — to celebrate wins and reflect on slips.

You are going to build that app: **Focus Guardian** 💡

---

## 🧑‍💻 **Your Mission**

Design and build a **Spring Boot + PostgreSQL** app that helps users **track their digital discipline**. You’ll let users submit "focus entries" where they:

* Say **how** they stayed off social media
* Record whether they were successful
* View all past entries
* See basic **analytics** like total entries and success rate

---

## 🛠️ Project Details

### 🔷 Project Name: `focus-guardian`

Create a new Spring Boot Maven project **manually** (no Spring Initializr).

### 📚 Technologies:

* Java 17+
* IntelliJ IDEA Community Edition
* PostgreSQL (via `psql` CLI)
* Spring Boot (Web + JPA)
* Postman or `curl` for testing

---

## 📋 Assignment Requirements

---

### ✅ Step 1: Set Up the Project

* Create a new **Maven** project in IntelliJ called `focus-guardian`
* Package name: `com.example.focusguardian`

---

### ✅ Step 2: Add Dependencies to `pom.xml`

Include:

* Spring Boot starter parent
* `spring-boot-starter-web`
* `spring-boot-starter-data-jpa`
* PostgreSQL JDBC driver
* Spring Boot Maven plugin

---

### ✅ Step 3: Package Structure

Create this structure:

```
com.example.focusguardian
├── model         # FocusEntry entity
├── repo          # FocusEntryRepository
├── web           # FocusEntryController
```

---

### ✅ Step 4: Create the `FocusEntry` Entity

Your data class should represent this structure:

| Field       | Type          | Description                             |
| ----------- | ------------- | --------------------------------------- |
| `id`        | Long          | Primary key, auto-generated             |
| `reason`    | String        | What helped the user stay focused       |
| `status`    | Boolean       | true = success, false = gave in         |
| `createdAt` | LocalDateTime | When the entry was submitted (auto-set) |

👉 Use JPA annotations: `@Entity`, `@Id`, `@GeneratedValue`, etc.
👉 Use `@PrePersist` to auto-set `createdAt` when saving.

---

### ✅ Step 5: Create the Repository

Create an interface that extends `CrudRepository<FocusEntry, Long>`.
No methods needed yet — you'll use inherited ones like:

* `save()`
* `findById()`
* `findAll()`
* `count()`

---

### ✅ Step 6: Create the Controller

Create a `FocusEntryController` with the following endpoints:

| Endpoint       | Method | Purpose                           |
| -------------- | ------ | --------------------------------- |
| `/focus`       | POST   | Add a new focus entry             |
| `/focus/{id}`  | GET    | View one entry                    |
| `/focus`       | GET    | View all entries                  |
| `/focus/stats` | GET    | Show total entries + success rate |

🔁 Use:

* `@RestController`
* `@RequestMapping("/focus")`
* `@PostMapping`, `@GetMapping`, `@PathVariable`, `@RequestBody`

---

### ✅ Step 7: Configure PostgreSQL

1. In `application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/focus_guardian
spring.datasource.username=postgres
spring.datasource.password=admin
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
```

2. In `psql`, create the DB:

```bash
psql -U postgres
CREATE DATABASE focus_guardian;
```

---

### ✅ Step 8: Test the App

Use **Postman** or `curl`:

* Submit a new entry:

```json
{
  "reason": "I put my phone on airplane mode and finished my math homework",
  "status": true
}
```

* Get all entries
* Try submitting a few `false` ones too (user gave in)

---

## 📊 Step 9: Add Analytics Endpoint

Create `/focus/stats` that returns JSON like:

```json
{
  "total": 6,
  "successes": 4,
  "failures": 2,
  "successRate": 66.67
}
```

Implement it by:

* Calling `findAll()`
* Filtering `status=true`
* Calculating the percentage

---

## ✨ Bonus Features (Optional)

| Feature                           | Idea                                 |
| --------------------------------- | ------------------------------------ |
| Filter entries by success/failure | `/focus/success` or `/focus/failure` |
| Add optional tag/category field   | e.g., `"studying"`, `"family time"`  |
| Add a weekly summary view         | Future `@Scheduled` extension        |
| Add user authentication           | For future expansion                 |

---

## 📝 Submission Instructions

Students should submit:

* Their entire IntelliJ project
* Sample JSON requests used for testing
* Screenshot of PostgreSQL table (via `psql`)
* Sample `/focus/stats` result

---

## 💬 Teaching Philosophy

| Why this matters     | How it helps students                               |
| -------------------- | --------------------------------------------------- |
| Real story & empathy | Students relate and reflect on digital habits       |
| REST + PostgreSQL    | Foundational backend skill                          |
| Boolean logic        | Think in true/false conditions (clean model design) |
| Analytics            | Start thinking about data as insight                |
| Manual setup         | Builds strong fundamentals for real-world apps      |


