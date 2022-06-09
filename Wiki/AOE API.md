# API
## Post Messages
### AOE Editor to Host
#### UC\_Message

A post message with “UC\_Message” is fired.

|Key|Value|
| :- | :- |
|msgId|string (always UC\_Message)|
|args|Object<br><table><tr><th>Key</th><th>Value</th></tr><tr><td>success</td><td>boolean</td></tr><tr><td>status</td><td>string</td></tr><tr><td>json</td><td>boolean</td></tr><tr><td>httpResponseCode</td><td>number</td></tr><tr><td>responseParsed</td><td>boolean</td></tr><tr><td>message</td><td>string</td></tr><tr><td>UC_Data</td><td>string \| object</td></tr></table>|


Details:

<table class="custom_td"><tr><td>msgId</td>
<td>
It denotes the type of post message. <br>
Here “UC_Message” refers to the post message which is sent whenever there is some action performed like save, rename, save as or some license details or access token of the document.
</td></tr><tr><td>args</td>
<td >
It denotes the arguments of the message.
</td></tr></table>
Whenever there is UC_Message as message id following arguments object keys are sent:

<table class="custom_td"><tr><td>
success
</td><td>
It's value can be true or false. <br>
It denotes whether the operation performed was successful or not.
<br><i>Example: To save a file key combination Ctrl+S is pressed but due to some error file cannot be saved, then there will be a post message with success value as false. If the file is saved successfully then the success value will be true.</i>
</td></tr><tr><td>
status</td><td>
It denotes the various status codes which are as follows:
<table><tr><th>Status Code</th><th>Meaning</th></tr>
<tr><td>ERRJSONPARSE </td><td> Message cannot be parsed</td></tr>
<tr><td>MSGACSTKN </td><td> Change in Access token </td></tr>
<tr><td>MSGSAVE </td><td> Save file</td></tr>
<tr><td>MSGSAVEAS </td><td> Save As file</td></tr>
<tr><td>MSGRENAME </td><td> Rename file</td></tr>
<tr><td>LMTRCHD</td><td> License limit reached <br>(maximum number of concurrent connection)</td></tr>
<tr><td>OOC</td><td> Out of credits.Consider adding credits.</td></tr>
<tr><td>EXPIRED</td><td> License expired for given api key.</td></tr>
<tr><td>INVALIDAPI</td><td> Invalid API key provided.</td></tr>
<tr><td>ERRUNKNOWN</td><td> Unexpected unknown error (default)</td></tr></table>
</td></tr><tr><td>
json</td><td>
It denotes whether the content is parsed correctly or not. It is false when the whole message or uc data cannot be parsed.
</td></tr><tr><td>
httpResponseCode </td>
<td>
Standard http response codes: <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status" target= "_blank">MDN | HTTP response status codes</a>
<br>
0 means no response.
</td></tr><tr><td>
reponseParsed
</td><td>
Denotes if response was parsed or not.
<br/>
If a response was sent and if it’s false then this represents the response wasn’t able to parse. Please check the response object.
</td></tr><tr><td>
message</td><td>
CustomMessage sent from oracle application.
</td></tr><tr><td>
uc_data
</td><td>
UC_Data sent from oracle application.
<br/>
It can be a string or object, depending on what is set on the oracle application.
</td></tr>
</table>

<hr/>

#### UC\_Data


|Key|Value|
| :- | :- |
|msgId|string (always UC\_Data)|
|args|Object<br><table><thead><tr><th>Key</th><th>Value</th></tr></thead><tbody><tr><td>success</td><td>boolean</td></tr><tr><td>json</td><td>boolean</td></tr><tr><td>message</td><td>string \| object</td></tr></tbody></table>|


Details:
<table class="custom_td"><tr><td>msgId</td><td>
It denotes the type of post message. 
<br>
Here “UC_Data” refers to the post message which is sent whenever UC_Data is detected on the response string.
</td></tr><tr><td>
args </td>
<td>
It denotes the arguments of the message.
</td></tr></table>

Whenever there is UC_Data as message id following arguments object keys are sent:
<table class="custom_td"><tr><td>
success</td><td>
It denotes whether the operation performed was successful or not.
</td></tr><tr><td>
json
</td><td>
It denotes whether the content is parsed correctly or not. It is false when the uc data cannot be parsed.
</td></tr><tr><td>
message
</td><td>
UC_Data sent from oracle application.
</td></tr></table>
<hr/>

#### UC\_Error


|Key|Value|
| :- | :- |
|msgId|string (always UC\_Error)|
|args|Object<br><table><thead><tr><th>Key</th><th>Value</th></tr></thead><tbody><tr><td>success</td><td>boolean (always false)</td></tr><tr><td>status</td><td>string</td></tr><tr><td>errorMessage</td><td>string</td></tr><tr><td>[key: string]</td><td>[value: any] (these has socket on close data )</td></tr></tbody></table>|



