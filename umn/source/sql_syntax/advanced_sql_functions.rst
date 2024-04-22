:original_name: ddm_03_0035.html

.. _ddm_03_0035:

Advanced SQL Functions
======================

.. table:: **Table 1** Restrictions on advanced SQL functions

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Item                              | Restriction                                                                                                                             |
   +===================================+=========================================================================================================================================+
   | SQL functions                     | -  PREPARE and EXECUTE syntax is not supported.                                                                                         |
   |                                   |                                                                                                                                         |
   |                                   | -  Customized data types and functions are not supported.                                                                               |
   |                                   |                                                                                                                                         |
   |                                   | -  Views, stored procedures, triggers, and cursors are not supported.                                                                   |
   |                                   |                                                                                                                                         |
   |                                   | -  Compound statements such as BEGIN...END, LOOP...END LOOP, REPEAT...UNTIL...END REPEAT, and WHILE...DO...END WHILE are not supported. |
   |                                   |                                                                                                                                         |
   |                                   | -  Process control statements such as IF and WHILE are not supported.                                                                   |
   |                                   |                                                                                                                                         |
   |                                   | -  The following prepared statements are not supported:                                                                                 |
   |                                   |                                                                                                                                         |
   |                                   |    **PREPARE**\  Syntax                                                                                                                 |
   |                                   |                                                                                                                                         |
   |                                   |    **EXECUTE**\  Syntax                                                                                                                 |
   |                                   |                                                                                                                                         |
   |                                   | -  Comments for indexes are not supported in table creation statements.                                                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
