:original_name: ddm_04_0028.html

.. _ddm_04_0028:

How Do I Handle Data with Duplicate Primary Keys in a Table?
============================================================

Scenario
--------

If there is already a primary key whose data type is a boundary value, in your DDM instance, duplicate primary keys will be reported when you insert a data record that is beyond the data range of the primary key.

Procedure
---------

#. Log in to the RDS console.
#. On the **Instances** page, locate the RDS for MySQL instance associated with your DDM instance and click the name of the RDS instance.
#. On the **Basic Information** page, choose **Parameters** in the left pane.
#. Click the **Parameters** tab and enter **sql_mode** in the text box. Then click the expanding button in the **Value** column, select **STRICT_ALL_TABLES** or **STRICT_TRANS_TABLES**, and click **Save**.

   .. note::

      **STRICT_ALL_TABLES** and **STRICT_TRANS_TABLES** are both strict modes. The strict mode controls how MySQL handles invalid or missing values.

      -  An invalid value might have the wrong data type for the column, or might be out of range.

      -  A value is missing when a new row to be inserted does not contain a value for a non-NULL column that has no explicit DEFAULT clause in its definition.

      -  If the DDM instance version is earlier than 2.4.1.3, do not set **sql_mode** to **ANSI_QUOTES**. If you set it to **ANSI_QUOTES**, double quotation marks used for each string will be translated into an identifier during SQL statement execution, making the string invalid.

         For example, **logic** in **select \* from test where tb = "logic"** cannot be parsed correctly.

      For more information about SQL modes, see `Server SQL Modes <https://dev.mysql.com/doc/refman/5.7/en/sql-mode.html>`__.

#. On the **Instances** page, restart the DDM instance.
