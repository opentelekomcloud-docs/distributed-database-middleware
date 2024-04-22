:original_name: ddm_api_01_0063.html

.. _ddm_api_01_0063:

Obtaining a Project ID
======================

Scenarios
---------

When calling APIs, you need to specify the project ID in some URLs. To do so, you need to obtain the project ID first Two methods are available:

-  :ref:`Obtaining the Project ID by Calling an API <ddm_api_01_0063__section85791974381>`
-  :ref:`Obtaining a Project ID from the Console <ddm_api_01_0063__section153711445316>`

.. _ddm_api_01_0063__section85791974381:

Obtaining the Project ID by Calling an API
------------------------------------------

The API used to obtain a project ID is **GET https://{Endpoint}/v3/projects**. **{Endpoint}** is the IAM endpoint and can be obtained from `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__. For details about API authentication, see :ref:`Authentication <ddm_api_01_0011>`.

The following is an example response. **id** indicates the project ID.

.. code-block::

   {
       "projects": [
           {
               "domain_id": "65382450e8f64ac0870cd180d14e684b",
               "is_domain": false,
               "parent_id": "65382450e8f64ac0870cd180d14e684b",
               "name": "project_name",
               "description": "",
               "links": {
                   "next": null,
                   "previous": null,
                   "self": "https://www.example.com/v3/projects/a4a5d4098fb4474fa22cd05f897d6b99"
               },
               "id": "a4a5d4098fb4474fa22cd05f897d6b99",
               "enabled": true
           }
       ],
       "links": {
           "next": null,
           "previous": null,
           "self": "https://www.example.com/v3/projects"
       }
   }

.. _ddm_api_01_0063__section153711445316:

Obtaining a Project ID from the Console
---------------------------------------

#. Sign up and log in to the management console.

#. Move your pointer over the username and select **My Credentials** in the displayed drop-down list.

   On the displayed page, view project IDs in the project list.


   .. figure:: /_static/images/en-us_image_0000001733265081.jpg
      :alt: **Figure 1** Viewing project IDs

      **Figure 1** Viewing project IDs
