:original_name: ddm_03_0037.html

.. _ddm_03_0037:

Using Global Sequences in INSERT or REPLACE Statements
======================================================

You can use global sequences in INSERT or REPLACE statements to provide unique global sequence across schemas in a DDM instance. Generating sequence numbers with NEXTVAL and CURRVAL is supported in INSERT or REPLACE statements. For example, you can execute schema.seq.nextval and schema.seq.currval to obtain global sequence numbers. CURRVAL returns the current sequence number, and NEXTVAL returns the next one. If no schema is specified, use the global sequence of the currently connected schema.

Concurrently executing schema.seq.nextval in multiple sessions is supported to obtain unique global sequence numbers.

Prerequisites
-------------

-  There are two schemas **dml_test_1** and **dml_test_2**.

-  Both of them have table **test_seq**.

   Run the following command to create a table:

   **create table test_seq(col1 bigint,col2 bigint) dbpartition by hash(col1);**

Procedure
---------

#. Log in to the required DDM instance using a client.

#. Click the **dml_test_1** schema and run the following commands to create a global sequence:

   **use dml_test_1**;

   **create sequence seq_test**;

   |image1|

#. Run the following command to use the global sequence in an INSERT or REPLACE statement:

   **insert into test_seq(col1,col2)values(seq_test.nextval,seq_test.currval)**;

   |image2|

#. Click the **dml_test_2** schema, run the following commands to use the global sequence in an INSERT or REPLACE statement:

   **use dml_test_2**;

   **insert into test_seq(col1,col2)values(dml_test_1.seq_test.nextval,dml_test_1.seq_test.currval)**;

   |image3|

   The global sequence is created in schema **dml_test_1**. To use the global sequence in **schema dml_test_2**, you need to specify a schema name, for example, **dml_test_1.seq_test.nextval** or **dml_test_1.seq_test.currval**.

   .. note::

      -  Using global sequences in INSERT and REPLACE statements is supported only in sharded tables, but not in broadcast or unsharded tables.
      -  NEXTVAL and CURRVAL are executed from left to right in INSERT and REPLACE statements. If NEXTVAL is referenced more than once in a single statement, the sequence number is incremented for each reference.
      -  Each global sequence belongs to a schema. When you delete a schema, the global sequence of the schema is also deleted.

.. |image1| image:: /_static/images/en-us_image_0000001733146257.png
.. |image2| image:: /_static/images/en-us_image_0000001685147446.png
.. |image3| image:: /_static/images/en-us_image_0000001685307194.png
