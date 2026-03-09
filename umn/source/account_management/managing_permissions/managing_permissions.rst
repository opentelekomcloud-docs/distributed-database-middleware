:original_name: ddm_12_0004.html

.. _ddm_12_0004:

Managing Permissions
====================

Permission Levels
-----------------

-  User level (supported)
-  Database level (supported)
-  Table level (supported)
-  Column level (not supported)
-  Subprogram level (not supported)
-  Global level (not supported)

Permission Types
----------------

DDM supports different permission types by using the GRANT statement.

=============== ==========================================
Permission Type Description
=============== ==========================================
ALL             All permissions
DROP            Deleting a table
INDEX           Creating/Deleting an index
ALTER           Executing ALTER statements
CREATE          Creating a table
SELECT          Reading table data
INSERT          Inserting data to a table
UPDATE          Updating data in a table
GRANT           Granting permissions to users
REVOKE          Deleting a user permission
SET             Setting user's passwords
FILE            Uploading database permissions from a file
CREATE USER     Creating a user
=============== ==========================================

Precautions
-----------

-  Basic permissions of a DDM account can only be modified on the DDM console.
-  If a DDM account has table or database permissions on a schema, the schema will be displayed in the row where the account is located.
-  Users created by the CREATE USER statement support only user-level permissions.
-  If a DDM account has been associated with a schema, deleting this schema or tables in it does not affect the permissions assigned to the account.
-  Permissions cannot be assigned to a DDM account created on the management and control plane unless the account is associated with a schema.

Permission Operations
---------------------

.. important::

   SHOW GRANTS is supported in versions in 3.0.2 or later. Other functions are available in versions 2.4.1.4 or later.

**CREATE USER**

Syntax:

.. code-block::

   CREATE USER username IDENTIFIED BY 'password';

Example: **Creating an account (whose name is Jenny and whose password is changed from xxxxxx to a custom one)**

.. code-block::

   CREATE USER Jenny IDENTIFIED BY 'xxxxxx';

.. note::

   Each username and password must meet the corresponding requirements.

**DROP USER**

Syntax:

.. code-block::

   DROP USER username

Example: **Removing user1**

.. code-block::

   DROP USER user1;

**SET PASSWORD**

Syntax:

.. code-block::

   SET PASSWORD FOR 'username'@'%' = 'password'

.. note::

   To be compatible with the MySQL syntax, the username must be in the format of 'username'@'%'.

Example: **Changing the password of Jenny**

.. code-block::

   SET PASSWORD FOR 'Jenny'@'%' = 'new_password'

**GRANT**

Syntax:

.. code-block::

   GRANT
      priv_type[, priv_type] ...
      ON priv_level
      TO user [auth_option]
      priv_level: {
          | *.*
          | db_name.*
          | db_name.tbl_name
          | tbl_name}
      auth_option: {
          IDENTIFIED BY 'password'
   }

.. note::

   If a GRANT statement provides no accounts and does not specify **IDENTIFIED BY**, a message **No account found** will be returned. If **IDENTIFIED BY** is specified, an account will be created accordingly and permissions will be granted to it.

   GRANT ALL [PRIVILEGES] can be used to assign table-, user-, and database-level permissions.

Example 1: Create a user-level account with all permissions. The username is **user2**.

Method 1: Create an account and then grant permissions to it.

.. code-block::

   CREATE USER user2 IDENTIFIED BY 'password';
   GRANT SELECT, INSERT ON *.* to user2;

Method 2: Use one SQL statement to create an account and grant it permissions.

.. code-block::

   GRANT SELECT, INSERT ON *.* to user2 IDENTIFIED BY 'password';

Example 2: Create a database-level account with all permissions. Create account **user3** in database **testdb** and grant the SELECT permissions of database **testdb** to the account.

Method 1: Create an account and then grant permissions to it.

.. code-block::

   CREATE USER user3 IDENTIFIED BY 'password';
   GRANT SELECT ON testdb.* to user3;

Method 2: Use one SQL statement to create an account and grant it permissions.

.. code-block::

   GRANT SELECT ON testdb.* to user3 IDENTIFIED BY 'password';

Example 3: Create a table-level account with all permissions. Create account **user4** in database **testdb** and grant all permissions of table **testdb.employees** to the account.

.. code-block::

   GRANT  ALL PRIVILEGES ON testdb.employees to user4 IDENTIFIED BY 'password';

**REVOKE**

Syntax:

.. code-block::

   REVOKE
       priv_type [, priv_type] ...
       ON priv_level FROM user;

Example: Deleting CREATE, DROP, and INDEX permissions of user **user4** on table **testdb.emp**.

.. code-block::

   REVOKE CREATE,DROP,INDEX ON testdb.emp FROM user4;

.. note::

   REVOKE can delete actions at each permission level of an account. The permission level is specified by **priv_level**.

**SHOW GRANTS**

Syntax:

.. code-block::

   SHOW GRANTS FOR username;

Example 1: Querying user permissions with any of the following statements:

.. code-block::

   SHOW GRANTS;
   SHOW GRANTS FOR CURRENT_USER;
   SHOW GRANTS FOR CURRENT_USER();


.. figure:: /_static/images/en-us_image_0000002454002032.png
   :alt: **Figure 1** Viewing the permissions of the current user

   **Figure 1** Viewing the permissions of the current user

Example 2: Querying other permissions. This operation can be performed only when the current user can grant user-level permissions.

.. code-block::

   mysql> show grants for user4;
   +-----------------------------+
   |Grants for user4            |
   +-----------------------------+
   |GRANT USAGE ON *.* TO user4 |
   +-----------------------------+
   1 row in set (0.00 sec)
