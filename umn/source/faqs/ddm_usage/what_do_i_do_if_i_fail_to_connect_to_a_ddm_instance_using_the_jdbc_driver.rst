:original_name: ddm_04_0008.html

.. _ddm_04_0008:

What Do I Do If I Fail to Connect to a DDM Instance Using the JDBC Driver?
==========================================================================

When you access a DDM instance using the MySQL driver (JDBC) in load balancing mode, an infinite loop may occur during connection switchover, resulting in stack overflow.

Fault Locating
--------------

#. Query the application logs and locate the fault cause.

   For example, the following logs show that the fault is caused by stack overflow.

   .. code-block::

      Caused by: java.lang.StackOverflowError
           at java.nio.HeapByteBuffer.<init>(HeapByteBuffer.java:57)
           at java.nio.ByteBuffer.allocate(ByteBuffer.java:335)
           at java.nio.charset.CharsetEncoder.encode(CharsetEncoder.java:795)
           at java.nio.charset.Charset.encode(Charset.java:843)
           at com.mysql.jdbc.StringUtils.getBytes(StringUtils.java:2362)
           at com.mysql.jdbc.StringUtils.getBytes(StringUtils.java:2344)
           at com.mysql.jdbc.StringUtils.getBytes(StringUtils.java:568)
           at com.mysql.jdbc.StringUtils.getBytes(StringUtils.java:626)
           at com.mysql.jdbc.Buffer.writeStringNoNull(Buffer.java:670)
           at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2636)

#. Analyze the overflow source.

   For example, the following logs show that the overflow results from an infinite loop inside the driver.

   .. code-block::

      at com.mysql.jdbc.LoadBalancedConnectionProxy.pickNewConnection(LoadBalancedConnectionProxy.java:344)
      at com.mysql.jdbc.LoadBalancedAutoCommitInterceptor.postProcess(LoadBalancedAutoCommitInterceptor.java:104)
      at com.mysql.jdbc.MysqlIO.invokeStatementInterceptorsPost(MysqlIO.java:2885)
      at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2808)
      at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2483)
      at com.mysql.jdbc.ConnectionImpl.setReadOnlyInternal(ConnectionImpl.java:4961)
      at com.mysql.jdbc.ConnectionImpl.setReadOnly(ConnectionImpl.java:4954)
      at com.mysql.jdbc.MultiHostConnectionProxy.syncSessionState(MultiHostConnectionProxy.java:381)
      at com.mysql.jdbc.MultiHostConnectionProxy.syncSessionState(MultiHostConnectionProxy.java:366)
      at com.mysql.jdbc.LoadBalancedConnectionProxy.pickNewConnection(LoadBalancedConnectionProxy.java:344)

#. Query the MySQL version, which is 5.1.44.

   According to the source code of the version, when a connection is obtained, **LoadBalance** updates the connection based on the load balancing policy and copies the configurations of the old connection to the new connection. If **AutoCommit** is **true** for the new connection, parameters of the new connection are inconsistent with those of the old connection, and **loadBalanceAutoCommitStatementThreshold** is not configured, an infinite loop occurs. The connection update function calls the parameter synchronization function, and the parameter synchronization function calls the connection update function at the same time, resulting in stack overflow.

Solution
--------

Add the **loadBalanceAutoCommitStatementThreshold=5&retriesAllDown=10** parameter to the URL for connecting to the DDM instance.

.. code-block::

   //Connection example when load balancing is used
   //jdbc:mysql:loadbalance://ip1:port1,ip2:port2..ipN:portN/{db_name}
   String url = "jdbc:mysql:loadbalance://192.168.0.200:5066,192.168.0.201:5066/db_5133?loadBalanceAutoCommitStatementThreshold=5&retriesAllDown=10";

-  **loadBalanceAutoCommitStatementThreshold** indicates the number of statements executed before a reconnection.

   If **loadBalanceAutoCommitStatementThreshold** is set to **5**, a reconnection is initiated after five SQL statements (queries or updates) are executed. A value of **0** indicates a sticky connection, and no reconnection is required. When automatic submission is disabled (**autocommit** is set to **false**), the system waits for the transaction to complete and then determines whether to initiate a reconnection.
