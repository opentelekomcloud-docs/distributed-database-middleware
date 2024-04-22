:original_name: ddm_01_0174.html

.. _ddm_01_0174:

Unsupported Features and Limitations
====================================

Unsupported Features
--------------------

-  Stored procedures
-  Triggers
-  Views
-  Events
-  User-defined functions
-  Foreign key reference and association

-  Full-text indexes and SPACE functions
-  Temporary tables
-  Compound statements such as BEGIN...END, LOOP...END LOOP, REPEAT...UNTIL...END REPEAT, and WHILE...DO...END WHILE

-  Process control statements such as IF and WHILE
-  RESET and FLUSH statements

-  BINLOG statement
-  HANDLER statement

-  INSTALL and UNINSTALL PLUGIN statements
-  Character sets other than ASCII, Latin1, binary, utf8, and utf8mb4

-  SYS schema

-  Optimizer Trace
-  X-Protocol

-  CHECKSUM TABLE syntax
-  Table maintenance statements, including ANALYZE, CHECK, CHECKSUM, OPTIMIZE, and REPAIR TABLE

-  Statements for assigning a value to or querying variable **session**

   For example:

   .. code-block::

      set @rowid=0;select @rowid:=@rowid+1,id from user;

-  SQL statements that use -- or /.../ to comment out a single line or multiple lines of code

-  DDM provides incomplete support for system variable queries. The returned values are variable values of RDS instances, instead of DDM kernel variable values. For example, the returned values of SELECT @@autocommit do not indicate the current transaction status.
-  Executing SET syntax to modify global variables

-  PARTITION syntax. Partitioned tables are not recommended.
-  LOAD XML statement

Unsupported Operators
---------------------

-  Assignment operator (:=) is not supported.
-  Operator (->) is not supported. This operator can be executed successfully in a single table. An error is reported when this operator is executed in other types of tables.
-  Operator (->>) is not supported. This operator can be executed successfully in a single table. An error is reported when this operator is executed in other types of tables.
-  Expression IS UNKNOWN

Unsupported Functions
---------------------

The compute layer of DDM does not support the following functions:

-  XML functions
-  Function **ANY_VALUE()**
-  Function **ROW_COUNT()**
-  Function **COMPRESS()**
-  Function **SHA()**
-  Function **SHA1()**
-  Function **MD5()**
-  Function **AES_ENCRYPT()**
-  Function **AES_DECRYPT()**
-  Aggregate function **JSON_OBJECTAGG()**
-  Aggregate function **JSON_ARRAYAGG()**
-  Aggregate function **STD()**
-  Aggregate function **STDDEV()**
-  Aggregate function **STDDEV_POP()**
-  Aggregate function **STDDEV_SAMP()**
-  Aggregate function **VAR_POP()**
-  Aggregate function **VAR_SAMP()**
-  Aggregate function **VARIANCE()**

SQL Syntax
----------

**SELECT**

-  DISTINCTROW

-  Configuring options [HIGH_PRIORITY], [STRAIGHT_JOIN], [SQL_SMALL_RESULT], [SQL_BIG_RESULT], [SQL_BUFFER_RESULT], and [SQL_NO_CACHE] [SQL_CALC_FOUND_ROWS] in SELECT statements on DDM instances

-  SELECT ... GROUP BY ... WITH ROLLUP

-  SELECT ... ORDER BY ... WITH ROLLUP

-  WITH

-  Window functions

-  SELECT FOR UPDATE supports only simple queries and does not support statements such as JOIN, GROUP BY, ORDER BY, and LIMIT. Option [NOWAIT \| SKIP LOCKED] for modifying FOR UPDATE is invalid for DDM.

-  DDM does not support multiple columns with the same name for each SELECT statement in UNION. Duplicate column names are used in the following SELECT statement:

   .. code-block::

      SELECT id, id, name FROM t1 UNION SELECT pk, pk, name FROM t2;

