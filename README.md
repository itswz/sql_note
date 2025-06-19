# 📘 Chapter 13: Designing Databases 数据库设计

---

## 🧩 Data Modelling 数据建模简介

**EN:**  
Data modelling is the process of modeling the data we want to store. It involves 4 main steps:

**中：**  
数据建模是将我们需要管理的数据结构化的过程，主要包括以下四个步骤：

1. **Understanding and analyzing the business requirements**  
   **理解和分析业务需求**

2. **Build a conceptual model**  
   **建立概念模型：** 通过可视化方式表示实体及其关系，以便与利益相关者沟通

3. **Build a logical model**  
   **建立逻辑模型：** 与具体数据库技术无关，定义数据结构

4. **Build a physical model**  is the implementation of logical model
   **建立物理模型：** 针对具体数据库技术进行的物理设计，如 MySQL、PostgreSQL 等

---


# 🧠 数据库设计笔记：Conceptual & Logical Models（中英对照）

---

## 📘 系统示例：学生选课系统（Student Course Enrollment System）

本系统用于记录学生注册课程的情况。

---

## 1️⃣ Conceptual Model（概念模型）

**EN:**  
The conceptual model represents real-world entities and how they are related. It focuses on business understanding, not implementation.

**中：**  
概念模型用于描述现实中的实体及其相互关系，关注的是业务结构，而非具体数据库实现。

---

### 🟦 Entities 实体 & 🟠 Attributes 属性

#### `Student` 学生
- `name` 姓名
- `email` 邮箱
- `date_registered` 注册日期

#### `Course` 课程
- `title` 课程标题
- `price` 价格
- `instructor` 授课人
- `tags` 标签（如分类、关键词）

#### `Enrollment` 选课记录
- 用于连接学生与课程，表示“学生选修了哪门课”
- 可添加属性如：选课时间、价格（价格随着时间变化）

---

### 🔷 Relationships 关系

- `Student` **enrolls in** `Course`  
  `学生` **选修** `课程`

---

### 🖼️ 概念图（ER结构，文字简图）


---

## 2️⃣ Logical Model（逻辑模型）

**EN:**  
The logical model transforms entities into table structures, defines primary/foreign keys, but still stays independent of specific database systems.

**中：**  
逻辑模型将实体转换为数据表结构，定义主键、外键和关联表，但仍与具体数据库无关。

---

### 🔧 数据表设计（逻辑结构）

#### 📄 Student 表

| 字段名 | 含义 | 数据类型 |
|--------|------|--------|
| `name` | 姓名 | string |
| `email` | 邮箱 | string |
| `date_registered` | 注册时间 | dataTime |

---

#### 📄 Course 表

| 字段名 | 含义 | 数据类型 |
|--------|------|--------|
| `title` | 课程标题 | string |
| `price` | 价格 | float |
| `instructor` | 授课人 | string |
| `tags` | 标签 | string |

---

#### 📄 Enrollment 表（关系表）

| 字段名 | 含义 | 数据类型 |
|--------|------|--------|
| `date` | 时间 | dateTime |
| `price` | 价格 | float |

# 数据库关系说明 / Database Relationship Explanation

## 学生(Student)与课程(Course)的关系  
**中文：**  
学生和课程之间是多对多（Many-to-Many）的关系。因为一个学生可以选修多门课程，而一门课程也可以被多个学生选修。

**English:**  
Student and Course have a many-to-many relationship because a student can take many courses, and a course can have many students.

---

## 学生(Student)与选课记录(Enrollment)的关系  
**中文：**  
学生和选课记录之间是一对多（One-to-Many）的关系。一个学生可以有多条选课记录，每条选课记录对应唯一一个学生。

**English:**  
Student and Enrollment have a one-to-many relationship because one student can have many enrollment records, but each enrollment record belongs to exactly one student.

---

## 课程(Course)与选课记录(Enrollment)的关系  
**中文：**  
课程和选课记录之间也是一对多（One-to-Many）的关系。一门课程可以有多条选课记录，每条选课记录对应唯一一门课程。

**English:**  
Course and Enrollment also have a one-to-many relationship because a course can have many enrollment records, but each enrollment record corresponds to exactly one course.


# Normal forms
## 1️⃣ First Normal Form (1NF) 第一范式

### ✅ Definition 定义：
> **EN:**  
Each cell should contain a single (atomic) value, and there should be no repeating columns.

> **中：**  
每个单元格必须包含**单一值（原子值）**，不能包含多个值；同时不允许出现重复列（如 course1, course2, course3）。


## 2️⃣ Second Normal Form (2NF) 第二范式

### ✅ Definition 定义：
> **EN:**  
Each table should describe **one entity**, and every column in that table should describe **attributes of that entity**.  
Also: the table must be in 1NF, and all non-key attributes must be **fully dependent on the entire primary key**.

> **中：**  
每张表应只描述**一个实体**，且该表中的每一列都应描述该实体的属性。  
此外：必须满足 1NF，且所有非主键属性必须**完全依赖于整个主键**，不能只依赖主键的一部分。

## 3️⃣ Third Normal Form (3NF) 第三范式

### ✅ Definition 定义：

> **EN:**  
A column in a table should not be derived from another column.  
In other words, every non-key attribute must depend **only on the primary key**, not on another non-key attribute.

> **中：**  
表中的某个字段不应该由另一个字段**推导得出**。  
换句话说，所有非主键字段**只能依赖主键**，不能依赖其他非主键字段（即**不允许传递依赖**）。

---
