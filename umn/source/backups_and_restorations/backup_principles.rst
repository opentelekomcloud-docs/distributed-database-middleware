:original_name: ddm_12_0016.html

.. _ddm_12_0016:

Backup Principles
=================

DDM instances cannot be backed up manually. The system automatically backs them up at 02:00 UTC+00:00 every day. Metadata backup can also be triggered by any of the key operations such as deleting a schema, clearing source data after shard configuration, and deleting a DDM instance.


.. figure:: /_static/images/en-us_image_0000001685147442.png
   :alt: **Figure 1** Backup flowchart

   **Figure 1** Backup flowchart

.. note::

   The metadata database stores information of your DDM instances and their associated data nodes. All of your DDM instances in different regions share the same metadata database.
