:original_name: ddm_api_01_0064.html

.. _ddm_api_01_0064:

Status Description
==================

DDM Instance Statuses
---------------------

.. table:: **Table 1** DDM instance statuses

   ================= =============================================
   Status            Description
   ================= =============================================
   CREATE            The DDM instance is being created.
   CREATEFAILED      The DDM instance fails to be created.
   RUNNING           The DDM instance is running and available.
   ERROR             The DDM instance is faulty.
   RESTARTING        The DDM instance is being restarted.
   RESIZING          Class of the DDM instance fail to be changed.
   GROWING           A DDM instance is being scaled out.
   REDUCING          A DDM instance is being scaled in.
   data_disk_full    Disk space is full.
   RESTORE           A DDM instance is being restored.
   BACKUP            A DDM instance is being backed up.
   SET_CONFIGURATION The instance parameters are being updated.
   ================= =============================================

DDM Schema Statuses
-------------------

.. table:: **Table 2** DDM schema statuses

   ================== ====================================
   Status             Description
   ================== ====================================
   CREATE             The schema is being created.
   RUNNING            The schema is running and available.
   CREATEFAILED       The schema fails to be created.
   DELETING           The schema is being deleted.
   Scaling out        The schema is being scaled out.
   Scaling out failed The schema fails to be scaled out.
   Rolling back       The schema is being rolled back.
   ================== ====================================

DDM Node Statuses
-----------------

.. table:: **Table 3** Node statuses

   =========== ========================================
   Status      Description
   =========== ========================================
   normal      The node is running normally.
   abnormal    The node is abnormal.
   creating    The DDM instance is being created.
   createfail  The DDM instance fails to be created.
   enlargefail The DDM instance fails to be scaled out.
   resizing    The node class is being changed.
   =========== ========================================
