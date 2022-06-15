The plug-in is an Oracle APEX region plug-in implementing LibreOffice Online framework.

# Standard attributes

The plug-in uses the following standard attributes exposed in the APEX page designer:

*   Has "Page Items to Submit" Attribute
    
*   Has "Initialization JavaScript Code" Attribute
    
*   Has "CSS Class" Column Attribute
    
*   Has "Custom Attributes" Column Attribute
    

# Custom attributes

## Application

All attributes available as **Component Settings** are listed and described below.

### API Key

| Type | Required | Dependent on |
| :--- | :------- | :----------- |
| Text | No       | None         |

Enter the valid API key. The API key is available in the APEX Office Edit portal: `https://www.apexofficeedit.com/ords/uc/r/aoe_portal/`

### Server-Side URL

| Type | Required | Dependent on |
| :--- | :------- | :----------- |
| Text | Yes      | None         |

Specify the URL under which the plug-in server-side files can be accessed. For example, the URL `https://www.exmaple-domian.com/` will be used to reference the server-side file `https://www.exmaple-domian.com//browser/575607fac/cool.html`.

The default value is `https://api.apexofficeedit.com/`

### URL to RESTful service module

| Type | Required | Dependent on |
| :--- | :------- | :----------- |
| Text | No       | None         |

URL to **ORDS RESTful service module** handling the plugin operations **create a new document**, **save changes**, **save document as**, **get document information** and **get document content**. The URL must be copied from **SQL Workshop \ RESTful Services \ Module Definition**.

The plug-in is delivered with the default ORDS RESTful service module named **APEX OFFice Edit**. The URL must include the suffix `files/`, for example, `http://www.apexrnd.be/ords181/aoe/aoe/files/`.

### Default Document Filename

| Type | Required | Dependent on |
| :--- | :------- | :----------- |
| Text | Yes      | None         |

The default name of a file when a new document is created. 

## Component

All the plug-in region attributes available in the Oracle APEX page designer are listed and described below.

### Allowed File Types

| Type     | Required | Dependent on |
| :------- | :------- | :----------- |
| Checkbox | Yes      | None         |

Use the following document types to restrict what document types can be created and opened by the end-user.

Available options:<br>

* Microsoft Word
* Microsoft Excel
* Microsoft PowerPoint
* Open Document Text
* Open Document Spreadsheet
* Open Document Presentation
* Open Document Draw

### Settings

| Type     | Required | Dependent on |
| :------- | :------- | :----------- |
| Checkbox | No       | None         |

Use the following options to set the plug-in configuration

Available options:

| Option                      | Description                                                  |
| :-------------------------- | :----------------------------------------------------------- |
| Disable Editor Messages     | **When selected** - only error messages are being shown within APEX Office Edit editor. <br /><br />**When not selected** <br />the editor shows success message as the editor prompt within plug-in iframe and the end-user has to close prompt manualy. For example when document is succesfuly updated the editor shows message **Successfuly uploaded file**. |
| Override Component Settings | When selected, components settings **Form action** and **REST URL** can be overridden on the region level in the page designer. |
| Use Custom Table            | When selected, a custom table storing a document can be defined on the region level. Otherwise **AOE\_FILES\_DEFAULT** table is used. Learn more in **Database Objects**. |
| Disable printing            | When selected, the end-user can't print the document using browser print functionality - the editor print button is not displayed. Printing is only possible when an APEX application is accessible under the same origin as the plug-in server-side files. Otherwise, printing is not possible - clicking the print button raises a cross-origin JavaScript error. |

### Server-Side URL

| Type | Required | Dependent on                                          |
| :--- | :------- | :---------------------------------------------------- |
| Text | Yes      | Settings \ Override Component Settings **is checked** |

Specify the URL under which the plug-in server-side files can be accessed. For example, the URL `[https://www.exmaple-domian.com](https://www.exmaple-domian.com/)` will be used to reference the server-side file `https://www.exmaple-domian.com/browser/aoe/cool.html`.

### URL to RESTful service module

| Type | Required | Dependent on                                          |
| :--- | :------- | :---------------------------------------------------- |
| Text | Yes      | Settings \ Override Component Settings **is checked** |

URL to **ORDS RESTful service module** handling the plug-in operations **create a new document**, **save changes**, **save document as**, **get document information** and **get document content**. The URL must be copied from **SQL Workshop \ RESTful Services \ Module Definition**. 

The plug-in is delivered with the default ORDS RESTful service module named **APEX Office Edit**. The URL must include the suffix `files/` for example `http://www.apexrnd.be/ords181/aoe/aoe/files/`.

### Item(s) Containing Primary Key(s) Value(s)

| Type         | Required | Dependent on |
| :----------- | :------- | :----------- |
| Page Item(s) | Yes      | None         |

A given APEX page item(s) is (are) used to identify a document to be loaded from default `AOE_FILES_DEFAULT` or custom table.

**When use custom table is checked**

Enter the page item containing the document's primary key. When an item specified as the primary key is set to `NULL`, the plug-in shows the document creation panel.

**When use custom table is not checked**

