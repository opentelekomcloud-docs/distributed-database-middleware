:original_name: ddm_02_0005.html

.. _ddm_02_0005:

Step 4: Log In to the DDM Schema
================================

After you create a DDM instance, you can log in to it using a client such as Navicat, or connect to the required schema in the instance using the CLI or JDBC driver.

This section describes how to log in to a DDM instance or a schema.

Preparations
------------

Before you log in to your DDM instance or schema, you have to obtain its connection address.

Obtaining the Schema Connection Address
---------------------------------------

#. Log in to the DDM console.
#. Hover on the left menu to display **Service List** and choose **Databases** > **Distributed Database Middleware**.
#. In the navigation pane, choose **Instances**. In the instance list, locate the required DDM instance and click its name.
#. In the navigation pane, choose **Schemas**.
#. In the schema list, locate the required schema and click its name.
#. In the **Connection Address** area, view CLI and JDBC connection addresses.

   .. note::

      -  If load balancing is enabled, one floating IP address will be assigned to a DDM instance even if it has multiple nodes. You can use this address to connect to the DDM instance for load balancing.
      -  There are some historical instances that do not support load balancing, so they have multiple IP addresses. For load balancing, you can use JDBC connection strings to connect to them.
      -  If read-only groups are created, each group will be assigned a load balancing address for service isolation.

Connection Methods
------------------

For details about method 1, see :ref:`Using Navicat to Log In to a DDM Instance <ddm_02_0005__section19691512121812>`.

For details about method 2, see :ref:`Using the MySQL CLI to Log In to a Schema <ddm_02_0005__section1621624581510>`.

For details about method 3, see :ref:`Using a JDBC Driver to Log In to a Schema <ddm_02_0005__section1690417388176>`.

.. note::

   #. For security purposes, select an ECS in the same VPC as your DDM instance.
   #. Ensure that a MySQL client has been installed on the required ECS or the MySQL connection driver has been configured.
   #. Before you log in to a DDM instance, configure its information on the client or connection driver.

.. _ddm_02_0005__section19691512121812:

Using Navicat to Log In to a DDM Instance
-----------------------------------------

#. Log in to the DDM console, locate the required DDM instance, and click its name.
#. Ask technical support to add an EIP to the feature whitelist. In the **Instance Information** area, click **Bind**. In the displayed dialog box, select the EIP and click **OK**. Bind the EIP with your DDM instance.
#. In the navigation pane on the left, click the VPC icon and choose **Access Control** > **Security Groups**.
#. On the **Security Groups** page, locate the required security group and click **Manage Rule** in the **Operation** column. On the displayed page, click **Add Rule**. Configure the security group rule as needed and click **OK**.

   .. note::

      After binding an EIP to your DDM instance, set strict inbound and outbound rules for the security group to enhance database security.

#. Open Navicat and click **Connection**. In the displayed dialog box, enter the host IP address (EIP), username, and password (DDM account).

   .. note::

      Navicat12 is recommended for Navicat clients.

#. Click **Test Connection**. If a message is returned indicating that the connection is successful, click **OK**. The connection will succeed 1 to 2 minutes later. If the connection fails, the failure cause is displayed. Modify the required information and try again.

.. note::

   Using Navicat to access a DDM instance is similar to using other visualized MySQL tools such as MySQL Workbench. Therefore, the procedure of using other visualized MySQL tools to connect to a DDM instance has been omitted.

.. _ddm_02_0005__section1621624581510:

Using the MySQL CLI to Log In to a Schema
-----------------------------------------

