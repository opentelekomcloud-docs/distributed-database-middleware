:original_name: ddm_01_0018.html

.. _ddm_01_0018:

Basic Concepts
==============

Data Node
---------

A data node is the minimum management unit of DDM. Each data node represents an independently running database, and it may be an RDS for MySQL or GaussDB(for MySQL) instance that is associated with your DDM instance. You can create multiple schemas in a DDM instance to manage data nodes and access each data node independently.

.. note::

   DDM instances do not store service-related data, which is stored in shards of data nodes.

VPC
---

A Virtual Private Cloud (VPC) is a private and isolated virtual network. You can configure IP address ranges, subnets, and security groups, assign EIPs, and allocate bandwidth for DDM instances.

Subnet
------

A subnet is a range of IP addresses, a logical subdivision of an IP network. Subnets are created for a VPC where you will place your DDM instances. Every subnet is defined by a unique CIDR block which cannot be modified once the subnet is created.

Security Group
--------------

A security group is a collection of rules for ECSs that have the same security protection requirements and are mutually trusted. After a security group is created, you can add different access rules to the security group, and these rules will apply to all ECSs added to this security group.

Your account automatically comes with a security group by default. The default security group allows all outbound traffic and denies all inbound traffic. Your ECSs in this security group can communicate with each other without the need to add rules.

Parameter Template
------------------

A parameter template acts as a container for configuration values that can be applied to one or more DDM instances. If you want to use your own parameter template, you only need to create a custom parameter template and select it when creating a DDM instance. You can also apply the parameter template to an existing DDM instance.

EIP
---

The Elastic IP (EIP) service provides independent public IP addresses and bandwidth for Internet access. EIPs can be bound to and unbound from DDM instances.

Region and Endpoint
-------------------

Before using an API to call resources, you need to specify its region and endpoint. For more details, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.
