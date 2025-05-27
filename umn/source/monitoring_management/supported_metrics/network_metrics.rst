:original_name: ddm_03_0054.html

.. _ddm_03_0054:

Network Metrics
===============

If load balancing is enabled for your DDM instance, you can view network metrics in the following table. If load balancing is not enabled, you do not have the permissions to view them.

.. table:: **Table 1** Load balancing metrics

   +-------------------+----------------------------------+----------------------------------------------------------------------------------+-------------+-------------------------+--------------------------------+
   | Metric ID         | Metric Name                      | Description                                                                      | Value Range | Monitored Object        | Monitoring Interval (Raw Data) |
   +===================+==================================+==================================================================================+=============+=========================+================================+
   | m7_in_Bps         | Inbound Rate                     | Traffic used for accessing the monitored object from the Internet per second     | >= 0        | Dedicated load balancer | 1 minute                       |
   |                   |                                  |                                                                                  |             |                         |                                |
   |                   |                                  | Unit: byte/s                                                                     |             |                         |                                |
   +-------------------+----------------------------------+----------------------------------------------------------------------------------+-------------+-------------------------+--------------------------------+
   | m8_out_Bps        | Outbound Rate                    | Traffic used by the monitored object to access the Internet per second           | >= 0        | Dedicated load balancer | 1 minute                       |
   |                   |                                  |                                                                                  |             |                         |                                |
   |                   |                                  | Unit: byte/s                                                                     |             |                         |                                |
   +-------------------+----------------------------------+----------------------------------------------------------------------------------+-------------+-------------------------+--------------------------------+
   | ma_normal_servers | Healthy Servers                  | Number of healthy backend servers associated with the monitored object           | >= 0        | Dedicated load balancer | 1 minute                       |
   |                   |                                  |                                                                                  |             |                         |                                |
   |                   |                                  | Unit: count                                                                      |             |                         |                                |
   +-------------------+----------------------------------+----------------------------------------------------------------------------------+-------------+-------------------------+--------------------------------+
   | l4_in_bps_usage   | Layer-4 Inbound Bandwidth Usage  | Percentage of inbound TCP/UDP bandwidth from the monitored object to the client  | 0-100       | Dedicated load balancer | 1 minute                       |
   +-------------------+----------------------------------+----------------------------------------------------------------------------------+-------------+-------------------------+--------------------------------+
   | l4_out_bps_usage  | Layer-4 Outbound Bandwidth Usage | Percentage of outbound TCP/UDP bandwidth from the monitored object to the client | 0-100       | Dedicated load balancer | 1 minute                       |
   +-------------------+----------------------------------+----------------------------------------------------------------------------------+-------------+-------------------------+--------------------------------+
