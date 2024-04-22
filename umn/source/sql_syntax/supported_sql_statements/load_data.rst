:original_name: ddm_03_0031.html

.. _ddm_03_0031:

LOAD DATA
=========

Standard Example
----------------

LOAD DATA LOCAL INFILE '/data/data.txt' IGNORE INTO TABLE test CHARACTER SET 'utf8' FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"' LINES TERMINATED BY '\\n' (id, sid, asf);

.. note::

   If a data field contains special characters like separators and escapes, execute OPTIONALLY ENCLOSED BY '"' to enclose the field with double quotation marks ("").

   Example:

   The following data field contains separators (,) and is enclosed with quotation marks:

   **"aab,,,bba,ddd"**

   If a data field contains quotation marks, the preceding method may not work. You can add a backslash (\\) before each quotation mark (") in the field, for example, **"aab,,,bba,ddd\\"ddd\\"bb,ae"**.

-  If keyword **LOCAL** is specified, the file is read from the client host. If keyword **LOCAL** is not specified, this function is not supported for security purposes.
-  You can use **FIELDS TERMINATED BY** to specify a separator between characters. The default value is **\\t**.
-  You can use **OPTIONALLY ENCLOSED BY** to ignore symbols in the data source fields.
-  You can use **LINES TERMINATED BY** to specify a newline character between lines. The default value is **\\n**.

   .. note::

      On some hosts running the Windows OS, the newline character of text files may be **\\r\\n**. The newline character is invisible, so you may need to check whether it is there.

-  You can use **CHARACTER SET** to specify a file code that should be the same as the code used by physical databases in the target RDS for MySQL instance, to avoid garbled characters. The character set code shall be enclosed in quotation marks to avoid parsing errors.
-  You can use **IGNORE** or **REPLACE** to specify whether repeated records are replaced or ignored.
-  Currently, the column name must be specified, and the sharding field must be included. Otherwise, the route cannot be determined.
-  For other parameters, see the `LOAD DATA INFILE Syntax <https://dev.mysql.com/doc/refman/8.0/en/load-data.html>`__ on the MySQL official website. The sequence of other parameters must be correct. For more information, visit `the MySQL official website <https://dev.mysql.com/doc/refman/8.0/en/load-data.html>`__.

.. important::

   #. Importing data affects performance of DDM instances and RDS for MySQL instances. Import data during off-peak hours.

   #. Do not to send multiple LOAD DATA requests at the same time. If you do so, SQL transactions may time out due to highly concurrent data write operations, table locking, and system I/O occupation, resulting in failure of all LOAD DATA requests.

   #. Manually submit transactions when using LOAD DATA to import data so that data records are modified correctly.

      For example, configure your client as follows:

      **mysql> set autocommit=0;**

      **mysql>** **LOAD DATA LOCAL INFILE** '/data/data.txt' **IGNORE INTO TABLE** **test CHARACTER SET** **'utf8' FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"' LINES TERMINATED BY '\\n' (id, sid, asf);**

      **mysql> commit;**

Use Constraints
---------------

There are the following constraints on LOAD DATA syntax.

-  LOW_PRIORITY is not supported.
-  CONCURRENT is not supported.
-  PARTITION (partition_name [, partition_name] ...) is not supported.
-  LINES STARTING BY 'string' is not supported.
-  User-defined variables are not supported.
-  ESCAPED BY supports only '\\\\'.
-  If you have not specified a value for your auto-increment key when you insert a data record, DDM will not fill a value for the key. The auto-increment keys of data nodes of a DDM instance all take effect, so the auto-increment key values may be duplicate.
-  If the primary key or unique index is not routed to the same physical table, REPLACE does not take effect.
-  If the primary key or unique index is not routed to the same physical table, IGNORE does not take effect.
