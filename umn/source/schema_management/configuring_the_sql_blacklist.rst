:original_name: ddm_03_0100.html

.. _ddm_03_0100:

Configuring the SQL Blacklist
=============================

Overview
--------

Configure a blacklist and add those statements to it to prevent the system executing some SQL statements.

Prerequisites
-------------

-  You have logged in to the DDM console.
-  A DDM instance is running properly and has available schemas.

Procedure
---------

#. In the instance list, locate the instance that contains schemas you require and click the instance name.
#. On the displayed page, choose **Schemas**.
#. In the schema list, locate the schema that you want to configure a blacklist for and click **Configure SQL Blacklist** in the **Operation** column.
#. In the displayed dialog box, click **Edit**, enter the required SQL statements or regular expressions in prefix match, full-text, and regular expression match boxes, and click **OK**.

   .. note::

      -  **Prefix Match**: Enter SQL statements that contain keywords such as DROP or DELETE and are not allowed by the current schema.
      -  **Full-text Match**: Enter full-text SQL statements that are not allowed by the current schema. Multiple spaces and line breaks will not be treated as if they were replaced or truncated as a single space.
      -  **Regular Expression Match**: Enter specific regular expressions that are not allowed by the current schema.
      -  Separate SQL statements in the blacklist with semicolons (;). The size of SQL statements for prefix match, full-text match, and regular expression match cannot exceed 1 KB, respectively.
      -  If you want to clear all the SQL statements in prefix match and full-text match areas, clear them separately and click **OK**.