**SORT and LIMIT**

-  LIMIT/OFFSET, value range: 0-2147483647

**Aggregation**

Function **asc** or **desc** cannot be used in the GROUP BY statement to sort out results.

.. note::

   -  DDM automatically ignores keyword **asc** or **desc** after GROUP BY.
   -  In MySQL versions earlier than 8.0.13, function **asc** or **desc** can be used in the GROUP BY statement to sort out results. In MySQL 8.0.13 or later, a syntax error is reported if you use function **asc** or **desc** this way. ORDER BY is recommended for sorting.

**Subqueries**

-  Subqueries that join grandparent queries are not supported.
-  Using subqueries in the HAVING clause and the JOIN ON condition is not supported.
-  Each derived table must have an alias.
-  A derived table cannot be a correlated subquery.

**LOAD DATA**

-  LOW_PRIORITY is not supported.
-  CONCURRENT is not supported.
-  PARTITION (partition_name [, partition_name] ...) is not supported.
-  LINES STARTING BY 'string' is not supported.
-  User-defined variables are not supported.
-  ESCAPED BY supports only '\\\\'.
-  If you have not specified a value for your auto-increment key when you insert a data record, DDM will not fill a value for the key. The auto-increment keys of data nodes of a DDM instance all take effect, so the auto-increment key values may be duplicate.
-  If the primary key or unique index is not routed to the same physical table, REPLACE does not take effect.
-  If the primary key or unique index is not routed to the same physical table, IGNORE does not take effect.

**INSERT and REPLACE**

-  INSERT DELAYED is not supported.

-  Only INSERT statements that contain sharding fields are supported.

-  PARTITION syntax is not supported. Partitioned tables are not recommended.

-  Setting **YYYY** of **datetime** (in the format of **YYYY-MM-DD HH:MM:SS**) to **1582** or any value smaller in INSERT statements is not supported.

-  Nesting a subquery in ON DUPLICATE KEY UPDATE of an INSERT statement is not supported. The following is an example:

   .. code-block::

      INSERT INTO t1(a, b)
      SELECT * FROM(SELECT c, d FROM t2 UNION SELECT e, f FROM t3) AS dt
      ON DUPLICATE KEY UPDATE b = b + c;

   Subquery c is used in the ON DUPLICATE KEY UPDATE clause.

-  The sharding key values in INSERT and REPLACE statements cannot be **DEFAULT**.

**UPDATE and DELETE**

-  Updating a sharding key value to **DEFAULT** is not supported.

-  Repeatedly updating the same field in one SQL statement is not supported.

-  Updating a sharding key using UPDATE JOIN is not supported. The following is an example:

   .. code-block::

      UPDATE tbl_1 a, tbl_2 b set a.name=b.name where a.id=b.id;

   **name** indicates the sharding key of table **tbl_1**.

-  Updating a sharding key by executing INSERT ON DUPLICATE KEY UPDATE is not supported.

-  Updating self-joins is not supported.

   .. code-block::

      UPDATE tbl_1 a, tbl_1 b set a.tinyblob_col=concat(b.tinyblob_col, 'aaabbb');

-  UPDATE JOIN supports only joins with WHERE conditions.

   The following is an example:

   .. code-block::

      UPDATE tbl_3, tbl_4 SET tbl_3.varchar_col='dsgfdg';

-  Referencing other object columns in assignment statements or expressions is not supported when UPDATE JOIN syntax is used. The following is an example:

   .. code-block::

      UPDATE tbl_1 a, tbl_2 b SET a.name=concat(b.name, 'aaaa'),b.name=concat(a.name, 'bbbb') ON a.id=b.id;

-  You can update a sharding field by two steps: delete the original sharding field and then insert a new field. During this process, the results of querying the sharding fields involved in the target table may be inconsistent.

**DDL**

