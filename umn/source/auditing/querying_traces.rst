:original_name: ddm_11_0003.html

.. _ddm_11_0003:

Querying Traces
===============

Scenarios
---------

After CTS is enabled, the tracker starts recording operations on cloud resources. Operation records for the last 7 days are stored on the CTS console.

This section describes how to query operation records for the last 7 days on the CTS console.

Procedure
---------

#. Log in to the management console.

#. Under **Management & Governance**, click **Cloud Trace Service**.

#. Choose **Trace List** in the navigation pane on the left.

#. Specify filter criteria to search for the required traces. The following filters are available:

   -  **Trace Source**, **Resource Type**, and **Search By**: Select a filter from the drop-down list.

      When you select **Resource ID** for **Search By**, you also need to select or enter a resource ID.

   -  **Operator**: Select a specific operator from the drop-down list.

   -  **Trace Status**: Available options include **All trace statuses**, **Normal**, **Warning**, and **Incident**. You can only select one of them.

   -  In the upper right corner of the page, you can specify a time range for querying traces.

#. Click **Query**.

#. Locate the required trace and click |image1| on the left of the trace to view details.

#. Click **View Trace** in the **Operation** column. On the displayed dialog box, the trace structure details are displayed.

#. Click **Export** on the right. CTS exports traces collected in the past seven days to a CSV file. The CSV file contains all information related to traces on the management console.

   For details about key fields in the trace structure, see sections "Trace Structure" and "Trace Examples" in the *Cloud Trace Service User Guide*.

.. |image1| image:: /_static/images/en-us_image_0000001733146333.png
