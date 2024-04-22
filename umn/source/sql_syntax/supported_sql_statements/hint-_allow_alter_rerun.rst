:original_name: ddm-08-0027.html

.. _ddm-08-0027:

HINT- ALLOW_ALTER_RERUN
=======================

**Command Format:**

**/*+ allow_alter_rerun=true*/**\ *<ALTER TABLE>*

**Description:**

Using this hint ensures that commands can be repeatedly executed, and no error is reported. This hint supports the following ALTER TABLE statements: ADD COLUMN, MODIFY COLUMN, DROP COLUMN, ADD INDEX, DROP INDEX, CHANGE COLUMN, ADD PARTITION, and DROP PARTITION.

Example:

**/*+ allow_alter_rerun=true*/ALTER TABLE aaa_tb ADD schoolroll varchar(128) not null comment 'Enrollment data'**