Enter comma-delimited page items containing the primary key(s) value(s) of a document to be loaded. When any APEX item specified as the primary key is set to `NULL`, the plug-in shows the document creation panel.

### Menu layout

| Type        | Required | Dependent on |
| :---------- | :------- | :----------- |
| Select list | Yes      | None         |

Select the layout of the editor menu to be used, available options are the following:

| Option       | Description                                                  |
| :----------- | :----------------------------------------------------------- |
| Classic      | An old-fashioned drop-down menu layout is used to render the editor menu. Hiding menu entries is **possible**. The menu customization can be done using the plug-in attribute **JavaScript Initialization Code**. See the help text for the attribute **JavaScript Initialization Code** to learn more. |
| Notebook Bar | The menu layout is organized as tabs and is user-friendly - menu entries are using icons. Hiding menu entries is **not possible**. |

### Document Permissions

| Type        | Required | Dependent on |
| :---------- | :------- | :----------- |
| Select list | Yes      | None         |

Available options:

* Everyone can read and edit
* Only the author can read and edit
* Everyone can read but the author can edit
* Custom function returning document permissions - when selected, the PL/SQL function is used to return document permission. See the attribute **Function Returning Document Permissions** for more details.

### Function Returning Document Permissions

| Type | Required | Dependent on                                                 |
| :--- | :------- | :----------------------------------------------------------- |
| Text | Yes      | Document Permissions \ Custom function returning document permissions **is selected** |

Specify PL/SQL function name returning document permission for the end-user and document ID(s). The given function must be:

* accessible in the context of the given ORDS RESTful service module
* accepting defined arguments
* returning `VARCHAR2` string containing document permissions to **read**, **update**, **save as a new file** and **print** a document

The function specification is the following:

```sql
function function_name(
  p_application_id in number,
  p_page_id        in number,
  p_session_id     in number,
  p_file_id        in varchar2,
  p_user_id        in varchar2
) return VARCHAR2;
```

| **Parameter**      | **Type** | **Description**                                              |
| :----------------- | :------- | :----------------------------------------------------------- |
| p\_application\_id | NUMBER   | An application ID in which the plug-in is run                |
| p\_page\_id        | NUMBER   | An application page ID in which the plug-in is run           |
| p\_session\_id     | NUMBER   | An application session ID in which the plug-in is currently run |
| p\_file\_id        | VARCHAR2 | A document ID. When the plug-in uses a custom table and multiple primary keys, the value contains comma-separated primary keys values |
| p\_user\_id        | VARCHAR2 | An APEX application end-user username                        |

**Document permissions pattern**

The returned value from the function must be following the pattern `X:Y:Z:P` where

*   **X** is permission to **read document**,

*   **Y** is permission to **update document**,

*   **Z** is permission to **save document as a new file**.

*   **P** is permission to **print document from browser**.

Allowed values are **0** and **1**, where

*   **0** is **permission denied**,

*   **1** is **permission granted**.

### On Document Read Callback

| Type | Required | Dependent on |
| :--- | :------- | :----------- |
| Text | No       | None         |

Enter the PL/SQL procedure name to be executed after a document content is successfully read and loaded by the plug-in RESTful service module. The given procedure must be:

* accessible in the context of the given ORDS RESTful service module
* accepting defined arguments

The procedure specification is the following:

```sql
procedure procedure_name(
  p_application_id        in number,
  p_page_id               in number,
  p_session_id            in number,
  p_file_id               in varchar2,
  p_user_id               in varchar2,
  p_file_content          in blob,
  p_file_filename         in varchar2,
  p_file_mime_type        in varchar2,
  p_file_last_update_date in timestamp,
  p_file_version          in number,
  p_file_blob_owner       in varchar2
);
```

| **Parameter**               | **Type**  | **Description**                                              |
| :-------------------------- | :-------- | :----------------------------------------------------------- |
| p\_application\_id          | NUMBER    | An application ID in which the plug-in is run                |
| p\_page\_id                 | NUMBER    | An application page ID in which the plug-in is run           |
| p\_session\_id              | NUMBER    | An application session ID in which the plug-in is currently run |
| p\_file\_id                 | VARCHAR2  | A document ID. When the plug-in uses multiple primary keys (a custom table must be used), the value contains comma-separated primary keys values |
| p\_user\_id                 | VARCHAR2  | An APEX application end-user username                        |
| p\_file\_content            | BLOB      | A document file content                                      |
| p\_file\_filename           | VARCHAR2  | A document filename                                          |
| p\_file\_mime\_type         | VARCHAR2  | A document MIME type                                         |
| p\_file\_last\_update\_date | TIMESTAMP | A document last modification time                            |
| p\_file\_version            | NUMBER    | A document current version                                   |
| p\_file\_blob\_owner        | VARCHAR2  | A document author (the end-user that crated a document)Standard Attribute |

### On Document Create Callback

| Type | Required | Dependent on |
| :--- | :------- | :----------- |
| Text | No       | None         |

Enter the PL/SQL procedure name to be executed after a new document is inserted into the default or custom table. The given procedure must be:

* accessible in the context of the given ORDS RESTful service module
* accepting defined arguments

