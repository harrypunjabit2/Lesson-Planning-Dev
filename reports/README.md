# 📊 Reports Module

This folder contains **audit and exception reports** for the Kumon Lesson Planning system.  
The goal of these reports is to identify gaps or issues in weekly lesson planning and provide CSV exports for review.

---

## 📂 Folder Structure
reports/
├─ sql/ # Raw SQL queries and CREATE VIEW scripts
├─ php/ # Plain PHP or Laravel controller code for CSV download
├─ examples/ # Example CSV outputs for reference
└─ README.md # This file (documentation)


---

## 📑 Reports Included

### 1. Students with **No Lesson Plan** (current week / next week)
- **Purpose:** Detects active students in `student_configs` with no lesson plan assigned.  
- **SQL:** `reports/sql/no_plan_current_week.sql`, `no_plan_next_week.sql`  
- **Output:** CSV → First Name, Last Name, Subject.

---

### 2. **New Concept** scheduled on a Class Day
- **Purpose:** Flags lesson plans where `new_concept = Y` but the day is marked as a class day (should only be on homework days).  
- **SQL:** `reports/sql/new_concept_classday.sql`  
- **Output:** CSV → Student info, Subject, Date, Day of Week, Flag.

---

### 3. **Test** scheduled on a Class Day
- **Purpose:** Flags lesson plans that contain a test (detected via worksheet/test flag) but are scheduled on class days.  
- **SQL:** `reports/sql/tests_classday.sql`  
- **Output:** CSV → Student info, Subject, Date, Day of Week, Flag.

---

### 4. Students in DB but **Missing on Lesson Plan**
- **Purpose:** Finds students listed in `student_configs` but not present in `lesson_plans` for the target week.  
- **SQL:** `reports/sql/missing_students.sql`  
- **Output:** CSV → First Name, Last Name, Subject.

---

## ⚙️ How to Use

### SQL
- Run the `.sql` files inside `reports/sql/` in MySQL/phpMyAdmin to create **views** or run ad-hoc queries.  
- Views can be reused by Laravel or PHP scripts.

### PHP / Laravel
- `reports/php/` contains examples:  
  - **Plain PHP:** Exports CSV directly from queries.  
  - **Laravel Controller:** Provides routes like `/reports/no-plan-current-week` for CSV download.  

### Examples
- `reports/examples/` holds sample CSVs so staff can preview output.

---

## 🚀 Next Steps
1. Developer integrates the SQL queries into the Laravel app.  
2. Add endpoints (see `routes/reports.php`) for CSV download.  
3. Optionally, schedule reports with Laravel’s Task Scheduler (`php artisan schedule:run`).  


