:original_name: ddm_05_0002.html

.. _ddm_05_0002:

Creating an Account
===================

Prerequisites
-------------

-  You have logged in to the DDM console.
-  There are schemas available in the DDM instance that you want to create an account for.

Procedure
---------

#. In the instance list, locate the required DDM instance and click its name.
#. In the navigation pane, choose **Accounts**.
#. On the displayed page, click **Create Account** and configure the required parameters.

   .. table:: **Table 1** Required parameters

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                           |
      +===================================+=======================================================================================================================================================+
      | Username                          | Username of the account.                                                                                                                              |
      |                                   |                                                                                                                                                       |
      |                                   | The username can consist of 1 to 32 characters and must start with a letter. Only letters, digits, and underscores (_) are allowed.                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Password                          | Password of the account. The password:                                                                                                                |
      |                                   |                                                                                                                                                       |
      |                                   | -  Must be case-sensitive.                                                                                                                            |
      |                                   | -  Can include 8 to 32 characters.                                                                                                                    |
      |                                   | -  Must contain at least three of the following character types: letters, digits, and special characters ``~!@#%^*-_=+?``                             |
      |                                   | -  Do not use weak or easy-to-guess passwords.                                                                                                        |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Confirm Password                  | The confirm password must be the same as the entered password.                                                                                        |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Schema                            | Schema to be associated with the account. You can select an existing schema from the drop-down list.                                                  |
      |                                   |                                                                                                                                                       |
      |                                   | The account can be used to access only the associated schemas.                                                                                        |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Permissions                       | Options: **CREATE**, **DROP**, **ALTER**, **INDEX**, **INSERT**, **DELETE**, **UPDATE**, and **SELECT**. You can select any or a combination of them. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Description of the account, which cannot exceed 256 characters.                                                                                       |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Confirm the settings and click **OK**.