The procedure specification is the following:

```sql
procedure procedure_name(
  p_application_id        in number,
  p_page_id               in number,
  p_session_id            in number,
  p_file_id               in varchar2,
  p_user_id               in varchar2,
  p_file_content          in blob,
  p_file_filename         in varchar2,
  p_file_mime_type        in varchar2,
  p_file_last_update_date in timestamp,
  p_file_version          in number,
  p_file_blob_owner       in varchar2
);
```

| **Parameter**               | **Type**  | **Description**                                              |
| :-------------------------- | :-------- | :----------------------------------------------------------- |
| p\_application\_id          | NUMBER    | An application ID in which the plug-in is run                |
| p\_page\_id                 | NUMBER    | An application page ID in which the plug-in is run           |
| p\_session\_id              | NUMBER    | An application session ID in which the plug-in is currently run |
| p\_file\_id                 | VARCHAR2  | A document ID. When the plug-in uses multiple primary keys (a custom table must be used), the value contains comma-separated primary keys values |
| p\_user\_id                 | VARCHAR2  | An APEX application end-user username                        |
| p\_file\_content            | BLOB      | A document file content                                      |
| p\_file\_filename           | VARCHAR2  | A document filename                                          |
| p\_file\_mime\_type         | VARCHAR2  | A document MIME type                                         |
| p\_file\_last\_update\_date | TIMESTAMP | A document last modification time                            |
| p\_file\_version            | NUMBER    | A document current version                                   |
| p\_file\_blob\_owner        | VARCHAR2  | A document author (the end-user that crated a document)      |

### On Document Update Callback

| Type | Required | Dependent on |
| :--- | :------- | :----------- |
| Text | No       | None         |

Enter PL/SQL procedure name to be executed after a document is successfully **updated** or **saved as a new file**. The given procedure must be:

* accessible in the context of the given ORDS RESTful service module
* accepting defined arguments

The procedure specification is the following:

```sql
procedure procedure_name(
  p_application_id                in number,
  p_page_id                       in number,
  p_session_id                    in number,
  p_file_id_old                   in varchar2,
  p_file_id_new                   in varchar2,
  p_user_id                       in varchar2
);
```

| **Parameter**      | **Type** | **Description**                                              |
| :----------------- | :------- | :----------------------------------------------------------- |
| p\_application\_id | NUMBER   | An application ID in which the plug-in is implemented        |
| p\_page\_id        | NUMBER   | An application page ID in which the plug-in is implemented   |
| p\_session\_id     | NUMBER   | An application session ID in which the end-user uses the plug-in |
| p\_file\_id\_old   | VARCHAR2 | **When a document is updated**  <br />the primary key(s) value(s) of an updated document.<br /><br />**When a document is saved as a new file**<br />the primary key(s) value(s) of a document before the end-user requested saving document as a new file with a new filename. If the plug-in uses multiple columns to identify a document, then primary key values are delimited by a colon. |
| p\_file\_id\_new   | VARCHAR2 | **When a document is updated**  <br>always NULL<br>    <br>**When a document is saved as a new file**  <br>The primary key(s) value(s) of a new document saved with a new filename. If the plug-in uses multiple columns to identify a document, then primary key(s) value(s) are delimited by a colon. |
| p\_user\_id        | VARCHAR2 | The end-user username used to authenticate in the APEX session   |

### Function Returning a New Primary Key(s)

| Type | Required | Dependent on                               |
| :--- | :------- | :----------------------------------------- |
| Text | No       | Settings \ Use Custom Table **is checked** |

Specify PL/SQL function name returning a new primary key(s) value(s) used in the insert statement of a new document. Primary key(s) value(s) must be returned and comma-delimited in the same order as given columns in the attribute **Document Primary Key(s) Column(s)**.

When a function is specified, the primary key(s) column(s) and returned value(s) are included in the insert statement of a new document. Otherwise, the primary key(s) column(s) are not included - value(s) should be handled by the table trigger.

The given function must be:

* accessible in the context of the given ORDS RESTful service module
* accepting the defined argument
* returning `VARCHAR2` string containing a new document primary key(s) value(s) delimited with comma

The function specification is the following:

```sql
function callback_session_get_pks(
  p_access_token in varchar2
) return varchar2;
```

| **Parameter**    | **Type** | **Description**                                       |
| :--------------- | :------- | :---------------------------------------------------- |
| p\_access\_token | VARCHAR2 | An application ID in which the plug-in is implemented |

When the plug-in uses a custom table implementing two primary keys **ID** and **ID2**, the function should return the value **"X,Y"** where:

*   **X** is a new value for column **ID**

*   **Y** is a new value for column **ID2**

```sql
function example_function(
  p_access_token in varchar2
) return varchar2
is
  v_decoded_access_token AOE_REST.t_wopi_access_token;  
  v_result               varchar2(4000);
begin
  v_decoded_access_token := AOE_REST.get_access_token_decoded(p_access_token);

  v_result := 'X,Y';
  
  return v_result;
end;
```

The plug-in access token type is defined as:

