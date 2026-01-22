# 🎓 Oracle University DB (Users, Privileges, Triggers, Procedures)

A complete **Oracle XE / SQL*Plus** lab project that demonstrates:

- Multi-user setup (**SYS / MANAGER / USER1 / USER2**)
- Schema design with constraints (PK/FK/CHK/UNQ)
- Cross-schema privileges and access control
- Sequences, triggers (auditing + prerequisite check)
- Functions (grade + GPA calculation)
- Procedures (warnings, suspension, course performance report)
- Basic concurrency/locking inspection (bonus)

> ⚠️ Note: This project is for **educational/lab use**. Privileges like `GRANT ANY PRIVILEGE` are not recommended in production.

---

## ✅ Requirements

- **Oracle Database XE** (tested pattern: **XEPDB1** pluggable DB)
- **SQL*Plus**
- Local listener running (example connect string):
  - `localhost:1521/XEPDB1`

---

## 📁 Project Structure

```
oracle-university-db/
│── sql/
│   │── 00_setup_container.sql
│   │── 01_users_and_privileges.sql
│   │── 02_schema_tables.sql
│   │── 03_cross_schema_grants.sql
│   │── 04_seed_data.sql
│   │── 05_sequences.sql
│   │── 06_triggers.sql
│   │── 07_functions.sql
│   │── 08_procedures.sql
│   │── 09_tests_and_demo.sql
│   │── 10_bonus_locking.sql
│── docs/
│   │── NOTES.md
│── .gitignore
│── README.md
```

---

## 🚀 How to Run (Recommended Order)

### 1) As SYS (set container + create users)
```sql
sqlplus / as sysdba
@sql/00_setup_container.sql
@sql/01_users_and_privileges.sql
```

### 2) As USER1 (create schema objects)
```sql
sqlplus USER1/u1@localhost:1521/XEPDB1
@sql/02_schema_tables.sql
@sql/05_sequences.sql
@sql/06_triggers.sql
@sql/07_functions.sql
@sql/08_procedures.sql
```

### 3) As SYS (grant manager ability to grant, then cross-schema grants)
```sql
sqlplus / as sysdba
@sql/00_setup_container.sql
@sql/03_cross_schema_grants.sql
```

### 4) As USER2 (insert demo data + run demos)
```sql
sqlplus USER2/u2@localhost:1521/XEPDB1
@sql/04_seed_data.sql
@sql/09_tests_and_demo.sql
```

### 5) Bonus: locking inspection
```sql
sqlplus / as sysdba
@sql/00_setup_container.sql
@sql/10_bonus_locking.sql
```

---

## 🧩 Main Objects

### Tables
- `Professors`, `Courses` (self-FK prerequisite)
- `Students`, `Register`
- `Exams`, `ExamResults`
- `AuditTrail`, `Warnings`, `DBUserCreationLog`

### Triggers
- `TRG_CHECK_PREREQ` — blocks registration if prerequisite course not passed
- `TRG_REGISTER_AUDIT_INS` / `TRG_REGISTER_AUDIT_DEL` — audit Register inserts/deletes

### Functions
- `FN_CALC_GRADE(examresult_id)` — sets grade/status based on score
- `FN_CALC_GPA(student_id)` — calculates GPA from grades & credit hours

### Procedures
- `PR_ISSUE_WARNINGS` — inserts warnings for students failing >= 2 courses
- `PR_SUSPEND_STUDENTS` — suspends students with >= 3 warnings (and audits)
- `PR_COURSE_PERFORMANCE_REPORT(course_id)` — prints report in DBMS_OUTPUT

---

## 🔐 Users & Roles (Lab Setup)

- `MANAGER` — admin-like lab user (can create/alter/drop users, grant privileges)
- `USER1` — schema owner (tables, triggers, functions, procedures)
- `USER2` — application user (insert/select on selected tables)

Passwords in this repo are **lab defaults** (u1/u2/123). Change them if needed.

---

## 📝 Author
**Yasmen Ramadan**  
📧 yasmin18ramadan@gmail.com  
🐙 https://github.com/Yasmmiinaah  
🔗 https://www.linkedin.com/in/yasmenramadan/

---
