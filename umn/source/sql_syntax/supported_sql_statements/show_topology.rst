:original_name: ddm_08_0017.html

.. _ddm_08_0017:

SHOW TOPOLOGY
=============

**Command Format:**

**show topology from** *<table_name>*;

It is used to view physical tables corresponding to a specified logical table.

**Output Details:**

**RDS_instance_id**: indicates the ID of the RDS instance.

**HOST**: indicates the IP address of the RDS instance.

**PORT**: indicates the port number of the RDS instance.

**DATABASE**: indicates the physical database in the RDS instance.

**TABLE**: indicates the physical table.

**ROW_COUNT**: indicates the estimated number of data entries in each physical table. The value is obtained from information_schema.TABLES.