```sql
TYPE t_wopi_access_token IS RECORD ( 
  file_id                         varchar2(4000), 
  session_id                      number,
  application_id                  number,
  page_id                         number,
  user_id                         varchar2(4000),
  rest_url                        varchar2(4000),
  valid_till                      DATE, 
  requesting_host                 VARCHAR2(50),
  table_schema                    varchar2(100),
  table_name                      varchar2(100),
  table_column_blob               varchar2(100),
  table_column_filename           varchar2(100),
  table_column_mimetype           varchar2(100),
  table_column_last_update        varchar2(100),
  table_column_owner              varchar2(100),
  table_column_version            varchar2(100),
  table_pks_names                 varchar2(100),
  table_pks_values                varchar2(100),
  readonly                        number,
  function_ret_pks_values         varchar2(100),
  plug_attr_settings              varchar2(100),
  function_file_perm              varchar2(100),
  procedure_file_read             varchar2(100),
  procedure_file_insert           varchar2(100),
  procedure_file_update           varchar2(100),
  document_perm_settings          varchar2(100),
  document_default_filename       varchar2(100)
);
```

The plug-in access token properties are described in the table below.

| **Property**                | **Type**       | **Description**                                              |
| :-------------------------- | :------------- | :----------------------------------------------------------- |
| file\_id                    | VARCHAR2(4000) | The current value of primary key(s) value(s).<br /><br />**When attribute Settings \\ Custom table is not checked**  <br />the current APEX Session State of page item defined in the plug-in attribute **Item Containing Primary Key Value**<br>    <br>**When attribute Settings \\ Custom table is checked<br />**the current APEX Session State of page item(s) defined in the plug-in attribute **Item(s) Containing Primary Key(s) Value(s)** |
| session\_id                 | NUMBER         | The current APEX Session ID from which the REST request was made |
| application\_id             | NUMBER         | The current APEX application ID from which the REST request was made |
| page\_id                    | NUMBER         | The current APEX application page ID from which the REST request was made |
| user\_id                    | VARCHAR2(4000) | The current APEX user by whom the REST request was initialized |
| rest\_url                   | VARCHAR2(4000) | The current URL to REST handler that was used to perform a REST call |
| valid\_till                 | DATE           | Time for which the access token is valid                     |
| requesting\_host            | VARCHAR2(50)   | The URL to the host from which the REST request was made     |
| table\_schema               | VARCHAR2(100)  | The schema in which a document is stored<br><br>**When attribute Settings \\ Custom table is not checked <br />**the current schema returned from `#OWNER#` substitution string<br><br />**When attribute Settings \\ Custom table is checked <br />**the value of the plug-in region attribute **Schema** |
| table\_name                 | VARCHAR2(100)  | The table name in which a document is stored<br><br>**When attribute Settings \\ Custom table is not checked** <br />the value is `AOE\_FILES\_DEFAULT`<br>    <br>**When attribute Settings \\ Custom table is checked** <br />the value of the plug-in region attribute **Table Name** |
| table\_column\_blob         | VARCHAR2(100)  | The column name in which a document contents is stored<br><br>**When attribute Settings \\ Custom table is not checked** <br />the value is always `CONTENT`<br><br />**When attribute Settings \\ Custom table is checked <br />**the value of the plug-in region attribute **Document File Content Column** |
| table\_column\_filename     | VARCHAR2(100)  | The column name in which a document filename is stored<br><br/>**When attribute Settings \\ Custom table is not checked** <br />the value is always `FILENAME`<br/>    <br/>**When attribute Settings \\ Custom table is checked <br />**the value of the plug-in region attribute **Document Filename Column** |
| table\_column\_mimetype     | VARCHAR2(100)  | The column name in which a document MIME-type is stored<br><br>**When attribute Settings \\ Custom table is not checked <br />**the value is always `MIME_TYPE`<br/>    <br>**When attribute Settings \\ Custom table is checked**<br />the value of the plug-in region attribute **Document MIME Type Column** |
| table\_column\_last\_update | VARCHAR2(100)  | The column name in which a document last update time is stored<br><br>**When attribute Settings \\ Custom table is not checked**<br />the value is always `LAST_UPDATE_DATE`<br/>    <br>**When attribute Settings \\ Custom table is checked** <br />the value of the plug-in region attribute **Document Last Update Column** |
| table\_column\_owner        | VARCHAR2(100)  | The column name in which a document owner name is stored<br><br>**When attribute Settings \\ Custom table is not checked**<br />the value is always `BLOB_OWNER`<br/>    <br>**When attribute Settings \\ Custom table is checked**<br />the value of the plug-in region attribute **Document Owner Column** |
| table\_column\_version      | VARCHAR2(100)  | The column name in which a document version is stored<br><br>**When attribute Settings \\ Custom table is not checked<br />**the value is always `VERSION`<br/>    <br>**When attribute Settings \\ Custom table is checked<br />**the value of the plug-in region attribute **Document Version Column** |
| table\_pks\_names           | VARCHAR2(100)  | The column(s) name(s) defined as primary key(s)<br><br>**When attribute Settings \\ Custom table is not checked** <br />the value is always `ID`<br/>    <br>**When attribute Settings \\ Custom table is checked**<br />the value of the plug-in region attribute **Primary Key(s) Column(s)** |
| table\_pks\_values          | VARCHAR2(100)  | The current value(s) of primary key(s) defined by the region plug-in attribute **Item(s) Containing Primary Key(s) Value(s)** |
| readonly                    | NUMBER         | When set to `1`  then a region implementing the plug-in is in read-only mode<br>When set to `0` then a region implementing the plug-in is not it read-only mode |
| function\_ret\_pks\_values  | VARCHAR2(100)  | The function name returning new primary key(s) value(s) for document creation.<br><br>**When attribute Settings \\ Custom table is not checked**<br />the value always `NULL`<br>    <br>**When attribute Settings \\ Custom table is checked**<br />the value of the plug-in region attribute **Function Returning a New Primary Key(s)** |
| plug\_attr\_settings        | VARCHAR2(100)  | The value of the plug-in region attribute **Settings**       |
| function\_file\_perm        | VARCHAR2(100)  | The function name returning new primary key(s) value(s) for document creation.<br><br>**When attribute Settings \\ Custom table is not checked**<br /> the value is always `NULL`<br>    <br>**When attribute Settings \\ Custom table is checked**<br />the value of the plug-in region attribute **Function Returning a New Primary Key(s)** |
| procedure\_file\_read       | VARCHAR2(100)  | The callback procedure name defined in the plug-in attribute **On Document Read Callback** |
| procedure\_file\_insert     | VARCHAR2(100)  | The callback procedure name defined in the plug-in attribute **On Document Insert Callback** |
| procedure\_file\_update     | VARCHAR2(100)  | The callback procedure name defined in the plug-in attribute **On Document Update Callback** |
| document\_perm\_settings    | VARCHAR2(100)  | The value of the plug-in region attribute **Document Permissions**. The value can be one of the following:<br><br>*   FUNCTION<br>*   EVERYONE\_CAN\_READ\_AND\_EDIT<br>*   ONLY\_AUTHOR\_CAN\_READ\_AND\_EDIT<br>*   EVERYONE\_CAN\_READ\_AUTHOR\_EDIT |
| document\_default\_filename | VARCHAR2(100)  | The value of the plug-in component setting **Default Document Filename** |

