The table below describes all database objects that are created after installing the sample application or installing the AOE as standalone plug-in in an existing application. 

- column **The plug-in** describes whether object is required for the manual installation
- column **The sample application** describes whether object is required for the manual installation

| Object Name                  | Object Type        | The plug-in | The sample application | Description                                                  |
| :--------------------------- | :----------------- | :---------: | :--------------------: | :----------------------------------------------------------- |
| **RESTful  Service**         | **Install script** |   **Yes**   |        **Yes**         | **The RESTful Service is used to handle all AOE host server requests to load,  create and update documents.** |
| **AOE_FILES_DEFAULT**        | **Table**          |     Yes     |          Yes           | **The table is used to store document content when a developer doesn’t provide custom table.** |
| AOE_FILES_DEFAULT_SEQ        | Sequence           |     Yes     |          Yes           |                                                              |
| BI_AOE_FILES_DEFAULT         | Trigger            |     Yes     |          Yes           |                                                              |
| **AOE_FILES_CUSTOM**         | **Table**          |     No      |          Yes           | **The table is used by the plug-in sample application in order to showcase the  usage of the plug-in attribute Settings \ Custom Table.** |
| BI_AOE_FILES_CUSTOM          | Trigger            |     No      |          Yes           | The trigger is  using sequence BI_AOE_FILES_DEFAULT.         |
| **AOE_REST_LOGS**            | **Table**          |     Yes     |          Yes           | The table is used by the plug-in REST service to log information about  requests performed by AOE host server to load and update document content. |
| AOE_REST_LOGS_SEQ            | Sequence           |     Yes     |          Yes           |                                                              |
| BI_AOE_REST_LOGS             | Trigger            |     Yes     |          Yes           |                                                              |
| **AOE_SAMPLE_FILE_VERSIONS** | **Table**          |     No      |          Yes           | **The table is used by the plug-in sample application in order to showcase the  usage of the plug-in callbacks to implement custom document versioning.** |
| **AOE_FILES_UPLOADED**       | **Table**          |     No      |          Yes           | **The table is used by the plug-in sample application to allow uploading  end-users documents.** |
| AOE_FILES_UPLOADED_SEQ       | Sequence           |             |          Yes           |                                                              |
| BI_AOE_FILES_UPLOADED        | Trigger            |             |          Yes           |                                                              |
| **PIP_CRYPTO**               | **Package**        |   **Yes**   |        **Yes**         | **The package is used by the plug-in to secure the plug-in access token.** |
| **UC_UTF7**                  | **Package**        |   **Yes**   |        **Yes**         | **The package is used by the plug-in to decode documents filenames from UTF7 to  UTF8.** |
| **UC_PLUGIN_UTIL**           | **Package**        |   **Yes**   |        **Yes**         | **The package is used by the plug-in to evaluate APEX regions read-only state.** |
| **AOE_REST**                 | **Package**        |   **Yes**   |        **Yes**         | **The package is used by the plug-in RESTful Service handlers to handle  requests performed by the AOE host server.** |
| **AOE_PLUGIN**               | **Package**        |   **Yes**   |        **Yes**         | **The plug-in package implementing region-type plug-in for Oracle APEX  application.** |
| **AOE_SAMPLE_APP_UTIL**      | **Package**        |   **No**    |        **Yes**         | **The package is used by the plug-in sample application to handle sample  application page processes and implement custom callbacks.** |
| **AOP_API21_PKG**            | **Package**        |   **Yes**   |        **Yes**         | **The APEX Office Print package is used by the plug-in sample application to  showcase the integration of AOP and AOE.** |
| AOP_API_PKG                  | Synonym            |     Yes     |          Yes           |                                                              |