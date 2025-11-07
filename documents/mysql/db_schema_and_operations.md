# 🧩 Database Setup and Operations

1. Database Operations <br>

1-1. Create Database
```sql
CREATE DATABASE mydb;
```
1-2. Select Database
```sql
USE mydb;
```
1-3. Drop Database
```sql
DROP DATABASE mydb;
```
---
2. Table Creation

2-1. Users Table
```sql
CREATE TABLE users(
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL COMMENT 'Name',
    gender CHAR(1) NOT NULL COMMENT 'F = Female, M = Male, N = Not Specified',
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP(),
    updated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP(),
    deleted_at DATETIME
);
```
Explains: <br>
- BIGINT UNSIGNED for large positive integers.
- AUTO_INCREMENT automatically increases the primary key.
- deleted_at can be NULL if not used.
- Use InnoDB engine and UTF8MB4 charset for modern applications.
- bigint unsigned -> data type
- primary key auto_increment -> constraint

2-2. Articles Table
```sql
CREATE TABLE articles(
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT UNSIGNED NOT NULL,
    title VARCHAR(200) NOT NULL COMMENT 'Title',
    content VARCHAR(2000) NOT NULL COMMENT 'Content',
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP(),
    updated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP(),
    deleted_at DATETIME
);
```

2-3. Posts Table
```sql
CREATE TABLE posts(
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT UNSIGNED NOT NULL,
    title VARCHAR(50) NOT NULL COMMENT 'Title',
    content VARCHAR(2000) NOT NULL COMMENT 'Content',
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP(),
    updated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP(),
    deleted_at DATETIME
);
```
---
3. Alter Table Operations

3-1. Add Foreign Key
```sql
ALTER TABLE posts
ADD CONSTRAINT fk_posts_user_id
    FOREIGN KEY (user_id)
    REFERENCES users(id);
```
Explains: <br>
- Foreign keys (FK) enforce referential integrity between tables.<br>
- Cascading deletions are often handled in application code, not in DB. <br>
- (Use these ON DELETE & ON UPDATE to maintain a strong relationship between parent and child tables)

3-2. Drop Foreign Key
```sql
ALTER TABLE posts
DROP CONSTRAINT fk_posts_user_id;
```
3-3. Add Column
```sql
ALTER TABLE posts
ADD COLUMN image VARCHAR(100);
```
3-4. Drop Column
```sql
ALTER TABLE posts
DROP COLUMN image;
```
3-5. Modify Column (often used to increase a previously limited data size.)
```sql
ALTER TABLE users
MODIFY COLUMN gender VARCHAR(10) NOT NULL COMMENT 'Male, Female, Not Specified';
```
---
4. Auto-Increment Adjustment (try not to use if you don't want to make duplicate keys)
```sql
ALTER TABLE users AUTO_INCREMENT = 10;
```
---
5. Table Deletion
```sql
DROP TABLE posts;
DROP TABLE users;
```
6. Delete All Table Data (use carefully)
```sql
TRUNCATE TABLE posts;
TRUNCATE TABLE users;
```
