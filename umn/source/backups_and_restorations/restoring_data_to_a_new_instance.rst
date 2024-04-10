:original_name: ddm_0600016.html

.. _ddm_0600016:

Restoring Data to a New Instance
================================

DDM allows you to restore data from the current instance to any point in time using an existing backup. This is a good choice for routine service backup and restoration.

This section uses an RDS for MySQL instance as an example to describe how to restore data to a new DDM instance.

Precautions
-----------

-  Restoring data to a new instance restores your DDM instance and its data nodes (RDS for MySQL instances). Before the restoration, you need to prepare a new DDM instance and as many new RDS for MySQL instances as there are data nodes.

-  Restoring data to a new DDM instance will overwrite data on it and cause the instance to be unavailable during restoration.
-  The new RDS for MySQL instances must have the same or later versions and as much as or more storage space than the original ones.
-  Restoration is not supported if the destination DDM instance is in the primary network and its associated RDS for MySQL instance is in the extended network.
-  The source DDM instance must be of the version 2.3.2.11 or later, and the destination DDM instance must be of the version 3.0.8 or later.
-  Time points that data can be restored to depend on the backup policy set on original data nodes.

Procedure
---------

#. Log in to the DDM console.

#. .. _ddm_0600016__li4793191882712:

   Create a new DDM instance in the region where the source DDM instance is located or select an existing DDM instance that meets the requirements.

   .. note::

      Ensure that the new DDM instance or the selected existing DDM instance is not associated with any RDS for MySQL instance and has no schemas or accounts.

#. .. _ddm_0600016__li1017501443616:

   On the RDS console, create as many RDS for MySQL instances as there are in the source DDM instance.

   .. note::

      -  Ensure that the new RDS instances have the same or later versions than RDS instances associated with the source DDM instance.
      -  Ensure that each new RDS for MySQL instance has the same or larger storage space than each source RDS instance.

#. Switch back to the DDM console, in the instance list, locate the DDM instance whose data you want to restore, and click its name.

#. In the navigation pane on the left, choose **Backups & Restorations**.

#. Click **Restore to New Instance**.

#. On the displayed **Restore to New Instance** page, specify a time range and a point in time, and select destination DDM instance and associated data nodes.

   .. table:: **Table 1** Parameter description

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                          |
      +===================================+======================================================================================================================+
      | Time Range                        | Select a time range.                                                                                                 |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+
      | Time Point                        | Select a time point.                                                                                                 |
      |                                   |                                                                                                                      |
      |                                   | DDM checks whether the associated data nodes have available backups at the selected point in time.                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+
      | Destination DDM Instance          | Select the DDM instance created in :ref:`2 <ddm_0600016__li4793191882712>` as the destination instance.              |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+
      | Associated Data Nodes             | Select the RDS for MySQL instances created in :ref:`3 <ddm_0600016__li1017501443616>` as the destination data nodes. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+

#. Confirm the information and click **OK**. Wait for 1 to 3 minutes for the data restoration to complete.
