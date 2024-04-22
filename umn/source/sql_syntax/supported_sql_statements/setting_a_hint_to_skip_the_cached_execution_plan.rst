:original_name: ddm_03_0039.html

.. _ddm_03_0039:

Setting a Hint to Skip the Cached Execution Plan
================================================

DDM allows you to configure a hint to control whether each SELECT statement skips the cached execution plan.

The hint is in the format of **/*!GAUSS:skip_plancache=**\ *flag*\ **\*/**.

*flag* can be set to **true** or **false**. **true** indicates that the statement skips the cached execution plan. **false** indicates that the statement does not skip the cached execution plan.

Currently, this function only applies to SELECT statements.