### Table Name

| Type | Required | Dependent on                               |
| ---- | -------- | ------------------------------------------ |
| Text | Yes      | Settings \ Use Custom Table **is checked** |

A custom table name in which a document content is stored. A custom table must have (at least) the following types of columns:

| Description                                                  | Type         |
| :----------------------------------------------------------- | :----------- |
| Column storing a document **filename**                       | VARCHAR2     |
| Column storing a document **owner** (an application end-user username) | VARCHAR2     |
| Column storing a document **MIME-type**                      | VARCHAR2     |
| Column storing a document **primary key**                    | NUMBER       |
| Column storing a document the **current version**            | NUMBER       |
| Column storing a document **content**                        | BLOB         |
| Column storing a document **last modification time**         | TIMESTAMP(6) |

**Multiple Primary Keys**
A custom table can use multiple primary keys to identify a document. Comma-delimited columns names must be set using the attribute **Primary Key(s) Column(s)**.

### Document Primary Key(s) Column(s)

| Type | Required | Dependent on                               |
| :--- | :------- | :----------------------------------------- |
| Text | Yes      | Settings \ Use Custom Table **is checked** |

Comma-delimited column names used as primary keys for a document.

### Document File Content Column

| Type | Required | Dependent on                               |
| :--- | :------- | ------------------------------------------ |
| Text | Yes      | Settings \ Use Custom Table **is checked** |

A column name which type is `BLOB` and is meant to store a document's file contents.

### Document Filename Column

| Type | Required | Dependent on                               |
| :--- | :------- | :----------------------------------------- |
| Text | Yes      | Settings \ Use Custom Table **is checked** |

A column name which type is `VARCHAR2` and is meant to store a document's filename (including the file extension).

### Document MIME Type Column

| Type | Required | Dependent on                               |
| :--- | :------- | ------------------------------------------ |
| Text | Yes      | Settings \ Use Custom Table **is checked** |

A column name which type is `VARCHAR2` and is meant to store a document's file MIME type.

### Document Last Update Column

| Type | Required | Dependent on                               |
| :--- | :------- | ------------------------------------------ |
| Text | Yes      | Settings \ Use Custom Table **is checked** |

A column name which type is `TIMESTAMP(6)` and is meant to store a document's last modification time.

### Document Version Column

| Type | Required | Dependent on                               |
| :--- | :------- | ------------------------------------------ |
| Text | Yes      | Settings \ Use Custom Table **is checked** |

A column name which type is `VARCHAR2` and is meant to store a document's current version.

### Document Owner Column

| Type | Required | Dependent on                               |
| :--- | :------- | :----------------------------------------- |
| Text | Yes      | Settings \ Use Custom Table **is checked** |

A column name which type is `VARCHAR2` and is meant to store a document's owner name (APEX user name).

# Additional Meta Data

## Has "Initialization JavaScript Code" Attribute

