The APEX Office Edit is delivered with fully configurated RESTful service module handling all document operations:

*   creating a new document,
    
*   getting document meta-data
    
*   getting document contents
    
*   updating document content
    
*   saving existing document as a copy with a new filename
    

# Resource handlers

RESTful resource handlers are using predefined PL/SQL code which should not be changed. Otherwise APEX Office Edit might be not working properly.

## Creating a new document

| URI Template       | Method | Source Type | Format |
| ------------------ | ------ | ----------- | ------ |
| files/create/:type | GET    | PL/SQL      | JSON   |

When the end-user clicks on a new document icon and then selects a document type to be created, the AJAX call is performed to this resource handler.

![](https://raw.githubusercontent.com/United-Codes/apexofficeedit-public/main/images/docs/REST_UI_creating_a_new_document_aoe_toolbar.png)

![](https://raw.githubusercontent.com/United-Codes/apexofficeedit-public/main/images/docs/REST_UI_creating_a_new_document_aoe_panel.png)

Source

The PL/SQL code defined in the procedure _AOE\_REST.rest\_create\_blank_ creates a blank BLOB of the given type and inserts it into the table defined in the plug-in attributes (table _AOE\_FILES\_DEFAULT_ is used when the plug-in region attribute _Settings \\ Use Custom Table_ is not checked).

```sql
declare
  v_log_scope varchar2(4) := 'REST';
begin
  AOE_REST.init;
    
  AOE_REST.log_info(v_log_scope, 'setting global variables "rest_create_blank"');
  
  AOE_REST.set_global_variables(:access_token);
  
  AOE_REST.log_info(v_log_scope, 'override g_current_file_id for not yet created BLOB');
  
  AOE_REST.g_current_file_id := AOE_REST.get_timestamp_ms;
  AOE_REST.log_info(v_log_scope, 'start processing "rest_create_blank"');
  AOE_REST.rest_create_blank(
    p_access_token => :access_token,
    p_blob_type    => :type,
    p_status_code  => AOE_REST.g_rest_status_code
  );
  :status_code := AOE_REST.g_rest_status_code;
  AOE_REST.log_info(v_log_scope, 'finished processing "rest_create_blank"  with status: %s', NVL(to_char(AOE_REST.g_rest_status_code), '%NULL%'));
exception
  when others then
    AOE_REST.log_error(v_log_scope, 'Errors was raised: '||SQLERRM);
end;
```

**Defined parameters**

| **Name** | **Bind Variable** | **Source Type** | **Access Method** | **Data Type** |
| --- | --- | --- | --- | --- |
| access\_token | access\_token | URI | IN  | STRING |

**Other bind variables used**

| **Bind Variable** | **Description** |
| --- | --- |
| :type | URI template parameter |
| :status\_code | Native REST bind variable to assign HTTP status code |

## Getting document meta-data

| URI Template | Method | Source Type | Format |
| ------------ | ------ | ----------- | ------ |
| files/:filed | GET    | PL/SQL      | JSON   |

The REST handler is called when

*   a document is loaded into APEX Office Edit (on page load, after refreshing the plug-in)
    
*   on the plug-in demand to fetch meta-data of loaded document.
    

**Source**

```sql
declare
  v_log_scope varchar2(4) := 'REST';
begin
  AOE_REST.init;
  
  AOE_REST.log_info(v_log_scope, 'setting global variables "rest_get_file_info"');
  AOE_REST.set_global_variables(:access_token);
  
  AOE_REST.log_info(v_log_scope, 'start processing "rest_get_file_info"');
  
  AOE_REST.rest_get_file_info(
    p_file_id       => :fileid, 
    p_access_token  => :access_token, 
    p_status_code   => AOE_REST.g_rest_status_code
  );
  
  :status_code := AOE_REST.g_rest_status_code;
  AOE_REST.log_info(v_log_scope, 'finished processing "rest_get_file_info"  with status: %s', NVL(to_char(AOE_REST.g_rest_status_code), '%NULL%'));
exception
  when others then
    AOE_REST.log_error(v_log_scope, 'While fetching document meta-data an error was raised: "'||SQLERRM||'"');
    AOE_REST.rest_exception_get_file_info(
      p_log_scope     => v_log_scope,
      p_status_code   => :status_code,
      p_content_type  => :content_type
    );
end;
```

**Defined parameters**

| **Name** | **Bind Variable** | **Source Type** | **Access Method** | **Data Type** |
| --- | --- | --- | --- | --- |
| access\_token | access\_token | URI | IN  | STRING |

**Other bind variables used**

| **Bind Variable** | **Description** |
| --- | --- |
| :fileid | URI template parameter |
| :status\_code | Native REST bind variable to assign HTTP status code |
| :content\_type | Native REST bind variable to assign response content type |

## Getting document contents

| URI Template           | Method | Source Type | Format |
| ---------------------- | ------ | ----------- | ------ |
| files/:fileid/contents | GET    | PL/SQL      | JSON   |

The REST handler is requested after **getting document meta-data** is successful (HTTP status code 200) and it does return document contents to AOE server-side which is then displayed within the AOE editor.

**Source**

```sql
declare
  v_log_scope varchar2(4) := 'REST';
  v_content_type varchar2(4000);
begin
  AOE_REST.init;
  
  AOE_REST.log_info(v_log_scope, 'setting global variables "rest_get_file_content"');
  AOE_REST.set_global_variables(:access_token);
  
  AOE_REST.log_info(v_log_scope, 'start processing "rest_get_file_content"');
  
  AOE_REST.rest_get_file_content(
    p_file_id      => :fileid,
    p_access_token => :access_token,
    p_status_code  => AOE_REST.g_rest_status_code,
    p_content_type => v_content_type
  );
  
  :status_code := AOE_REST.g_rest_status_code;
  :content_type := v_content_type;
  AOE_REST.log_info(v_log_scope, ':content_type: %s', NVL(to_char(v_content_type), '%NULL%'));
  AOE_REST.log_info(v_log_scope, 'finished processing "rest_get_file_content" with status: %s', NVL(to_char(AOE_REST.g_rest_status_code), '%NULL%'));
exception
  when others then
    AOE_REST.log_error(v_log_scope, 'While fetching document contents an error was raised: "'||SQLERRM||'"');
    AOE_REST.rest_exception_get_file_content(
      p_log_scope => v_log_scope,
      p_status_code => :status_code
    );
end;
```

**Defined parameters**

| **Name** | **Bind Variable** | **Source Type** | **Access Method** | **Data Type** |
| --- | --- | --- | --- | --- |
| access\_token | access\_token | URI | IN  | STRING |

**Other bind variables used**

| **Bind Variable** | **Description** |
| --- | --- |
| :fileid | URI template parameter |
| :status\_code | Native REST bind variable to assign HTTP status code |
| :content\_type | Native REST bind variable to assign response content type |

## Updating document content

| URI Template           | Method | Source Type | Format |
| ---------------------- | ------ | ----------- | ------ |
| files/:fileid/contents | POST   | PL/SQL      | JSON   |

TBD

**Source**

```sql
declare
  v_log_scope varchar2(4) := 'REST';
begin
  AOE_REST.init;
  
  AOE_REST.log_info(v_log_scope, 'setting global variables "rest_update"');
  AOE_REST.set_global_variables(:access_token);
  
  AOE_REST.log_info(v_log_scope, 'start processing "rest_update"');
  
  AOE_REST.rest_update ( 
    p_file_id          => :fileid,
    p_access_token     => :access_token,
    p_change_timestamp => :passed_header_timestamp,
    p_body             => :body,
    p_ismodifiedbyuser => :ismodifiedbyuser,
    p_autosaveflag     => :autosaveflag,
    p_isexitsave       => :is_exit_save,
    p_status_code      => AOE_REST.g_rest_status_code,
    p_additional_data  => :data
  );
  
  :status_code := AOE_REST.g_rest_status_code;
  AOE_REST.log_info(v_log_scope, 'finished processing "rest_update"  with status: %s', NVL(to_char(AOE_REST.g_rest_status_code), '%NULL%'));
exception
  when others then
    AOE_REST.log_error(v_log_scope, 'While saving a document an error was raised: '||SQLERRM);
    AOE_REST.rest_exception_update(
      p_log_scope     => v_log_scope,
      p_status_code   => :status_code
    );
end;
```

**Defined parameters**

| **Name** | **Bind Variable** | **Source Type** | **Access Method** | **Data Type** |
| --- | --- | --- | --- | --- |
| access\_token | access\_token | URI | IN  | STRING |
| X-LOOL-WOPI-ExtendedData | data | HTTP Header | IN  | STRING |
| X-LOOL-WOPI-Timestamp | passed\_header\_timestamp | HTTP Header | IN  | STRING |
| X-LOOL-WOPI-IsAutosave | autosaveflag | HTTP Header | IN  | STRING |
| X-LOOL-WOPI-IsExitSave | is\_exit\_save | HTTP Header | IN  | STRING |
| X-LOOL-WOPI-IsModifiedByUser | ismodifiedbyuser | HTTP Header | IN  | STRING |

**Other bind variables used**

| **Bind Variable** | **Description** |
| --- | --- |
| :fileid | URI template parameter |
| :status\_code | Native REST bind variable to assign HTTP status code |

## Saving existing document as a copy with a new filename

| URI Template  | Method | Source Type | Format |
| ------------- | ------ | ----------- | ------ |
| files/:fileid | POST   | PL/SQL      | JSON   |

TBD

**Source**

```
declare
  v_log_scope varchar2(4) := 'REST';
begin
  AOE_REST.init;
  
  AOE_REST.log_info(v_log_scope, 'setting global variables "rest_save_as"');
  AOE_REST.set_global_variables(:access_token);
  
  AOE_REST.log_info(v_log_scope, 'start processing "rest_save_as"');
  
  AOE_REST.rest_save_as(
    p_file_id            => :fileid,
    p_access_token       => :access_token,
    p_body               => :body,
    p_wopi_override      => :wopi_override,      --X-WOPI-Override
    p_suggested_name     => :suggested_name,     --X-WOPI-SuggestedTarget
    p_filename           => :filename,           --X-WOPI-RelativeTarget
    p_h_should_overwrite => :h_should_overwrite, --X-WOPI-OverwriteRelativeTarget
    p_status_code        => AOE_REST.g_rest_status_code
  );
  
  :status_code := AOE_REST.g_rest_status_code;
  AOE_REST.log_info(v_log_scope, 'finished processing "rest_save_as"  with status: %s', NVL(to_char(AOE_REST.g_rest_status_code), '%NULL%'));
exception
  when others then
    AOE_REST.log_error(v_log_scope, 'While saving a document as copy an error was raised: '||SQLERRM);
    AOE_REST.rest_exception_save_as(
      p_log_scope     => v_log_scope,
      p_status_code   => :status_code
    );
end;
```

**Defined parameters**

| **Name** | **Bind Variable** | **Source Type** | **Access Method** | **Data Type** |
| --- | --- | --- | --- | --- |
| access\_token | access\_token | URI | IN  | STRING |
| X-WOPI-OverwriteRelativeTarget | h\_should\_overwrite | HTTP Header | IN  | STRING |
| X-WOPI-RelativeTarget | filename | HTTP Header | IN  | STRING |
| X-WOPI-SuggestedTarget | suggested\_name | HTTP Header | IN  | STRING |
| X-WOPI-Override | wopi\_override | HTTP Header | IN  | STRING |

**Other bind variables used**

| **Bind Variable** | **Description** |
| --- | --- |
| :fileid | URI template parameter |
| :status\_code | Native REST bind variable to assign HTTP status code |
| :body | Native REST bind variable referencing document content |

# Error Handling

## Creating a new document

TBD

***

**Invalid access token**

The error is raised when:

* Access token is expired - the end-user doesn’t interact with APEX Office Edit for longer than 10 hours
* Access token is invalid - the request is malformed and access token can’t be decoded by the APEX Office Edit REST handler

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_creating_doc_access_token_invalid.png?raw=true)

***

**Unexpected PL/SQL Error**

The error is raised when unhandled PL/SQL error is raised for example:

* insert callback procedure name is defined but it doesn’t exists
* insert callback procedure name is defined but it raises an error
* custom table is used but given configuration it is invalid (for example invalid column name)
* other unexpected PL/SQL error

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_creating_doc_unexpected_plsql_error.png?raw=true)



