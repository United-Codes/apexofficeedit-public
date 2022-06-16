# REST Web Service

## Resource handlers
### Creating a new document
The REST handler is used by the plug-in to create a new document of selected type. When the end-user clicks on a new document icon and then selects a document type to be created, the AJAX call is performed to this resource handler.
**Source**
### Getting document meta-data for APEX

| URI Template    | Method | Source Type | Format |
| --------------- | ------ | ----------- | ------ |
| **files/meta/** | GET    | PL/SQL      | JSON   |

The REST handler is used by the plug-in to fetch basic information about the currently opened document. When a document is loaded into AOE editor, the plug-in exposes document meta-data through the plug-in event **AOE Document Loaded**. Learn more about the event in **Region plugin \ Events \ Document Loaded** documentation.

**Source**

```sql
declare
  v_log_scope varchar2(4) := 'REST';
begin
  AOE_REST.init;
  
  AOE_REST.log_info(v_log_scope, 'setting global variables "rest_get_doc_meta_data"');
  AOE_REST.set_global_variables(:access_token);
  
  AOE_REST.log_info(v_log_scope, 'start processing "rest_get_doc_meta_data"');
  
  AOE_REST.rest_get_doc_meta_data(
    p_access_token  => :access_token, 
    p_status_code   => AOE_REST.g_rest_status_code
  );
  
  :status_code := AOE_REST.g_rest_status_code;

  AOE_REST.log_info(v_log_scope, 'finished processing "rest_get_doc_meta_data"  with status: %s', NVL(to_char(AOE_REST.g_rest_status_code), '%NULL%'));
exception
  when others then
    AOE_REST.log_error(v_log_scope, 'While fetching document meta-data an error was raised: "'||SQLERRM||'"');

end;
```



**Defined parameters**

| **Name**      | **Bind Variable** | **Source Type** | **Access Method** | **Data Type** |
| ------------- | ----------------- | --------------- | ----------------- | ------------- |
| access\_token | access\_token     | URI             | IN                | STRING        |



### Getting document meta-data for AOE host
The REST handler is used by the AOE host server to fetch a document meta-data. Based on returned data the AOE host server renders a document with configuration returned by the REST handler.
### Getting document contents
The REST handler is used by the AOE host server to fetch a document contents. The handler is requested after successful **getting document meta-data for AOE host** (HTTP status code 200).
### Updating document content
The REST handler is used by the AOE host server update the currently opened document content.
### Saving existing document as a copy with a new filename
The REST handler is used by the AOE host server to create a new document based on existing, currently opened document.
## Error Handling
### Creating a new document
### Getting document meta-data
### Getting document contents
### Updating document content
### Saving existing document as a copy with a new filename
## Error debugging