:original_name: ddm_06_1000.html

.. _ddm_06_1000:

Tags
====

Tag Management Service (TMS) enables you to use tags on the console to manage resources. TMS works with other cloud services to manage tags. TMS manages tags globally. Other cloud services manage only their own tags.

Precautions
-----------

-  A tag consists of a key and value. You can add only one value for each key.
-  Each instance can have up to 20 tags.

Adding a tag
------------

#. Log in to the DDM console.

#. On the **Instances** page, locate the required instance and click its name.

#. In the navigation pane on the left, click **Tags**.

#. Click **Add Tag**.

#. In the displayed dialog box, enter a tag key and value and click **OK**.

   The tag key and value must comply with the following rules.

   .. table:: **Table 1** Parameter description

      +-----------------------------------+----------------------------------------------------------------------------------------+
      | Item                              | Description                                                                            |
      +===================================+========================================================================================+
      | Tag key                           | This parameter is mandatory and cannot be null. The key:                               |
      |                                   |                                                                                        |
      |                                   | -  Must be unique for each instance.                                                   |
      |                                   | -  Can only consist of digits, letters, underscores (_), hyphens (-), and at sign (@). |
      |                                   | -  Can include 1 to 36 characters.                                                     |
      |                                   | -  Cannot be an empty string or start with **\_sys\_**.                                |
      +-----------------------------------+----------------------------------------------------------------------------------------+
      | Tag value                         | This parameter is mandatory. The value:                                                |
      |                                   |                                                                                        |
      |                                   | -  Is an empty string by default.                                                      |
      |                                   | -  Can only consist of digits, letters, underscores (_), hyphens (-), and at sign (@). |
      |                                   | -  Can contain 0 to 43 characters.                                                     |
      +-----------------------------------+----------------------------------------------------------------------------------------+

#. View and manage the tag on the **Tags** page.

Editing a Tag
-------------

#. Log in to the DDM console.

#. On the **Instances** page, locate the required instance and click its name.

#. On the **Tags** page, locate the tag that you want to edit and click **Edit** in the **Operation** column. In the displayed dialog box, change the tag value and click **OK**.

   Only the tag value can be edited.

#. View and manage the tag on the **Tags** page.

Deleting Tags
-------------

#. Log in to the DDM console.
#. On the **Instances** page, locate the required instance and click its name.
#. In the navigation pane, choose **Tags**. On the displayed page, locate the tag that you want to delete and click **Delete** in the **Operation** column. In the displayed dialog box, click **Yes**.
#. Check that the tag is no longer displayed on the **Tags** page.

Searching for Instances by Tag
------------------------------

After tags are added, you can search for instances by tag to quickly find specific types of instances.

#. Log in to the DDM console.
#. On the **Instances** page, click **Search by Tag** in the upper right corner of the instance list.
#. Enter a tag key and a tag value and click **Search**.
#. View the instance found.