#. Log in to the required ECS, open the CLI, and run the following command:

   .. code-block::

      mysql -h ${DDM_SERVER_ADDRESS} -P ${DDM_SERVER_PORT} -u ${DDM_USER} -p [-D ${DDM_DBNAME}] [--default -character -set=utf8][--default_auth=mysql_native_password] [--ssl]

   .. table:: **Table 1** Parameter description

      +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter                          | Description                                                                                                                                            | Example Value         |
      +====================================+========================================================================================================================================================+=======================+
      | DDM_SERVER_ADDRESS                 | IP address of the DDM instance                                                                                                                         | 192.168.0.200         |
      +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | DDM_SERVER_PORT                    | Connection port of the DDM instance                                                                                                                    | 5066                  |
      +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | DDM_USER                           | Account of the DDM instance                                                                                                                            | dbuser01              |
      +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | DDM_DBNAME                         | (Optional) Name of the target schema in the DDM instance                                                                                               | ``-``                 |
      +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | default-character-set=utf8         | (Optional) Select character set UTF-8 for encoding.                                                                                                    | ``-``                 |
      |                                    |                                                                                                                                                        |                       |
      |                                    | Configure this parameter if garbled characters are displayed during parsing due to inconsistency between MySQL connection code and actually used code. |                       |
      +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | default_auth=mysql_native_password | (Optional) The password authentication plug-in is used by default.                                                                                     | ``-``                 |
      |                                    |                                                                                                                                                        |                       |
      |                                    | If you use the MySQL 8.0 client, this parameter is required.                                                                                           |                       |
      +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | ssl                                | (Optional) To use SSL to encrypt connections, you need to enable SSL first.                                                                            | ``-``                 |
      |                                    |                                                                                                                                                        |                       |
      |                                    | If you have enabled SSL, encrypted connections are used by default.                                                                                    |                       |
      +------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

#. View the command output. The following is an example output of running a MySQL command in the Windows CLI.

   .. code-block::

      C:\Users\testDDM>mysql -h 192.168.0.200 -P 5066 -D db_5133 -u dbuser01 -p
      Enter password:
      Reading table information for completion of table and column names
      You can turn off this feature to get a quicker startup with -A

      Welcome to the MySQL monitor.  Commands end with ;or \g.
      Your MySQL connection id is 5
      Server version: 5.6.29

      Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

      Oracle is a registered trademark of Oracle Corporation and/or its
      affiliates. Other names may be trademarks of their respective
      owners.

      Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

      mysql>

.. _ddm_02_0005__section1690417388176:

Using a JDBC Driver to Log In to a Schema
-----------------------------------------

#. Load the required JDBC driver.

   .. code-block::

      Class.forname(com.mysql.jdbc.Driver);

   .. note::

      JDBC drivers 5.1.49 or later are recommended.

#. Create a database connection.

   .. code-block::

      String username = "dbuser01" ;
      String password = "xxxxxx" ;
      String url = "jdbc:mysql://192.168.0.200:5066/db_5133";
      Connection con = DriverManager.getConnection(url , username , password);

#. Create a Statement object.

   .. code-block::

      Statement stmt = con.createStatement();

#. Execute the required SQL statement.

   .. code-block::

      ResultSet rs = stmt.executeQuery("select now() as Systemtime");
      con.close();

#. .. _ddm_02_0005__li139111931387:

   (Optional) Optimize code as needed.

   .. code-block::

      loadBalanceAutoCommitStatementThreshold=5&loadBalanceHostRemovalGracePeriod=15000&loadBalanceBlacklistTimeout=60000&loadBalancePingTimeout=5000&retriesAllDown=10&connectTimeout=10000&useSSL=true;

   .. note::

      -  Parameters **loadBalanceAutoCommitStatementThreshold** and **retriesAllDown** must be configured based on the example in :ref:`5 <ddm_02_0005__li139111931387>`. Otherwise, an infinite loop may occur during the connection switchover, resulting in stack overflow.
      -  **loadBalanceAutoCommitStatementThreshold**: defines the number of matching statements which will trigger the driver to potentially swap physical server connections.
      -  **loadBalanceHostRemovalGracePeriod**: indicates the grace period to wait for a host being removed from a load-balanced connection, to be released when it is the active host.
      -  **loadBalanceBlacklistTimeout**: indicates the time in milliseconds between checks of servers which are unavailable, by controlling how long a server lives in the global blacklist.
      -  **loadBalancePingTimeout**: indicates the time in milliseconds that the connection will wait for a response to a ping operation when you set **loadBalanceValidateConnectionOnSwapServer** to **true**.
      -  **retriesAllDown**: indicates the maximum number of connection attempts before an exception is thrown when a valid host is searched. SQLException will be returned if the threshold of retries is reached with no valid connections obtained.
      -  **connectTimeout**: indicates the maximum amount of time in milliseconds that the JDBC driver is willing to wait to set up a socket connection. **0** indicates that the connection does not time out. This parameter is available to JDK-1.4 or later versions. The default value is **0**.
      -  **useSSL**: indicates that an SSL connection is used to connect to DDM. This parameter is set to **true** by default.
