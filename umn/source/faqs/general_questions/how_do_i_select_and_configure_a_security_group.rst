:original_name: ddm_04_0067.html

.. _ddm_04_0067:

How Do I Select and Configure a Security Group?
===============================================

DDM uses VPCs and security groups to ensure security of your instances. The following provides guidance for you on how to correctly configure a security group.

Intra-VPC Access to DDM Instances
---------------------------------

Access to a DDM instance includes access to the DDM instance from the ECS where a client is located and access to its associated data nodes.

The ECS, DDM instance, and data nodes must be in the same VPC. In addition, correct rules should be configured for their security groups to allow network access.

#. Using the same security group is recommended for the ECS, DDM instance, and data nodes. After a security group is created, network access in the group is not restricted by default.

#. If different security groups are configured, you may need to refer to the following configurations:

   .. note::

      -  Assume that the ECS, DDM instance, and RDS for MySQL instance are configured with security groups **sg-ECS**, **sg-DDM**, and **sg-RDS**, respectively.
      -  Assume that the service port of the DDM instance is **5066** and that of the RDS for MySQL instance is **3306**.
      -  The remote end should be a security group or an IP address.

   Add the rules described in :ref:`Figure 1 <ddm_04_0067__fig153211250183316>` to the security group of the ECS to ensure that your client can access the DDM instance.

   .. _ddm_04_0067__fig153211250183316:

   .. figure:: /_static/images/en-us_image_0000001685147478.png
      :alt: **Figure 1** ECS security group rules

      **Figure 1** ECS security group rules

   Add the rules in :ref:`Figure 2 <ddm_04_0067__fig09669136435>` and :ref:`Figure 3 <ddm_04_0067__fig14207437194314>` to the security group of the ECS where your DDM instance is located so that your DDM instance can access associated data nodes and can be accessed by your client.

   .. _ddm_04_0067__fig09669136435:

   .. figure:: /_static/images/en-us_image_0000001733266413.png
      :alt: **Figure 2** Configuring security group inbound rules for your DDM instance

      **Figure 2** Configuring security group inbound rules for your DDM instance

   .. _ddm_04_0067__fig14207437194314:

   .. figure:: /_static/images/en-us_image_0000001733146301.png
      :alt: **Figure 3** Configuring security group outbound rules for your DDM instance

      **Figure 3** Configuring security group outbound rules for your DDM instance

   Add the rules in :ref:`Figure 4 <ddm_04_0067__fig11248191010442>` to the security group of the ECS where the data node is located so that your DDM instance can access the node.

   .. _ddm_04_0067__fig11248191010442:

   .. figure:: /_static/images/en-us_image_0000001733266417.png
      :alt: **Figure 4** Configuring security group rules of the RDS instance

      **Figure 4** Configuring security group rules of the RDS instance