The attribute value must be an anonymous function accepting only one parameter which is a JSON object containing all plug-in options rendered from the plug-in package on page load. The function must return this JSON object to initialize the plug-in. Specified object properties can be used to customize the plug-in UI and logging in the application debug mode enabled.

```javascript
function( pOptions ) {
  pOptions.buttons             = [];
  pOptions.menuHideItems       = [];
  pOptions.hideSidebar         = false;
  pOptions.hideMenu            = false;
  pOptions.hideRuler           = false;
  pOptions.logPrefixAsStaticId = false;  
  pOptions.height              = 500;
  pOptions.zoomLevel           = 10;  
  
  return pOptions;
}
```

The parameters which can be safely customized are described below:

### **buttons** `Array`

An `Array` of JSON objects defining a custom button to be added to the AOE toolbar. Clicked button triggers **AOE Button Clicked** event. The possibility to add custom buttons is experimental and might be removed or updated. 

A custom button JSON must implement the following properties:

| Property     | Type   | Description                                                  |
| :----------- | :----- | :----------------------------------------------------------- |
| id           | String | An unique button ID is used to identify clicked custom button when the plug-in event **AOE Button Clicked** is triggered. |
| imgurl       | String | An URL to the button SVG icon. _To reference **APEX Office Print** icon use_ `#PLUGIN_PREFIX#aop.svg`. |
| label        | String | A text to be displayed when the custom button is hovered.        |
| insertBefore | String | An existing button ID before which a custom button is added. For example: `save`, `print`. Placing a custom button before the existing button is supported only when **Menu Layout** is set to **Classic**. Otherwise, the custom button is added in the toolbar before menu entries. |

An example implementation might look like the following code:

```javascript
function( pOptions ) {
  pOptions.buttons             = [];
  pOptions.menuHideItems       = [];
  pOptions.hideSidebar         = false;
  pOptions.hideMenu            = false;
  pOptions.hideRuler           = false;
  pOptions.logPrefixAsStaticId = false;  
  pOptions.height              = 500;
  pOptions.zoomLevel           = 10;  

  pOptions.buttons.push({
    "id": "aop",
    "imgurl": "#PLUGIN_FILES#aop.svg",
    "label": "APEX Office Print",
    "insertBefore": "print"
  });

  return pOptions;
}
```

### **menuHideItems** `Array`

An `Array` of menu entries IDs. The menu customization works only when the attribute **Menu layout** is set to **Classic**. The list of menu entries is the following:

* menu **File** IDs: _file, save, saveas, downloadas, print, closedocument_
* menu **Edit** IDs: _editmenu, repair, changesmenu_
* menu **View** IDs: _view, fullscreen, zoomin, zoomout, zoomreset, showruler, showresolved_
* menu **Insert** IDs: _insert, insertgraphic, insertcomment, insertsection, inserthyperlink_
* menu **Format** IDs: _format_
* menu **Table** IDs: _table_
* menu **Tools** IDs: _tools_
* menu **Help** IDs: _help, online, keyboard, report, about, last-mod_

### **hideMenu** `Boolean`

Flag determining whether the document editor menu is displayed.

### **hideRuler** `Boolean`

Flag determining whether the document editor shows ruler.

### **logPrefixAsStaticId** `Boolean`

Flag determining whether the plug-in widget produces JavaScript logs (in application debug mode) using region static ID as the prefix or is using the default prefix. Enabling this property is helpful when debugging multiple instances of the plug-in on the same page.

### **height** `Number`

The document editor's default height in `pixels`.

### **zoomLevel** `Number`

The list of zoom levels to be used for the is listed below:

*   level **1** = **20%**
*   level **2** = **25%**
*   level **3** = **30%**
*   level **4** = **35%**
*   level **5** = **40%**
*   level **6** = **50%**
*   level **7** = **60%**
*   level **8** = **70%**
*   level **9** = **85%**
*   level **10** = **100%**
*   level **11** = **120%**
*   level **12** = **150%**
*   level **13** = **170%**
*   level **14** = **200%**
*   level **15** = **235%**
*   level **16** = **280%**
*   level **17** = **335%**
*   level **18** = **400%**
*   level **19** = **400%**
*   level **20** = **400%**

# Events

The plug-in exposes events that can be bound using APEX dynamic actions. The plug-in events are triggered on the DOM node with the class attribute set to **uc-aoe--widget**.

## AOE Before Update

The event `ucaoebeforeactionsave` is triggered when the end-user initializes updating the contents of a document using the AOE editor UI (or after performing the **CTRL+S** shortcut).

The event is triggered without any additional data and it serves only an informative purpose indicating AOE starts updating the current document.

## AOE After Update

The event `ucaoeafteractionsave` is triggered when a document is successfully saved by the REST handler updating document contents.

The event is triggered along with the data described in the table below.

| **Property** | **Type** | **Description** |
| :-- | :-- | :-- |
| this.data.**success** | Boolean | Boolean flag indicating if updating document contents was successful |
| this.data.**msg** | JSON | JSON object containing postMessage `UC_Message` triggering the event |

## AOE Before Save As

