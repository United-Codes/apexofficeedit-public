# Default table

By the default, the plug-in uses default table **AOE\_FILES\_DEFAULT** to store documents. The default table uses sequence **AOE\_FILES\_DEFAULT\_SEQ** and trigger **BI\_AOE\_FILES\_DEFAULT**. The default table, trigger and sequence are created along with sample application and by the plug-in DDL installation script.

| **Column Name** | **Data Type** | **Nullable** | **Primary Key** | **Description** |
| :-- | :-- | :-: | :-: | :-- |
| ID  | NUMBER | ![(error)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/error.png) | ![(tick)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/check.png) | Column is used to uniquely identify a document |
| CONTENT | BLOB | ![(tick)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/check.png) | ![(error)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/error.png) | Column is used to store a document contents |
| FILENAME | VARCHAR2(200) | ![(tick)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/check.png) | ![(error)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/error.png) | Column is used to store a document filename |
| MIME\_TYPE | VARCHAR2(200) | ![(tick)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/check.png) | ![(error)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/error.png) | Column is used to store a document MIME-type |
| BLOB\_OWNER | VARCHAR2(50) | ![(tick)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/check.png) | ![(error)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/error.png) | Column is used to store a document owner name |
| VERSION | NUMBER | ![(tick)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/check.png) | ![(error)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/error.png) | Column is used to store a document current version |
| LAST\_UPDATE\_DATE | TIMESTAMP(6) | ![(tick)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/check.png) | ![(error)](https://united-codes.atlassian.net/wiki/s/1607903193/6452/cc22dcd50a41cdc02a85aec87a200df397e2c555/_/images/icons/emoticons/error.png) | Column is used to store a document last modification time |

# Flows

Creating, loading, and updating documents are the result of communication between the AOE host server and the plug-in through the plug-in Oracle REST service handlers. If the process is interrupted by PL/SQL error raised by the RESTful Service handler, the plug-in shows a user-friendly error to the end-user described in [RESTful service \ Error Handling](https://github.com/United-Codes/apexofficeedit-public/wiki/RESTful-service#error-handling).

**The flows described below are illustrative and should be considered as-is.**

## Loading documents

1.  The end-user initializes loading a document (for example through a classic report showing all documents)
    
    1.  A page item defined for the plug-in attribute **Item Containing Primary Key Value** is set with document ID
        
    2.  A region implementing the plug-in is refreshed
        
    3.  The plug-in creates the AOE access token containing information about the requested document
        
    4.  The plug-in refreshes iframe referencing AOE host server files
    
2.  AOE interprets the access token generated for the file to be loaded
    
3.  AOE host server initializes request to the plug-in RESTful Service in order to fetch document meta-data
    
    1.  REST service handler evaluates the plug-in configuration delivered through the access token (access token validity, end-user permissions, region read-only mode)
        
    2.  REST service handler returns document meta-data
    
4.  AOE host server interprets returned information and initializes request to the plug-in RESTful Service to fetch document contents
    
    1.  REST service handler fetches a document BLOB based on the plug-in access token information
        
    2.  REST service handler returns a document's contents
    
5.  AOE host server renders AOE editor with document opened
    
6.  AOE host server sends postMessage indicating document loading
    
7.  The plug-in triggers the event **AOE Document loaded**
    

## Creating a new document

1.  The end-user initializes creating a new document
    
    1.  The plug-in requests the plug-in REST Service handler to create a new document in the table specified by the plug-in attributes
        
    2.  REST service handler evaluates the plug-in configuration delivered through the access token (access token validity, default filename)
        
    3.  REST service handler checks if the default filename is already taken. If yes it assigns a new filename using the first available number in brackets.  
        _For example, the default filename is **New file**, but the filename is already taken so a new document filename is **New file (1)**_
        
    4.  REST service handler inserts blank document contents in the defined table
        
    5.  REST service handler executed update callback (if defined)
        
    6.  REST service handler returns document meta-data
    
2.  The plug-in evaluates the response from the RESTful service handler
    
    1.  A page item defined for the plug-in attribute **Item Containing Primary Key Value** is set with document ID
        
    2.  A region implementing the plug-in is refreshed
        
    3.  Go to flow **Loading documents**
        

## Saving document content

1.  The end-user clicks the button **Save** (or click menu position **File \\ Save**)
    
    1.  The plug-in sends postMessage to the AOE host server to update documents contents
        
    2.  The plug-in triggers the event **AOE Before Update**
    
2.  AOE host server initializes request to RESTful Service in order to save document contents
    
    1.  REST service handler evaluates the plug-in configuration delivered through the access token
        
    2.  REST service handler updates document contents in the defined table
        
    3.  REST service handler executed update callback (if defined) with parameters indicating a document was updated
        
    4.  REST service handler returns document modification time
    
3.  AOE host server interprets the result and enables the end-user to continue work on a document.
    
4.  AOE host server sends postMessage indicating that document was updated
    
5.  The plug-in triggers the event **AOE After Update**
    

## Saving document as a new file

1.  The end-user clicks the button **Save As** (or click menu position **File \\ Save As**)
    
    1.  The plug-in shows a dialog with a form to save a document with a new filename
        
    2.  The end-user provides a new filename
        
    3.  the end-user click the dialog button **Save as**
        
    4.  The plug-in sends postMessage to the AOE host server to save a document as a new file with the given filename
        
    5.  The plug-in triggers the event **AOE Before Save As**
    
2.  AOE host server initializes request to RESTful Service in order to save a document as a new file
    
    1.  REST service handler evaluates the plug-in configuration delivered through the access token
        
    2.  REST service handler checks if the filename is already taken. If yes it assigns a new filename using the first available number in brackets.  
        _For example, the end-user provided the filename **New file**, but the filename is already taken so the new filename assigned is **New file (1)**_
        
    3.  REST service handler inserts an updated document with a new filename
        
    4.  REST service handler executes an update callback (if defined) with parameters indicating a document was saved as a new document
        
    5.  REST service handler generates and returns an access token for a new document along with other document meta-data
    
3.  AOE host server interprets the result and sends postMessage indicating that the document was saved as a new document with a new filename
    
4.  The plug-in triggers the event **AOE After Save As** with property reloaded set to **false**
    
5.  AOE host server reloads a document and sends postMessage indicating that the document was reloaded
    
6.  The plug-in triggers the event **AOE After Save As** with property reloaded set to **true**
    