## Getting document meta-data

When the plug-in catches error while fetching document meta-data, the end-user can still interact with the plug-in in the following way:

*   close error message and enable new file mode of the plug-in (button “Create a new file”)
    
*   trigger apexrefresh event on the plug-in region in order to try again (button “Refresh”)
    
*   close error message in order to display AOE server message but he won’t be able to interact with the plug-in any longer and refreshing a page is required.

***

**Invalid access token**

The error is raised when the plug-in REST handler catches regarding access token:

* access token is expired - the end-user doesn’t interact with APEX Office Edit for longer than 10 hours
* access token is invalid - the request is malformed and access token can’t be decoded by the APEX Office Edit REST handler

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_get_meta_data_inalid_access_token.png?raw=true)

***

**Requested document not found**

The error is raised when the plug-in REST handler catches error **no\_data\_found** for valid plug-in configuration.

When debugging this error it’s advised to check the plug-in configuration (primary key value(s)) against APEX Session State.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_get_meta_data_doc_404.png?raw=true)

***

**Invalid plug-in configuration**

The error is raised when the plug-in REST handler catches error other than no data found error.

This error might occur when the end-user is redirected to the page with valid document ID but the plug-in instance have invalid custom table configuration (for example not existing table or column).

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_get_meta_data_plug_cfg_invalid.png?raw=true)