The event `ucaoebeforeactionsaveas` is triggered when the end-user provides a new filename and after clicking the button **Save as** in the plug-in dialog **Save as a new document**.

The event is triggered without any additional data and it serves only an informative purpose indicating AOE starts saving a document as a new document with a given filename.

## AOE After Save As

The event `ucaoeafteractionsaveas` is triggered when the plug-in REST handler finishes processing the end-user request saving a document as a new file. The event is triggered along with the data described in the table below.

| **Property**           | **Type** | **Description**                                              |
| :--------------------- | :------- | :----------------------------------------------------------- |
| this.data.**success**  | Boolean  | Boolean flag indicating if saving a document as a new file was successful |
| this.data.**msg**      | JSON     | JSON object containing postMessage `UC_Message` triggering the event |
| this.data.**reloaded** | Boolean  | Boolean flag indicating if AOE editor already reloaded the document |

When saving a document as a new file **is successful** the event is triggered twice. The first event is triggered with `this.data.reloaded` set to `false` and the second event is triggered with `this.data.reloaded` set to `true` when AOE finishes loading a new document.

## AOE Button Clicked

The event `ucaoebuttonclicked` is triggered when a custom button is clicked by the end-user.

The event is triggered along with the data described in the table below.

| **Property** | **Type** | **Description** |
| :-- | :-- | :-- |
| this.data.**buttonId** | String | A button ID given by a developer |
| this.data.**msg** | JSON | JSON object containing postMessage UC\_Message triggering the event |
| this.data.**document** | JSON | JSON object containing a loaded document meta-data returned by the plug-in REST handler |
| this.data.document.**lastUpdate** | String | The date of a document last update time in format `YYYY-MM-DD HH24:MI:SS` |
| this.data.document.**size** | Number | A document size in bytes |
| this.data.document.**filename** | String | A document current filename |
| this.data.document.**version** | Number | A document current version |
| this.data.document.**pksColumns** | String | The column(s) name(s) defined as primary key(s)<br><br>**When attribute Settings \\ Custom table is not checked**<br />the value is always `ID`<br>    <br>**When attribute Settings \\ Custom table is checked**<br />the value of the plug-in region attribute **Item(s) Containing Primary Key(s) Value(s)** |
| this.data.document.**pksValues** | String | The current value(s) of primary key(s)<br /><br />**When attribute Settings \\ Custom table is not checked**<br />the value stored in APEX Session State for item defined in the plug-in region attribute **Item Containing Primary Key Value**<br>    <br>**When attribute Settings \\ Custom table is checked**<br />the value stored in APEX Session State for item defined in the plug-in region attribute **Item(s) Containing Primary Key(s) Value(s)** |

## AOE Document Loaded

The event `ucaoedocumentloaded` is triggered every time a document is successfully loaded into the APEX Office Edit.

The event is triggered along with the data described in the table below.

| **Property** | **Type** | **Description** |
| :-- | :-- | :-- |
| this.data.**document** | JSON | JSON object containing a loaded document meta-data returned by the plug-in REST handler |
| this.data.document.**lastUpdate** | String | The date of a document last update time in format `YYYY-MM-DD HH24:MI:SS` |
| this.data.document.**size** | Number | A document size in bytes |
| this.data.document.**filename** | String | A document current filename |
| this.data.document.**version** | Number | A document current version |
| this.data.document.**pksColumns** | String | The column(s) name(s) defined as primary key(s)<br><br>**When attribute Settings \\ Custom table is not checked**<br />the value is always `ID`<br>    <br>**When attribute Settings \\ Custom table is checked**<br />the value of the plug-in region attribute **Item(s) Containing Primary Key(s) Value(s)** |
| this.data.document.**pksValues** | String | The current value(s) of primary key(s)<br><br>**When attribute Settings \\ Custom table is not checked**<br />the value stored in APEX Session State for item defined in the plug-in region attribute **Item Containing Primary Key Value**<br>    <br>**When attribute Settings \\ Custom table is checked**<br />the value stored in APEX Session State for item defined in the plug-in region attribute **Item(s) Containing Primary Key(s) Value(s)** |

## AOE Initialized

The event `ucaoeinitialized` is triggered as the result of the plug-in initialization process (the plug-in waits for the iframe **ready event** and then waits for postMessage **App\_LoadingStatus**). After receiving **App\_LoadingStatus** postMessage it is safe to assume that APEX Office Edit is initialized and the plug-in triggers the AOE Initialized event.

The event is triggered without any additional data and it serves only an informative purpose indicating AOE editor is ready to be used by the end-user.

## AOE Message

The event `ucaoemessage` is triggered each time the plug-in receives the postMessage sent by the APEX Office Edit host server. Messages are used to communicate between AOE hosts with the plug-in implemented in an application.

The event is triggered along with the data described in the table below.

| **Property** | **Type** | **Description** |
| :-- | :-- | :-- |
| this.data.msg.**MessageId** | String | The unique message ID |
| this.data.msg.**SendTime** | Number | Time stamp when message is sent (result of browser `Date.now()`) |
| this.data.msg.**Values** | JSON | JSON object containing message data. Message data differs depending on message. |

# Translation Messages