-  SQL statements for modifying database names and sharding field names and types
-  SQL statements for creating and deleting schemas
-  Index FULL_TEXT
-  AS SELECT clause of the CREATE TABLE statement
-  CREATE TABLE ... LIKE statement
-  Dropping multiple tables with one SQL statement
-  Executing multiple SQL statements at the same time
-  Creating foreign keys for broadcast and sharded tables
-  Creating tables whose names are prefixed by **\_ddm**
-  Creating temporary sharded or broadcast tables
-  Specifying globally unique keys in the CREATE TABLE statement

Indexes
-------

-  Global secondary indexes
-  Global unique indexes. Unique keys and primary keys may not be globally unique.

Table Recycle Bins
------------------

-  Hints
-  Deleting tables by schema
-  Deleting tables by logical table
-  After a table is recovered, its globally unique sequence increases automatically but may not follow the last sequence value.
-  Shard configuration
-  Retaining copies with no time limit
-  Recovering data to a table with any name
-  Unlimited copies

Transactions
------------

-  Savepoints
-  XA syntax. DDM has implemented distributed transactions through XA, so the user layer does not need to process the syntax.
-  Customizing the isolation level of a transaction. Currently, DDM supports only the READ COMMITTED isolation level. In consideration of compatibility, DDM does not report errors for any SQL statement (such as SET GLOBAL TRANSACTION ISOLATION LEVEL REPEATABLE READ) to set the database isolation level, but will ignore the modifications to the transaction isolation level.
-  Setting a transaction to read-only (START TRANSACTION READ ONLY). DDM can enable read/write of a transaction, instead of enabling read-only, to ensure compatibility.

Permissions
-----------

-  Column-level permissions
-  Subprogram-level permissions

Database Management Statements
------------------------------

-  SHOW TRIGGERS
-  Most of SHOW statements such as SHOW PROFILES, SHOW ERRORS, and SHOW WARNINGS
-  The following SHOW statements are randomly sent to a database shard. If database shards are on different RDS for MySQL instances, the returned variables or table information may be different.

   -  SHOW TABLE STATUS;
   -  SHOW VARIABLES Syntax;
   -  SHOW WARNINGS Syntax does not support the combination of LIMIT and COUNT.
   -  SHOW ERRORS Syntax does not support the combination of LIMIT and COUNT.

INFORMATION_SCHEMA
------------------

-  Only simple queries of SCHEMATA, TABLES, COLUMNS, STATISTICS, and PARTITIONS are supported. No subqueries, JOINs, aggregate functions, ORDER BY, and LIMIT are allowed.

Broadcast Tables
----------------

If a broadcast table is used, do not use any function that has different results returned each time it is executed. Otherwise, data inconsistency will occur between different shards. If such functions are indeed required, calculate their results, write the results to your SQL statements, and then execute the SQL statements on the broadcast table. Functions of this type include but are not limited to the following:

-  CONNECTION_ID()
-  CURDATE()
-  CURRENT_DATE()
-  CURRENT_TIME()
-  CURRENT_TIMESTAMP()
-  CURTIME()
-  LAST_INSERT_ID()
-  LOCALTIME()
-  LOCALTIMESTAMP()
-  NOW()
-  UNIX_TIMESTAMP()
-  UTC_DATE()
-  UTC_TIME()
-  UTC_TIMESTAMP()
-  CURRENT_ROLE()
-  CURRENT_USER()
-  FOUND_ROWS()
-  GET_LOCK()
-  IS_FREE_LOCK()
-  IS_USED_LOCK()
-  JSON_TABLE()
-  LOAD_FILE()
-  MASTER_POS_WAIT()
-  RAND()
-  RELEASE_ALL_LOCKS()
-  RELEASE_LOCK()
-  ROW_COUNT()
-  SESSION_USER()
-  SLEEP()
-  SYSDATE()
-  SYSTEM_USER()
-  USER()
-  UUID()
-  UUID_SHORT()
