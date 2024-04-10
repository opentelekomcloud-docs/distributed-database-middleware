:original_name: ddm_04_0006.html

.. _ddm_04_0006:

How Can I Handle Garbled Characters Generated When I Connect a MySQL Instance to a DDM Instance?
================================================================================================

If the MySQL connection code is inconsistent with the actual one, garbled characters may be displayed during parsing on DDM.

In this case, configure **default-character-set=utf8** to specify the encoding system.

Example:

.. code-block::

   mysql -h 127.0.0.1 -P 5066 -D database --default-character-set=utf8 -u ddmuser
