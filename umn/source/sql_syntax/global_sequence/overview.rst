:original_name: ddm_12_0010.html

.. _ddm_12_0010:

Overview
========

Global sequences are mainly database-based global sequences.

.. note::

   -  The start auto-increment SN can be modified.
   -  Global sequence provides sequence numbers that are globally unique but may not increase continuously.

.. table:: **Table 1** Table types supported by global sequence

   ========== ========= ========= =============
   Table Type Sharded   Broadcast Unsharded
   ========== ========= ========= =============
   DB-based   Supported Supported Not supported
   ========== ========= ========= =============

Creating an Auto-Increment Sequence
-----------------------------------

#. Log in to the required DDM instance using a client.

#. Open the required schema.

#. Run the following command to create an auto-increment sequence:

   **create sequence** <seq_name>;

   .. note::

      -  *<seq_name>* indicates the sequence name.
      -  The auto-increment key should be a BIGINT value. To avoid duplicate values, do not use TINYINT, SMALLINT, MEDIUMINT, INTEGER, or INT as the auto-increment key.
      -  Run **show sequences** to view the usage of the auto-increment sequence. If the usage reaches 100%, do not insert data anymore.

Dropping an Auto-Increment Sequence
-----------------------------------

#. Log in to the required DDM instance using a client.

#. Open the required schema.

#. Run **show sequences** to view all global sequences.

#. Run the following command to drop an auto-increment sequence:

   **drop sequence** <seq_name> ;

   **drop sequence** *DB.*\ <seq_name>;

   .. note::

      -  The sequence name is case-insensitive.
      -  If an auto-increment sequence is inherent to a table, the sequence cannot be deleted.

Modifying the Start Value of an Auto-Increment Sequence
-------------------------------------------------------

#. Log in to the required DDM instance using a client.

#. Open the required schema.

#. Run **show sequences** to view all global sequences.

#. Run the command to change the start value:

   **alter sequence** <seq_name> **START WITH** <start_value>\ *;*

   .. note::

      -  *<seq_name>* indicates the sequence name.
      -  *<start_value>* indicates the start value of the target sequence.

Querying an Auto-Increment Sequence
-----------------------------------

#. Log in to the required DDM instance using a client.

#. Open the required schema.

#. Run **show sequences** to view all global sequences.

   **show sequences**;

   |image1|

Modifying the Auto-Increment Cache Value
----------------------------------------

.. important::

   This feature is only available in kernel 3.0.3 and later versions.

#. Log in to the required DDM instance using a client.
#. Open the required schema.
#. Run command **alter sequence test cache 5000** to modify the global sequence cache value of table **test**.
#. Run command **show sequences** to view the cache value (**INCREMENT** value) of table **test**.

Updating Auto-Increment Sequences of All Tables
-----------------------------------------------

.. important::

   This feature is available only in kernel 3.0.4.1 or later.

#. Log in to the required DDM instance using a client.
#. Run command **fresh all sequence start value** to change sequences of all schemas.

.. |image1| image:: /_static/images/en-us_image_0000001685307306.jpg