Some parts of the APEX Office Edit can be translated using **Oracle APEX Translation Texts**. 

| Translation Code                                 | Translation default text                                     |
| ------------------------------------------------ | ------------------------------------------------------------ |
| UC_AOE_DIALOG_SAVE_BUTTON_CANCEL                 | Cancel                                                       |
| UC_AOE_DIALOG_SAVE_BUTTON_SAVE_AS                | Save as                                                      |
| UC_AOE_DIALOG_SAVE_ITEM_FILENAME_LABEL           | Filename                                                     |
| UC_AOE_DIALOG_SAVE_TITLE_SAVE_AS                 | Save as a new document                                       |
| UC_AOE_MASK_ACT_CREATING_A_FILE                  | Creating a new document                                      |
| UC_AOE_MASK_ACT_FILE_CREATED                     | A new document has been created                              |
| UC_AOE_MASK_ACT_FILE_SAVED_LOAD                  | Loading saved document                                       |
| UC_AOE_MASK_ACT_INIT_AS_SAVE                     | Saving document as a new document                            |
| UC_AOE_MASK_ACT_INIT_SAVE                        | Saving a document in progress                                |
| UC_AOE_MASK_ACT_REFRESHING                       | Refreshing                                                   |
| UC_AOE_MASK_AOE_INIT                             | Initializing APEX Office Edit                                |
| UC_AOE_MASK_BTN_CLOSE                            | Close                                                        |
| UC_AOE_MASK_BTN_NEW_FILE_PANEL                   | Create a new file                                            |
| UC_AOE_MASK_BTN_REFRESH                          | Refresh                                                      |
| UC_AOE_MASK_MSG_FILE_LOADED                      | Document loaded                                              |
| UC_AOE_MASK_MSG_FRAME_READY                      | Frame ready                                                  |
| UC_AOE_MASK_MSG_IFRAME_LOADED                    | Iframe loaded                                                |
| UC_AOE_NEW_DOCUMENT_BACK_TO_EDIT                 | Get back to the currently opened document                    |
| UC_AOE_NEW_FILE_BTN_HINT                         | Create a new document                                        |
| UC_AOE_NEW_FILE_BTN_LABEL                        | Create a new document                                        |
| UC_AOE_NEW_FILE_TYPE_TITLE_DOCX                  | Microsoft Word                                               |
| UC_AOE_NEW_FILE_TYPE_TITLE_ODP                   | Open Document Presentation                                   |
| UC_AOE_NEW_FILE_TYPE_TITLE_ODS                   | Open Document Spreadsheet                                    |
| UC_AOE_NEW_FILE_TYPE_TITLE_ODT                   | Open Document Text                                           |
| UC_AOE_NEW_FILE_TYPE_TITLE_PPTX                  | Microsoft PowerPoint                                         |
| UC_AOE_NEW_FILE_TYPE_TITLE_XLSX                  | Microsoft Excel                                              |
| UC_AOE_READONLY_PROMPT_MESSAGE                   | Load a document to preview it.                               |
| UC_AOE_REST_ACCESS_TOKEN_INVALID                 | The invalid access token.                                    |
| UC_AOE_REST_ATTR_INVALID_CFG                     | The plug-in configuration is invalid.                        |
| UC_AOE_REST_FILE_NOT_FOUND                       | Requested document not found.                                |
| UC_AOE_REST_FILE_NOT_TYPE_NOT_ALLOWED            | Document type is not allowed.                                |
| UC_AOE_REST_NOT_RECOGNIZED_HTTP_STATUS           | Not handled HTTP status code. Contact the application administrator. |
| UC_AOE_REST_OTHER_PLSQL_ERROR                    | An unexpected error was raised. Contact the application administrator. |
| UC_AOE_REST_SAVEAS_INV_REQ_HEAD_FILENAMES        | Malformed request header (filenames)                         |
| UC_AOE_REST_SAVEAS_INV_REQ_HEAD_MISSING_FILENAME | Malformed request header (missing filename)                  |
| UC_AOE_REST_SAVEAS_INV_REQ_HEAD_PUT_RELATIVE     | Malformed request header (PUT_RELATIVE).                     |
| UC_AOE_REST_SCOPE_DOC_CONTENT                    | Fetching document contents failed.                           |
| UC_AOE_REST_SCOPE_DOC_META                       | Fetching document meta-data failed.                          |
| UC_AOE_REST_SCOPE_SAVEAS_FAIL                    | Saving document as copy failed.                              |
| UC_AOE_REST_SCOPE_UPDATE_FAIL                    | Updating document contents failed.                           |
| UC_AOE_REST_UNKNOWN_UC_MESSAGE_STATUS            | Not handled plug-in message status.<br/>Contact application  administrator |
| UC_AOE_REST_UPDATE_OK                            | Document saved successfully                                  |
| UC_AOE_REST_UPDATE_STATUS_409                    | Malformed last update time.                                  |
| UC_AOE_REST_USER_CANT_READ_FILE                  | The user is not permitted to read the document.              |
| UC_AOE_VALIDATION_FILENAME_NOT_SET               | Filename is required                                         |