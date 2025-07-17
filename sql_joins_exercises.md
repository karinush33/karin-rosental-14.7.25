# 📊 תרגול SQL: סוגי JOIN (1:1, 1\:N, M\:N)

## 🔐 קשר אחד לאחד: משתמשים + סיסמאות

### ✅ הצג את כל המשתמשים עם הסיסמה שלהם (INNER JOIN)

```sql
SELECT us.name, p.password_hash
FROM users us
INNER JOIN passwords p ON us.user_id = p.user_id;
```

### ✅ הצג את כל המשתמשים, כולל כאלה שאין להם סיסמה (LEFT JOIN)

```sql
SELECT us.*, p.password_hash
FROM users us
LEFT JOIN passwords p ON us.user_id = p.user_id;
```

### ✅ הצג את המשתמשים שאין להם סיסמה כלל

```sql
SELECT us.*, p.password_hash
FROM users us
LEFT JOIN passwords p ON us.user_id = p.user_id
WHERE p.password_hash IS NULL;
```

---

## 🧑‍💼 קשר אחד לרבים: מחלקות + עובדים

### ✅ הצג את כל העובדים עם שם המחלקה שלהם

```sql
SELECT e.name AS employee_name, d.name AS department_name
FROM departments d
JOIN employees e ON e.department_id = d.department_id;
```

### ✅ הצג את כל המחלקות וספור כמה עובדים יש בכל מחלקה

```sql
SELECT d.name AS department_name, COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e ON d.department_id = e.department_id
GROUP BY d.name;
```

### ✅ הצג את כל העובדים כולל כאלה שלא שויכו למחלקה

```sql
SELECT e.name AS employee_name, d.name AS department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id;
```

### ✅ הצג מחלקות שאין בהן אף עובד

**הערה:** כרגע אין מחלקות שאין להן עובדים.

```sql
SELECT d.department_id, d.name
FROM departments d
LEFT JOIN employees e ON d.department_id = e.department_id
WHERE e.employee_id IS NULL;
```

---

## 👥 קשר רבים לרבים: אזרחים + חברות כבלים + מנויים

### ✅ הצג את כל המנויים עם שם האזרח ושם החברה

```sql
SELECT ci.name AS citizen_name, ca.name AS company_name
FROM subscriptions s
INNER JOIN citizens ci ON s.citizen_id = ci.citizen_id
INNER JOIN cable_tv ca ON s.company_id = ca.company_id;
```

### ✅ הצג את כל האזרחים וכמה חברות הם מנויים אליהן

```sql
SELECT ci.name, COUNT(s.company_id) AS subscription_count
FROM citizens ci
LEFT JOIN subscriptions s ON ci.citizen_id = s.citizen_id
GROUP BY ci.name;
```

### ✅ הצג את כל חברות הכבלים וכמה מנויים יש להן

```sql
SELECT ca.name, COUNT(s.citizen_id) AS subscriber_count
FROM cable_tv ca
LEFT JOIN subscriptions s ON ca.company_id = s.company_id
GROUP BY ca.name;
```

### ✅ הצג אזרחים שלא מנויים לאף חברה

```sql
SELECT ci.name
FROM citizens ci
LEFT JOIN subscriptions s ON ci.citizen_id = s.citizen_id
WHERE s.company_id IS NULL;
```

### ✅ הצג חברות שאין להן אף מנוי

**הערה:** כרגע אין חברות שאין להן מנויים.

```sql
SELECT ca.name
FROM cable_tv ca
LEFT JOIN subscriptions s ON ca.company_id = s.company_id
WHERE s.citizen_id IS NULL;
```

---

🧠 נבנה באהבה עם SQL + DBeaver