***

**Document type is not allowed**

The error is raised when the plug-in REST handler catches error regarding document MIME-type. The plug-in configuration excludes document types to be loaded, but the current APEX Session State (the plug-in primary key(s) value(s)) points to prohibited document type.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_get_meta_data_doc_type_not_allowed.png?raw=true)

***

**User permission to read a document**

The error is raised when the plug-in REST handler catches error regarding the end-user permission to load particular document.

The end-user permission to read document can be set in page designer level using the plug-in attribute **Document Permissions** and attribute **Function Returning Document Permissions**.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_get_meta_data_doc_perm.png?raw=true)



***

**Unexpected PL/SQL Error**

The error is raised when the plug-in REST handler catches unhandled PL/SQL error.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_get_meta_data_plsql_error.png?raw=true)

## Getting document contents

When the plug-in catches error while fetching document meta-data, the end-user can still interact with the plug-in in the following way:

*   close error message and enable new file mode of the plug-in (button “Create a new file”)
    
*   trigger apexrefresh event on the plug-in region in order to try again (button “Refresh”)
    
*   close error message in order to display AOE server message but he won’t be able to interact with the plug-in any longer and refreshing a page is required.

***

**Invalid access token**

The error is raised when the plug-in REST handler catches regarding access token:

* access token is expired - the end-user doesn’t interact with APEX Office Edit for longer than 10 hours
* access token is invalid - the request is malformed and access token can’t be decoded by the APEX Office Edit REST handler

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_get_blob_invalid_access_token.png?raw=true)



