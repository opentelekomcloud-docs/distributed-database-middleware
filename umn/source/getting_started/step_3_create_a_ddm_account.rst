:original_name: ddm_02_0000.html

.. _ddm_02_0000:

Step 3: Create a DDM Account
============================

Procedure
---------

#. Log in to the DDM console, in the instance list, locate the required DDM instance and click its name.
#. In the navigation pane, choose **Accounts**.
#. On the displayed page, click **Create Account** and configure required parameters.

   .. table:: **Table 1** Required parameters

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                           |
      +===================================+=======================================================================================================================================================+
      | Username                          | Username of the account.                                                                                                                              |
      |                                   |                                                                                                                                                       |
      |                                   | The username can include 1 to 32 characters and must start with a letter. Only letters, digits, and underscores (_) are allowed.                      |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Password                          | Password of the account. The password:                                                                                                                |
      |                                   |                                                                                                                                                       |
      |                                   | -  Can include 8 to 32 characters.                                                                                                                    |
      |                                   | -  Must contain at least three of the following character types: letters, digits, and special characters ``~!@#%^*-_=+?``                             |
      |                                   | -  Cannot be a weak password. It cannot be overly simple and easily guessed.                                                                          |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Confirm Password                  | The confirm password must be the same as the entered password.                                                                                        |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Schema                            | Schema to be associated with the DDM account. You can select an existing schema from the drop-down list.                                              |
      |                                   |                                                                                                                                                       |
      |                                   | Only the associated schemas can be accessed using the account.                                                                                        |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Permissions                       | Options: **CREATE**, **DROP**, **ALTER**, **INDEX**, **INSERT**, **DELETE**, **UPDATE**, and **SELECT**. You can select any or a combination of them. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Description of the account, which cannot exceed 256 characters.                                                                                       |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.
