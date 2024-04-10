:original_name: ddm_03_0068.html

.. _ddm_03_0068:

Overview and Application Scenarios
==================================

Overview
--------

Shard configuration is a core function of DDM. With this function, you can increase data nodes or shards to improve database storage and concurrency as services grow. Shard configuration has little impacts on your services, so you do not need to worry about database scaling and subsequent O&M as your services are burst.

Application Scenarios
---------------------

DDM provides the following methods of configuring shards to meet different service needs.

**Method 1: Keep shards unchanged and increase data nodes**

This method does not change the number of shards and only increases the number of data nodes. Some shards are migrated from original data nodes to new data nodes. The shard data is not redistributed, so this method is the fastest one among all three methods and is recommended.

This method underpins rapid service growth after horizontal sharding and can reduce costs at the early stage of services. It is also suitable if RDS for MySQL instances cannot meet storage space and read/write performance requirements.


.. figure:: /_static/images/en-us_image_0000001685147678.png
   :alt: **Figure 1** Adding RDS for MySQL instances with shards unchanged

   **Figure 1** Adding RDS for MySQL instances with shards unchanged

**Method 2: Add shards with data nodes unchanged**

This method adds shards, but not data nodes. It changes total shards, total table shards, and table sharding rules. Data is redistributed to all shards. Old tables in original shards will be deleted, and broadcast tables are increased.

This method is suitable if the associated RDS for MySQL instance has sufficient storage space but one of its tables contains a large amount of data, with query performance limited.


.. figure:: /_static/images/en-us_image_0000001685307426.png
   :alt: **Figure 2** Adding shards with RDS for MySQL instances unchanged

   **Figure 2** Adding shards with RDS for MySQL instances unchanged

**Method 3: Add both shards and data nodes**

This method increases both shards and data nodes. It changes total shards, total table shards, and table sharding rules. Data is redistributed to all shards. Old tables in original shards will be deleted, and broadcast tables are increased.

This method is suitable if RDS for MySQL instances cannot meet storage space and read/write requirements and there is a physical table containing a large amount of data with query performance limited.


.. figure:: /_static/images/en-us_image_0000001733266613.png
   :alt: **Figure 3** Adding shards and RDS for MySQL instances

   **Figure 3** Adding shards and RDS for MySQL instances