Details:
<table class="custom_td"><tr><td>msgId</td><td>
It denotes the type of post message. <br>
Here “UC_Error” refers to the post message which is sent whenever there is an error while closing the socket.
</td></tr><tr><td>args</td><td>
It denotes the arguments of the message.
</td></tr></table>
Whenever there is UC_Error as message id following arguments object keys are sent:

<table class="custom_id"><tr><td>success</td>
<td>
It denotes whether the operation performed was successful or not.
</td></tr><tr><td>
status
</td><td>
Status code is ERRSOCKETCLOSE
</td></tr><tr><td>
errorMessage</td><td>
Error string message.
</td></tr><tr><td colspan="2">
Other keys and values from socket close events.
</td></tr></table>
<hr/>

#### MSGALERT


|Key|Value|
| :- | :- |
|msgId|string (always MSGALERT)|
|args|Object<br><table><thead><tr><th>Key</th><th>Value</th></tr></thead><tbody><tr><td>msg</td><td>string</td></tr></tbody></table>|


Details:
<table class="custom_td"><tr><td>msgId</td><td>
It denotes the type of post message. 
<br>
Here “MSGALERT” refers to the post message which is only sent when Show_Custom_Message_Dialog flag is set to false, and every warning messages will not be shown as dialog message instead it will be a post message.
</td></tr><tr><td>
args </td><td>
It denotes the arguments of the message.
</td></tr><tr></table>
Whenever there is MSGALERT as message id following arguments object keys are sent:
<table class="custom_td"><tr><td>
msg</td><td>
Message value will be text that would be shown if there was a dialog message. 
</td></tr></table>
<hr/>

### Host to AOE Editor

#### Show Custom Message Dialog
|Key|Value|
| :- | :- |
|MessageId|string (Show\_Custom\_Message\_Dialog)|
|Value|object<br><table><thead><tr><th>Key</th><th>Value</th></tr></thead><tbody><tr><td>Flag</td><td>boolean</td></tr></tbody></table>|

Details:
<table class="custom_td"><tr><td>
MessageId
</td><td>
It denotes the type of post message. 
<br>
Here “Show_Custom_Message_Dialog” refers to the post message which can be sent to AOE Editor to show/hide custom message dialog.
</td></tr><tr><td>
Value 
</td><td>
It denotes the value of the message
</td></tr></table>
Whenever there is Show\_Custom\_Message\_Dialog as message id following arguments object keys should be passed with it.
<table class="custom_td"><tr><td>
Flag</td><td>
Flag true shows the custom message dialog whereas flag false hides the custom message.
</td></tr></table>
**Reponse**: No response is received from the AOE Editor, it will just show/hide the next dialog messages.

<hr/>

#### Sidebar Visibility

|Key|Value|
| :- | :- |
|MessageId|string (Side\_Bar\_Visibility)|
|Value|object<br><table><thead><tr><th>Key</th><th>Value</th></tr></thead><tbody><tr><td>Flag</td><td>boolean</td></tr></tbody></table>|

Details:
<table class="custom_td"><tr><td>
MessageId
</td><td>
It denotes the type of post message. 
<br>
Here “Side_Bar_Visibility” refers to the post message which can be sent to the AOE Editor to show/hide the sidebar.
</td></tr><tr><td>
Value 
</td><td>
It denotes the value of the message
</td></tr></table>
Whenever there is Side\_Bar\_Visibility as message id following arguments object keys should be passed with it.
<table class="cutom_td"> <tr><td>
Flag</td>
<td>
Flag true shows the sidebar whereas flag false hides the sidebar.
</td></tr></table>
**Reponse**: No response is received from the AOE Editor, it will just show/hide the sidebar.

<hr/>

#### Get Access Token


|Key|Value|
| :- | :- |
|MessageId|string (Get\_Access\_Token)|

Details:
<table class="custom_td"><tr><td>
MessageId
</td><td>
It denotes the type of post message. 
<br>
Here “Get_Access_Token” refers to the post message which can be sent to the AOE Editor to get the access token of the current document.
</td></tr></table>
**Reponse**: AOE Editor  sends a post message to the host with message id UC\_Message and status as “REQACSTKN”


|Key|Value|
| :- | :- |
|msgId|string (always UC\_Message)|
|args|Object<br><table><tr><th>Key</th><th>Value</th></tr><tr><td>success</td><td>boolean</td></tr><tr><td>status</td><td>string (REQACSTKN)</td></tr><tr><td>message</td><td>string</td></tr></table>|

