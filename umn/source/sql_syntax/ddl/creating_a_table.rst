:original_name: ddm_08_0029.html

.. _ddm_08_0029:

Creating a Table
================

.. note::

   -  Do not create tables whose names start with **\_ddm**. DDM manages such tables as internal tables by default
   -  Sharded tables do not support globally unique indexes. If the unique key is different from the sharding key, data uniqueness cannot be ensured.
   -  The auto-increment key should be a BIGINT value. To avoid duplicate values, do not use TINYINT, SMALLINT, MEDIUMINT, INTEGER, or INT as the auto-increment key.

Database and Table Sharding
---------------------------

The following is an example statement when HASH is used for database sharding and MOD_HASH for table sharding:

.. code-block::

   CREATE TABLE tbpartition_tb1 (
   id bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary key id',
   name varchar(128),
   PRIMARY KEY(id)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci
   DBPARTITION BY HASH(id)
   TBPARTITION BY MOD_HASH(name) tbpartitions 8;

Database Sharding
-----------------

The following is an example statement when HASH is used:

.. code-block::

   CREATE TABLE dbpartition_tb1 (
   id bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary key id',
   name varchar(128),
   PRIMARY KEY(id)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci
   DBPARTITION BY HASH(id);

Creating a Broadcast Table
--------------------------

The following is an example statement:

.. code-block::

   CREATE TABLE broadcast_tb1 (
   id bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary key id',
   name varchar(128),
   PRIMARY KEY(id)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci
   BROADCAST;

Creating a Table When Sharding Is not Used
------------------------------------------

A global sequence can also be specified for an unsharded table, but this function is always ignored. An unsharded table provides auto-increment using auto-increment values of corresponding physical tables.

The following is an example statement:

.. code-block::

   CREATE TABLE single_tb1 (
   id bigint NOT NULL AUTO_INCREMENT COMMENT 'Primary key id',
   name varchar(128),
   PRIMARY KEY(id)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
