:original_name: ddm_04_0068.html

.. _ddm_04_0068:

What High-Reliability Mechanisms Does DDM Provide?
==================================================

Protection of Data Integrity
----------------------------

DDM instance faults do not affect data integrity.

-  Service data is stored in shards of data nodes, but not on DDM.
-  Configuration information of schemas and logical tables is stored in DDM databases. Primary and standby DDM databases are highly available.

High Availability
-----------------

DDM is deployed using multiple stateless nodes in cluster mode and provides services through the IP address bound to your load balancer.

-  If one DDM node becomes faulty, an error is returned for connections established on the node, without affecting the DDM cluster. The faulty node is generally deleted from the cluster within 5 seconds.
-  If a data node becomes faulty, services can be restored within 30 seconds after the data node is recovered.
