- 登入
  ```
  root@186e495b9fdd:~# psql -U postgres
  psql (11.11 (Debian 11.11-1.pgdg90+1))
  Type "help" for help.

  postgres=#
  ```

- 建立資料表

    ```
      CREATE TABLE COMPANY(
     ID INT PRIMARY KEY     NOT NULL,
     NAME           TEXT    NOT NULL,
     AGE            INT     NOT NULL,
     ADDRESS        CHAR(50),
     SALARY         REAL
    );

    CREATE TABLE DEPARTMENT(
     ID INT PRIMARY KEY      NOT NULL,
     DEPT           CHAR(50) NOT NULL,
     EMP_ID         INT      NOT NULL
    );
    ```

- 列出資料表

    ```
    postgres=# \d
               List of relations
     Schema |    Name    | Type  |  Owner
    --------+------------+-------+----------
     public | company    | table | postgres
     public | department | table | postgres
    (2 rows)
    ```

- 列出資料表結構

    ```
    postgres=# \d company
                      Table "public.company"
     Column  |     Type      | Collation | Nullable | Default
    ---------+---------------+-----------+----------+---------
     id      | integer       |           | not null |
     name    | text          |           | not null |
     age     | integer       |           | not null |
     address | character(50) |           |          |
     salary  | real          |           |          |
    Indexes:
        "company_pkey" PRIMARY KEY, btree (id)
    ```

- 新增單筆資料

    ```
    INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) VALUES (1, 'Paul', 32, 'California', 20000.00);
    ```

- 新增多筆資料

    ```
    INSERT INTO COMPANY (ID,NAME,AGE,ADDRESS,SALARY) VALUES (4, 'Mark', 25, 'Rich-Mond ', 65000.00 ), (5, 'David', 27, 'Texas', 85000.00);
    ```

- 查詢資料

    ```
    postgres=# SELECT * FROM COMPANY;
     id | name  | age |                      address                       | salary
    ----+-------+-----+----------------------------------------------------+--------
      1 | Paul  |  32 | California                                         |  20000
      4 | Mark  |  25 | Rich-Mond                                          |  65000
      5 | David |  27 | Texas                                              |  85000
    (3 rows)
    ```

- 刪除指定資料

    ```
    postgres=# DELETE FROM COMPANY WHERE id = 4;
    DELETE 1
    postgres=# SELECT * FROM COMPANY;
     id | name  | age |                      address                       | salary
    ----+-------+-----+----------------------------------------------------+--------
      1 | Paul  |  32 | California                                         |  20000
      5 | David |  27 | Texas                                              |  85000
    (2 rows)
    ```

- 更改指定的資料

    ```
    postgres=# UPDATE COMPANY SET age = 25 WHERE id = 5;
    UPDATE 1
    postgres=# SELECT * FROM COMPANY;
     id | name  | age |                      address                       | salary
    ----+-------+-----+----------------------------------------------------+--------
      1 | Paul  |  32 | California                                         |  20000
      5 | David |  25 | Texas                                              |  85000
    (2 rows)
    ```

- 更改資料表的結構，新增欄位

    ```
    postgres=#  ALTER TABLE COMPANY ADD join_date date;
    ALTER TABLE
    postgres=# \d company
                       Table "public.company"
      Column   |     Type      | Collation | Nullable | Default
    -----------+---------------+-----------+----------+---------
     id        | integer       |           | not null |
     name      | text          |           | not null |
     age       | integer       |           | not null |
     address   | character(50) |           |          |
     salary    | real          |           |          |
     join_date | date          |           |          |
    Indexes:
        "company_pkey" PRIMARY KEY, btree (id)
    ```

- 更改資料表的結構，刪除欄位

    ```
    postgres=#     ALTER TABLE COMPANY DROP join_date;
    ALTER TABLE
    postgres=# \d company
                      Table "public.company"
     Column  |     Type      | Collation | Nullable | Default
    ---------+---------------+-----------+----------+---------
     id      | integer       |           | not null |
     name    | text          |           | not null |
     age     | integer       |           | not null |
     address | character(50) |           |          |
     salary  | real          |           |          |
    Indexes:
        "company_pkey" PRIMARY KEY, btree (id)
    ```

- 刪除資料表

    ```
    postgres=#  DROP TABLE company;
    DROP TABLE
    postgres=# \d
               List of relations
     Schema |    Name    | Type  |  Owner
    --------+------------+-------+----------
     public | department | table | postgres
    (1 row)
    ```

