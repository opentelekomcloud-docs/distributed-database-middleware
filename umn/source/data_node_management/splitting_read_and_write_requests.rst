:original_name: ddm_06_0012.html

.. _ddm_06_0012:

Splitting Read and Write Requests
=================================

Read/write splitting offloads read requests from primary instances to read replicas on a data node at a ratio, improving processing of read/write transactions. This function is transparent to applications, and you do not need to modify service code. Configure read weights of primary instances and their read replicas on the DDM console, and read traffic will be distributed at the preset ratio and write traffic will be forwarded to the primary instances by default. The ratio is generally based on service requirements and loads of associated data nodes.

Data is asynchronously replicated from the primary instance to read replicas, and there is a delay between them in milliseconds. Set weights of the primary instance and its read replicas to 0 and 100, respectively, that is, distribute all read requests to read replicas if sub-second latency is allowed for read requests and these requests require high query costs that may impact read/write transactions. In other scenarios, adjust the ratio based on service requirements.

Precautions
-----------

-  The SELECT statements that contain hints or modify data in transactions are all executed by the primary instances.
-  If the associated primary instance becomes faulty and parameter **Seconds_Behind_Master** on its read replicas is set to **NULL**, read-only requests are still forwarded to the primary instance. Recover the faulty instance as soon as possible.

Prerequisites
-------------

-  You have created a DDM instance and a data node with read replicas.
-  You have created a schema.

Procedure
---------

#. On the **Instances** page, locate the required DDM instance and click its name.
#. In the navigation pane, choose **Data Nodes**.
#. On the displayed page, locate the target instance and click **Configure Read Weight** in the **Operation** column. The read weight can be 0 to 100.

   -  If you create a read replica for the associated instance, the read replica will handle all separated read requests by default. To re-assign read/write requests, you can configure read weights of the associated instance and its read replica.

   -  After the read weights are configured, the primary instance and its read replica will handle read requests according to the following formulas:

      -  Primary instance: Read weight of primary instance/Total read weights of primary instance and read replica
      -  Read replica: Read weight of read replica/Total read weights of primary instance and read replica

      For example: If an RDS for MySQL instance contains one primary instance and one read replica and read weights of the primary instance and its read replica are 20 and 80 respectively, they will process read requests in the ratio of 1:4. In other words, the primary instance processes 1/4 of read requests and read replica processes 3/4. Write requests are automatically routed to the primary instance.

#. After the read weights are configured successfully, you can view the weights on the **Data Nodes** page.
