# MySql


- ANALYZE TABLE users;


Index
```
CREATE TABLE EMPLOYEE (
    first_name varchar(40) not null,
    last_name varchar(40) not null,
    department varchar(40) not null,
    joining_date date not null
);
INSERT INTO EMPLOYEE (first_name, last_name, department, joining_date) VALUES ('Jaxon', 'Armstrong', 'Engineering', '2005-05-20');
INSERT INTO EMPLOYEE (first_name, last_name, department, joining_date) VALUES ('Donna', 'Mckee', 'Sales', '2015-08-02');
INSERT INTO EMPLOYEE (first_name, last_name, department, joining_date) VALUES ('Donna', 'Walton', 'Finance', '2005-01-10');
INSERT INTO EMPLOYEE (first_name, last_name, department, joining_date) VALUES ('Donna', 'Hardy', 'Engineering', '2023-05-20');
INSERT INTO EMPLOYEE (first_name, last_name, department, joining_date) VALUES ('Donna', 'Benton', 'Product', '2010-07-28');
INSERT INTO EMPLOYEE (first_name, last_name, department, joining_date) VALUES ('Donna', 'Sawyer', 'Sales', '2005-03-29');
INSERT INTO EMPLOYEE (first_name, last_name, department, joining_date) VALUES ('Donna', 'Schaefer', 'Finance', '2019-01-18');
INSERT INTO EMPLOYEE (first_name, last_name, department, joining_date) VALUES ('Donna', 'Bauer', 'Engineering', '2020-09-14');
INSERT INTO EMPLOYEE (first_name, last_name, department, joining_date) VALUES ('Tomas', 'Pennington', 'Engineering', '2019-05-20');

CREATE INDEX FN_IN ON EMPLOYEE(first_name);
CREATE INDEX DEP_IN ON EMPLOYEE(department);
CREATE INDEX JD_IN ON EMPLOYEE(joining_date);

or

ALTER TABLE EMPLOYEE
    ADD INDEX FN_IN(first_name),
    ADD INDEX DEP_IN(department),
    ADD INDEX JD_IN(joining_date)
;

DROP INDEX FN_IN ON EMPLOYEE;
DROP INDEX DEP_IN ON EMPLOYEE;
DROP INDEX JD_IN ON EMPLOYEE;

>Get list of all index in DB
DELIMITER $$
CREATE PROCEDURE GetAllIndexesINDB(IN dbName VARCHAR(64))
BEGIN
    -- Ensure that the database name is not null or empty
    IF dbName IS NOT NULL AND dbName != '' THEN
        -- Query to retrieve index information
        SELECT
            *
        FROM
            INFORMATION_SCHEMA.STATISTICS
        WHERE
            TABLE_SCHEMA = dbName
        ORDER BY
            TABLE_NAME, INDEX_NAME, SEQ_IN_INDEX;
    ELSE
        -- Error message if the database name is invalid
        SELECT 'Invalid database name' AS ErrorMessage;
    END IF;
END $$
DELIMITER ;

>Query
>CALL GetAllIndexesINDB('explore');

>DROP  PROCEDURE GetAllIndexesINDB;

Create a temporary table to do more analysis on indexing
CREATE TABLE MY_INDEXS (
    TABLE_CATALOG VARCHAR(255),
    TABLE_SCHEMA VARCHAR(255),
    TABLE_NAME VARCHAR(255),
    NON_UNIQUE TINYINT,
    INDEX_SCHEMA VARCHAR(255),
    INDEX_NAME VARCHAR(255),
    SEQ_IN_INDEX INT,
    COLUMN_NAME VARCHAR(255),
    COLLATION CHAR(1),
    CARDINALITY INT,
    SUB_PART INT,
    PACKED VARCHAR(10),
    NULLABLE VARCHAR(3),
    INDEX_TYPE VARCHAR(16),
    COMMENT VARCHAR(255),
    INDEX_COMMENT VARCHAR(255),
    IS_VISIBLE VARCHAR(3),
    EXPRESSION TEXT
);

> SELECT DISTINCT INDEX_TYPE FROM MY_INDEXS;
> SELECT * FROM MY_INDEXS GROUP BY TABLE_NAME;
> SELECT * FROM MY_INDEXS WHERE TABLE_NAME='users';
```
