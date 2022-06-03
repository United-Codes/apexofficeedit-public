This section describes first steps with APEX Office Edit from the perspective of Oracle APEX.

# Installation

The plug-in implementing APEX Office Edit can be installed in two scenarios:

*   installation through installing APEX Office Edit sample application
    
*   installation using DDL script and the Oracle APEX plug-in installation file (manual installation)
    

## Sample application

### **Importing sample application**

1. Log into your application builder
2. Click on the tile Import to start APEX wizard installing application from the application installation file
3. Make sure the schema in which you want to install sample application is REST enabled

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_1.png?raw=true)

4. Click on the region “Drag and Drop”
5. Select sample application file
6. Click the button “Next”

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_2.png?raw=true)

7.  Click on the region “Drag and Drop”
8.  Select sample application file
9.  Click the button “Next”

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_3.png?raw=true)

### Install sample application

After successful uploading the application installation file, the APEX shows confirmation step.

1. Click the button “Next”
2. Configure or use default values in the form
3. Click the button “Install Application”
4. 

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_4.png?raw=true)

4. Don’t close the page
5. Wait until APEX finishes installing the application. When installing the application you will be redirected to the next step.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_5.png?raw=true)



In order to run the sample application, all sample application supporting objects must be installed

In order to run the sample application, all sample application supporting objects must be installed.

6. Make sure switch “Install Supporting Objects” is checked
2. Click the button “Next”

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_6.png?raw=true)

8. Click the button “Install”

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_7.png?raw=true)

1. Don’t close the page
2. Wait until APEX finishes installing supporting objects. When installing supporting objects you will be redirected to the next step.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_8.png?raw=true)

When installation is finished (the sample application and supporting objects are installed), the confirmation screen is displayed.

If any error occurred while installing the sample application you will be prompted about errors and you can verify supporting objects installation by clicking the button “Install Summary”.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_9.png?raw=true)

In this screen you can see all errors. If no errors are raised the sample application is successfully installed and the last step is to update the REST URL in freshly installed application.<br>

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_10.png?raw=true)

### The plug-in REST service configuration

1. Go to application Shared Components
2. Go to Other Components \\ Plug-ins
3. Select region plug-in UC - APEX Office Edit (AOE)
4. Read help texts for attributes “Server-Side URL(Value Required)” and “URL to RESTful service module(Value Required)“
5. Proceed to the next step in this instruction

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_plug_comp_1.png?raw=true)

1. From the top bar menu select SQL Workshops \ RESTful services
2. Select module APEX Office Edit
3. Copy value of an “Full URL” module attribute
4. Go back to the plug-in component settings from this instruction previous step

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_plug_comp_2.png?raw=true)

1. Replace the default value “[http://www.apexrnd.be/ords181/aoe/aoe/files/”](https://united-codes.atlassian.net/wiki/spaces/UCAOE/pages/1966374926/Getting+started#) with the “Full URL” copied in this instructions previous step (preserve the suffix “files/”)
2. Click the button “Apply Changes”

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_plug_comp_3.png?raw=true)

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_plug_comp_4.png?raw=true)

### Testing the sample application

1. Run the sample application
2. Click on document icon you wish to create
3. If configuring the plug-in component settings was done right, a new document should be created and opened in the plug-in editor

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_test_1.png?raw=true)

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_test_2.png?raw=true)

## Manual installation

### Running installation DDL Script

1. Go to SQL Workshop \ SQL Scripts
2. Click button Upload

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_1.png?raw=true)

3. In the Upload Script select installation file ddl_unitedcodes_apex_office_edit.sql
2. Click the button Upload

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_2.png?raw=true)

5. After the script is successfuly uploaded click the button Run

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_3.png?raw=true)

6. On the confirmation screen click the button Run now

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_4.png?raw=true)

7. Execution of the script should not raise errors

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_5.png?raw=true)

### Installing the plug-in in an example application

1. Go to APEX application builder home page
2. Select the application in which you want to use APEX Office Edit
3. Go to Shared Components \ Plug-ins
4. Click the button Import

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_1.png?raw=true)

5. In import step select the APEX Office Edit plug-in installation file **region_type_plugin_unitedcodes_aoe.sql**
2. Click the button Next

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_2.png?raw=true)

7. In import **File Import Confirmation** step click the button Next

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_3.png?raw=true)

8. In import **Install Plug-in** step click the button Install Plug-in

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_4.png?raw=true)

After successful installation you need to update the plug-in component settings. Go to the next step 

### The plug-in REST service configuration

1. Go to application Shared Components
2. Go to Other Components \\ Plug-ins
3. Select region plug-in UC - APEX Office Edit (AOE)
4. Read help texts for attributes “Server-Side URL(Value Required)” and “URL to RESTful service module(Value Required)“
5. Proceed to the next step in this instruction

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_comp_1.png?raw=true)

6. From the top bar menu select SQL Workshops \ RESTful services
2. Select module APEX Office Edit
3. Copy value of an “Full URL” module attribute
4. Go back to the plug-in component settings from this instruction previous step

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_comp_2.png?raw=true)

10. Replace the default value “[http://www.apexrnd.be/ords181/aoe/aoe/files/”](https://united-codes.atlassian.net/wiki/spaces/UCAOE/pages/1966374926/Getting+started#) with the “Full URL” copied in this instructions previous step (preserve the suffix “files/”)
2. Click the button “Apply Changes”

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_comp_3.png?raw=true)

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_comp_4.png?raw=true)

