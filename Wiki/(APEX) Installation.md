# Introduction

The plug-in implementing **APEX Office Edit** can be installed in two scenarios:

*   by installing the AOE sample application 
    
*   by executing the DDL script and installing the region plug-in in an existing application (manual installation)
    

# Sample application

## **Importing sample application**

1. Log into your application builder
2. Click on the tile Import tile to start APEX wizard installing application from the application installation file
3. Make sure the schema in which you want to install the sample application is REST enabled

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_1.png?raw=true)

4. Click on the region **Drag and Drop**
5. Select sample application file
6. Click the button **Next**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_2.png?raw=true)

After successfully uploading the application installation file, the APEX shows the wizard confirmation step.

1. Click the button **Next**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_3.png?raw=true)

## Set application installation settings

1. Configure or use default values in the form
2. Click the button **Install Application**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_4.png?raw=true)

3. Don’t close the page - wait until APEX finishes installing the application. When installing the application you will be redirected to the next step.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_5.png?raw=true)

4. Make sure switch **Install Supporting Objects** **is checked** - in order to install the sample application all sample application supporting objects must be installed successfully
5. Click the button **Next**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_6.png?raw=true)

6. Click the button **Install**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_7.png?raw=true)

7. Don’t close the page - wait until APEX finishes installing supporting objects. When installing supporting objects you will be redirected to the next step

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_8.png?raw=true)

8. When the sample application installation is finished, the APEX wizard confirmation screen is displayed.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_9.png?raw=true)

9. If the installation is terminated by error it can be verified after clicking the button **Install Summary** - summary presents the status of installing all supporting objects.  

10. When the sample application installation is successful, the last step is to update the plug-in component settings for the RESTful service installed by the sample application supporting objects.

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_imp_sample_app_10.png?raw=true)

## Configure the plug-in RESTful service

In order to finish the sample application installation, it is required to configure the plug-in RESTful service

1. Fill in the instructions described in **The plug-in REST service configuration**
2. Test the sample application

## Testing the sample application

1. Run the AOE sample application
2. Click on a document type tile you wish to create
3. The AOE should create a document of selected type

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_test_1.png?raw=true)

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_test_2.png?raw=true)

***

# Manual installation

## Running installation DDL Script

1. From the APEX application builder top menu bar select **SQL Workshops** and then **SQL Scripts**
2. Click button **Upload**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_1.png?raw=true)

3. In the **Upload Script dialog** click on item **File** and select the AOE installation file `ddl_unitedcodes_apex_office_edit.sql`
2. Click the button **Upload**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_2.png?raw=true)

5. After the script is successfully uploaded click the button **Run**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_3.png?raw=true)

6. In the confirmation screen click the button **Run now**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_4.png?raw=true)

7. Examine script installation summary - the script should not raise any errors
7. Proceed to the next step **Installing the plug-in in an existing example application**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_script_5.png?raw=true)

## Installing the plug-in in an existing example application

1. Go to APEX application builder home page
2. Select the application in which you want to use **APEX Office Edit**
3. Go to **Shared Components \ Plug-ins**
4. Click the button **Import**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_1.png?raw=true)

5. Click on the region **Drag and Drop** to select the AOE region plug-in installation file `region_type_plugin_unitedcodes_aoe.sql`
6. Click the button **Next**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_2.png?raw=true)

7. In **File Import Confirmation** step click the button **Next**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_3.png?raw=true)

8. In **Install Plug-in** step click the button **Install Plug-in**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_manual_plug_4.png?raw=true)

After successful installation, the plug-in component settings must be updated. Go to the next step **The plug-in REST service configuration**.

In order to create the first AOE instance please follow instructions **Creating the plug-in instance in an existing application**

## Configure the plug-in RESTful service

In order to finish the sample application installation, it is required to configure the plug-in RESTful service:

1. Fill in the instructions described in **The plug-in REST service configuration**
2. Test the sample application

## Implement the plug-in in an existing application

In order to create the first instance of the AOE please go to the instructions described in section **Getting started \ Creating the plug-in instance in an existing application**.

# The plug-in REST service configuration

1. Go to an application **Shared Components**
2. Go to **Other Components \\ Plug-ins**
3. Click on the region plug-in **UC - APEX Office Edit (AOE)**
4. Read help texts for attributes **Server-Side URL(Value Required** and **URL to RESTful service module(Value Required)**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_plug_comp_1.png?raw=true)

6. From the APEX application builder top menu bar select **SQL Workshops** and then **RESTful services**
7. Select module **APEX Office Edit**
8. Copy the value of an **Full URL** module attribute

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_plug_comp_2.png?raw=true)

9. Go back to the plug-in component settings
10. Replace the attribute **URL to RESTful service module** default value ()`[http://www.apexrnd.be/ords181/aoe/aoe/files/` ) with the value copied in **step 8**  (the attribute **Full URL** of AOE RESTful service module)
11. Add suffix `files/`
12. Click the button **Apply Changes**

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_plug_comp_3.png?raw=true)

![](https://github.com/United-Codes/apexofficeedit-public/blob/main/images/docs/get_start_app_plug_comp_4.png?raw=true)