Details:
<table class="custom_td"><tr><td>
msgId
</td><td>
It denotes the type of post message. 
<br>
Here “UC_Message” refers to the post message.
</td><tr></tr><td>
args 
</td><td>
It denotes the arguments of the message.
</td></tr><tr><td>
success
</td><td>
It denotes whether the operation performed was successful or not.
</td></tr><tr><td>
message</td>
<td>
Message  is the access token.
</td></tr><tr><td>
status
</td><td>
It is the status code. It will be REQACSTKN  for this post message.
</td></tr></table>
<hr/>

#### Get Document Save Status


|Key|Value|
| :- | :- |
|MessageId|string (Get\_Document\_Save\_Status)|

Details:
<table class="custom_td"><tr><td>
MessageId
</td><td>
It denotes the type of post message. 
<br>
Here “Get_Document_Save_Status” refers to the post message which can be sent to the AOE Editor to know whether the document has been saved or not.
</td></tr></table>

**Reponse**: AOE Editor  sends a post message to the host with message id UC\_Message and status as “Doc\_Save\_Status”


|Key|Value|
| :- | :- |
|msgId|string (always UC\_Message)|
|args|Object<br><table><thead><tr><th>Key</th><th>Value</th></tr></thead><tbody><tr><td>success</td><td>boolean</td></tr><tr><td>status</td><td>string (Doc_Save_Status)</td></tr></tbody></table>|

Details:
<table class="custom_td"><tr><td>
msgId
</td><td>
It denotes the type of post message. 
<br>
Here “UC_Message” refers to the post message.
</td></tr><tr><td>
args 
</td><td>
It denotes the arguments of the message.
</td></tr><tr><td>
success
</td><td>
It denotes whether the document is saved or not. If a document is saved it will return true, else it will return false when the document is not saved.
</td></tr><tr><td>
status
</td><td>
It is the status code and it will be Doc_Save_Status only for this post message.
</td></tr></table>
<hr/>

#### Set Zoom Level


|Key|Value|
| :- | :- |
|MessageId|string (Set\_Zoom\_Level)|
|Value|object<br><table><thead><tr><th>Key</th><th>Value</th></tr></thead><tbody><tr><td>level</td><td>int</td></tr></tbody></table>|

Details:
<table class="custom_td"><tr><td>
MessageId</td><td>
It denotes the type of post message. 
<br>
Here “Set_Zoom_Level” refers to the post message which can be sent to the AOE Editor to set the zoom level
</td></tr><tr><td>
Value 
</td><td>
It denotes the value of the message
</td></tr></table>
Whenever there is Set\_Zoom\_Level as message id following arguments object keys should be passed with it.

<table class="custom_td"><tr><td>
level
</td><td>
Integer value from (1-18) to set the zoom level.
<br/>
1 minimum 20% & 18 maximum 400%
</td></tr></table>

|**Level**|**Zoom Percentage**|**Level**|**Zoom Percentage**|
| :- | :- | :- | :- |
|1|20%|10|100%|
|2|25%|11|120%|
|3|30%|12|150%|
|4|35%|13|170%|
|5|40%|14|200%|
|6|50%|15|235%|
|7|60%|16|280%|
|8|70%|17|335%|
|9|85%|18|400%|


<hr/>

#### Show Print Button 

|Key|Value|
| :- | :- |
|MessageId|string (Show\_Print\_Button)|
|Value|object<br><table><thead><tr><th>Key</th><th>Value</th></tr></thead><tbody><tr><td>Flag</td><td>boolean</td></tr></tbody></table>|

Details:
<table class="custom_td"><tr><td>
MessageId
</td><td>
It denotes the type of post message. 
<br>
Here Show_Print_Button refers to the post message which can be sent to the AOE Editor to show/hide the print button on notebookbar UI.
</td></tr><tr><td>
Value 
</td><td>
It denotes the value of the message
</td></tr></table>
Whenever there is Show\_Print\_Button as message id following arguments object keys should be passed with it.
<table class="cutom_td"> <tr><td>
Flag</td>
<td>
Flag true shows the print button whereas flag false hides the print button.
</td></tr></table>
**Reponse**: No response is received from the AOE Editor, it will just show/hide the print icon under File tab.


#### Toggle Theme
|Key|Value|
| :- | :- |
|MessageId|string (Toggle\_Theme)|
|Value|object<br><table><thead><tr><th>Key</th><th>Value</th></tr></thead><tbody><tr><td>theme</td><td>string</td></tr></tbody></table>|

Details:
<table class="custom_td"><tr><td>
MessageId
</td><td>
It denotes the type of post message. 
<br>
Here “Toogle Theme” refers to the post message which can be sent to AOE Editor to change theme from light and dark.
</td></tr><tr><td>
Value 
</td><td>
It denotes the value of the message
</td></tr></table>
Whenever there is Toggle\_Theme as message id following arguments object keys should be passed with it.
<table class="custom_td"><tr><td>
theme</td><td>
Two theme option is currently available i.e. "light" or "dark"
</td></tr></table>
**Reponse**: No response is received from the AOE Editor, it will just change the theme.