In order to create first APEX Office instance please follow instruction **Creating the plug-in instance in an existing application**

# Creating the plug-in instance in an existing application

This section describes first steps how to create the plug-in instance implementing APEX Office Edit. If any plug-in attribute purpose is not clear please read help texts defined for each attribute.

## Default table

|     |     |     |
| --- | --- | --- |
|     |     |     |
| 1   | 1.  Create a new empty page | ![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-124409.png?api=v2) |
| 2   | Create the plug-in region<br><br>1.  Create a new region<br>    <br>2.  Set **Identification \\ Title** to **APEX Office Edit on default table**<br>    <br>3.  Change **Indentification \\ Type** to **UC - APEX Office Edit (AOE) \[Plug-in\]** | ![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-124605.png?api=v2) |
| 3   | Create APEX item containing document ID<br><br>1.  Create page item<br>    <br>2.  Set **Identification \\ Name** to **P4\_DOCUMENT\_ID**<br>    <br>3.  Change **Type** to **Hidden**<br>    <br>4.  Set **Settings \\ Value Protected** to **No** | ![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-125058.png?api=v2) |
| 4   | Configure the plug-in<br><br>1.  Go to region **APEX Office Edit on default table \\ Attributes**<br>    <br>2.  Set **Item Containing Primary Key Value** to **P4\_DOCUMENT\_ID**<br>    <br>3.  Save and run the page | ![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220513-161642.png?api=v2) |
| 5   | In the result, the plug-in is prepared to start creating a first document. Clicking on document icon creates a blank document of selected type.<br><br>Continue basic implementation in section **Loading documents into APEX Office Edit** | ![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-125617.png?api=v2)![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-125814.png?api=v2) |

# Loading documents into APEX Office Edit

This section describes first steps how to load document into APEX Office Edit. The plug-in state is based on APEX Session State for page items defined as primary key(s). If the given item(s) is/are NULL the plug-in shows panel allowing the end-user to create a new document. In order to load document to the APEX Office Edit, item(s) must not be NULL, and the plug-in configuration must be valid.

## Default table

The instructions presented below are meant to be the continuation of **Creating the plug-in instance in an existing application**.

|     |     |     |
| --- | --- | --- |
|     |     |     |
| 1   | **Create classic report showing all created files**<br><br>1.  Create a new page region<br>    <br>2.  Set **Identification \\ Title** to **All files**<br>    <br>3.  Set **Indentification \\ Type** to **Classic Report**<br>    <br>4.  Set **Source \\ Table Name** to **AOE\_FILES\_DEFAULT**<br>    <br>5.  Select column **CONTENT** in **All files \\ Columns tree**<br>    <br>6.  Set **Identification \\ Type** to **Hidden Column**<br>    <br><br>**Define link on column FILENAME**<br><br>1.  Select column **FILENAME in All files \\ Columns tree**<br>    <br>2.  Set **Identification \\ Type** to **Link**<br>    <br>3.  Click button **No Link Defined** in **Link \\ Target**<br>    <br>4.  Set **Target \\ Type** to **URL**<br>    <br>5.  Set **URL** to javascript:<br>    <br>    ```<br>    javascript: apex.event.trigger(document, 'loaddocument', #ID#);<br>    ```<br>    <br>6.  Click button **OK**<br>    <br>7.  Go to the next step to create a dynamic action | ![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-130800.png?api=v2)![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-131152.png?api=v2)![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-132936.png?api=v2) |
| 2   | **Create dynamic action enforcing loading a file**<br><br>1.  Create a new dynamic action<br>    <br>2.  Set **Identification \\ Name** to **Load document**<br>    <br>3.  Set **When \\ Event** to **Custom**<br>    <br>4.  Set **When \\ Custom Event** to **loaddocument**<br>    <br>5.  Set **When \\ Selection Type** to **JavaScript Expression**<br>    <br>6.  Set **When \\ JavaScript Expression** to **document**<br>    <br><br>**Define true actions**<br><br>1.  Select default **Show** action<br>    <br>2.  Set **Identification \\ Action** to **Set Value**<br>    <br>3.  Set **Settings \\ Set Type** to **JavaScript Expression**<br>    <br>4.  Set **Settings \\ JavaScript Expression** to **this.data**<br>    <br>5.  Set **Affected Elements \\ Item(s)** to **P4\_DOCUMENT\_ID**<br>    <br>6.  Set **Execution Options \\ Fire on Initialization** to **No**<br>    <br>7.  Create a new true action<br>    <br>8.  Set **Identification \\ Action** to **Refresh**<br>    <br>9.  Set **Affected Elements \\ Selection Type** to **Region**<br>    <br>10.  Set **Affected Elements \\ Region** to **APEX Office Edit on default table**<br>    <br>11.  Move region All files above region APEX Office Edit on default table<br>    <br>12.  Save and run the page<br>    <br><br>Region column filename contains links. Clicking on link will force APEX Office Edit to load selected document by setting primary key item and refreshing region implementing the plug-in. | ![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-132125.png?api=v2)![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-132548.png?api=v2)![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-133122.png?api=v2)![](https://united-codes.atlassian.net/wiki/download/attachments/1966374926/image-20220510-133733.png?api=v2) |