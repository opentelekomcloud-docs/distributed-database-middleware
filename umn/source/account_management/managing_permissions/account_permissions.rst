:original_name: ddm_12_0002.html

.. _ddm_12_0002:

Account Permissions
===================

DDM permissions management is based on MySQL permissions management. DDM supports most of MySQL syntax and permissions. For more information about MySQL accounts and permissions, see `MySQL documentation <https://dev.mysql.com/doc/refman/5.7/en/access-control.html>`__.

This document describes DDM account rules, permission levels, permission items, and permission operations.

.. note::

   DDM Accounts created by CREATE USER or GRANT have nothing to do with accounts in associated RDS instances, and will not be synchronized to RDS instances either.