***

**Unexpected PL/SQL Error**

The error is raised when the plug-in REST handler catches unhandled error, for example:

* read callback procedure name is defined but it doesn’t exists
* read callback procedure name is defined and it raises an error
* other unexpected PL/SQL error

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_get_blob_unexpected_plsql.png?raw=true)

## Updating document content

When the plug-in catches error while fetching document meta-data, the end-user can still interact with the plug-in in the following way:

*   close error message in order to get back to the APEX Office Edit editor

***

**Invalid access token**

The error is raised when the plug-in REST handler catches regarding access token:

* access token is expired - the end-user doesn’t interact with APEX Office Edit for longer than 10 hours
* access token is invalid - the request is malformed and access token can’t be decoded by the APEX Office Edit REST handler

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_update_invalid_access_token.png?raw=true)

***

**Malformed update time**

The error is raised when AOE server performs request to REST handler with invalid last update time.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_update_update_time.png?raw=true)

***

**Unexpected PL/SQL Error**

The error is raised when the plug-in REST handler catches unhandled error, for example:

* update callback procedure name is defined but it doesn’t exists
* update callback procedure name is defined and it raises an error
* other unexpected PL/SQL error

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_update_unexpected_plsql.png?raw=true)

## Saving existing document as a copy with a new filename

When the plug-in catches error while fetching document meta-data, the end-user can still interact with the plug-in in the following way:

*   close error message in order to get back to the APEX Office Edit editor

***

**Invalid access token**

The error is raised when the plug-in REST handler catches regarding access token:

* access token is expired - the end-user doesn’t interact with APEX Office Edit for longer than 10 hours
* access token is invalid - the request is malformed and access token can’t be decoded by the APEX Office Edit REST handler

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_saveas_invalid_access_token.png?raw=true)

***

**Malformed request header (PUT_RELATIVE)**

The error is raised when AOE server performs invalid request to REST handler. **Contact United Codes in order to further assistance.**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_saveas_malformed_request_put_relative.png?raw=true)

***

**Malformed request header (filenames)**

The error is raised when AOE server performs invalid request to REST handler. **Contact United Codes in order to further assistance**.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_saveas_malformed_request_filenames.png?raw=true)

***

**Malformed request header (missing filename)**

The error is raised when AOE server performs invalid request to REST handler<br><br>Contact United Codes in order to further assistance

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_saveas_malformed_request_missing_filename.png?raw=true)

***

**Unexpected PL/SQL Error**

The error is raised when the plug-in REST handler catches unhandled error, for example:

* update callback procedure name is defined but it doesn’t exists
* update callback procedure name is defined and it raises an error
* other unexpected PL/SQL error

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_error_saveas_unexpected_plsql.png?raw=true)

# Error debugging

APEX Offce Edit logs every request made to the plug-in RESTful service handlers. When an error is raised it is displayed to the end-user. All REST handlers errors includes unique REST log ID allowing easy debugging with REST logs table.

| ![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_err_debug_example_1.png?raw=true) | ![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_err_debug_example_2.png?raw=true) | ![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_err_debug_example_3.png?raw=true) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_err_debug_example_4.png?raw=true) | ![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_err_debug_example_5.png?raw=true) |                                                              |

APEX Office Edit sample application is deliviered with REST logs viewer and it supports debugging REST handler errors with simple report. Lets assume that while creating a new document an unexpected error was raised as on the image below.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_err_debug_step_1.png?raw=true)

In order to learn what caused an unexpected error while craeting a new document copy the debug ID **1931652608631445**. Click the button **REST logs**.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_err_debug_step_2.png?raw=true)

In region **Reports settings** set **Documents logs** to **REST request ID**. In the result a new field **REST request unique ID** is shown. Paste copied debug ID and in the region **Filters** set **REST handler level** to **Yes**, and set **Creating blank document** to **Yes**. In the result REST logs will be showing logs only for given debug ID.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/REST_err_debug_step_3.png?raw=true)

The logs and the error logged in REST logs table clearly shows that given procedure name for insert callback (the plug-in attribute **On Document Create Callback)** doesn’t exists.