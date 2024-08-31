---
sidebar_position: 50
---

# .gbdialog Reference

![generalbots-2018](https://user-images.githubusercontent.com/65977273/94922431-949c3900-0490-11eb-800a-6b478d689f2a.png)

General Bots BASIC using HEAR and TALK keywords provides a easy to write bot language accessible to everyone and used as incomer for people willing to make their own bot.

It is like creating a conversation Node.js application just using BASIC. All code will run isolated on a Node VM:

![image](https://user-images.githubusercontent.com/14840374/200206510-9f5bd788-e710-4932-9ed8-a09599656cea.png)


## Using Conversational BASIC

The following file types are loaded from a .gbdialog package: `.vbs`, `.vb`, `.basic` and `.bas`.

## General Bots BASIC reference

To organize the instructions functionally, I'll group them into five categories: **Basic Interaction**, **Data Handling**, **Web Automation**, **File Management**, and **Advanced Operations**. Each group will include relevant instructions with examples.

```markdown
## Basic Interaction

| Instruction / Usage                                           | Description                                                                 | Example |
| ------------------------------------------------------------- | --------------------------------------------------------------------------- | ------- |
| HEAR _variable_                                               | Hears something from the person into a _variable_ for later use.            | <pre>HEAR name <br/>TALK "Your name is " + name.<br/></pre> |
| TALK _message_                                                | Talk the specified _message_ to the person.                                 | <pre>TALK "Hello world."</pre> |
| WAIT _seconds_                                                | Wait a number of seconds before continuing the conversation.                | <pre>WAIT 10 <br/> TALK "Waited for 10 seconds."</pre> |
| confirm _variable_ (Comming soon)                             | Waits for confirmation like 'yes', 'y', 'yeah' and returns true or false     | <pre>HEAR confirm <br/>TALK "Please confirm if you want to proceed." <br/> if confirm THEN TALK "Confirmed." ELSE TALK "Not confirmed."</pre> |
| HEAR _variable_ AS EMAIL                                      | Hears and validates an email address from the user.                         | <pre>HEAR email AS EMAIL <br/> TALK "Email received: " + email.</pre> |
| HEAR _variable_ AS DATE                                       | Hears and validates a date from the user.                                   | <pre>HEAR date AS DATE <br/> TALK "Date received: " + date.</pre> |
| HEAR _variable_ AS NAME                                       | Hears and validates a name from the user.                                   | <pre>HEAR name AS NAME <br/> TALK "Name received: " + name.</pre> |
| HEAR _variable_ AS INTEGER                                    | Hears and validates an integer from the user.                               | <pre>HEAR age AS INTEGER <br/> TALK "Age received: " + age.</pre> |
| HEAR _variable_ AS BOOLEAN                                    | Hears and validates a boolean (true/false) from the user.                   | <pre>HEAR agree AS BOOLEAN <br/> TALK "Agreement status: " + agree.</pre> |
| HEAR _variable_ AS HOUR                                       | Hears and validates an hour from the user.                                  | <pre>HEAR hour AS HOUR <br/> TALK "Hour received: " + hour.</pre> |
| HEAR _variable_ AS MONEY                                      | Hears and validates a monetary amount from the user.                        | <pre>HEAR amount AS MONEY <br/> TALK "Amount received: " + amount.</pre> |
| HEAR _variable_ AS MOBILE                                     | Hears and validates a mobile number from the user.                          | <pre>HEAR mobile AS MOBILE <br/> TALK "Mobile number received: " + mobile.</pre> |
| HEAR _variable_ AS ZIPCODE                                    | Hears and validates a ZIP code from the user.                               | <pre>HEAR zipcode AS ZIPCODE <br/> TALK "ZIP Code received: " + zipcode.</pre> |
| HEAR _variable_ AS "Abacate", "Maçã", "Morango"               | Displays the specified menu and waits for user selection.                    | <pre>HEAR fruit AS "Abacate", "Maçã", "Morango" <br/> TALK "You selected: " + fruit.</pre> |
| HEAR _variable_ AS LANGUAGE                                   | Hears and validates a language code from the user.                          | <pre>HEAR language AS LANGUAGE <br/> TALK "Language selected: " + language.</pre> |
| HEAR _variable_ AS LOGIN (internal)                           | Waits for Active Directory login integration before proceeding.            | <pre>HEAR user AS LOGIN <br/> TALK "User logged in: " + user.</pre> |

## Data Handling

| Instruction / Usage                                           | Description                                                                 | Example |
| ------------------------------------------------------------- | --------------------------------------------------------------------------- | ------- |
| _variable_ = GET "_file_.xlsx", "_A1:A1_"                     | Gets the value of the cell specified in range address                       | <pre>name = GET "data.xlsx", "A1:A1" <br/> TALK "The value is " + name.</pre> |
| SET "_file_.xlsx", "_A1:A1_", 42                              | Sets the value of the cell specified in range address                       | <pre>SET "data.xlsx", "A1:A1", 42 <br/> TALK "Value set in Excel."</pre> |
| _variable_ = GET "https://server/query"                       | Gets the value from the specified web service                                | <pre>result = GET "https://api.example.com/data" <br/> TALK "Data received: " + result.</pre> |
| POST "https://", _data_                                       | Sends data to the specified URL                                              | <pre>POST "https://api.example.com/submit", "data" <br/> TALK "Data posted successfully."</pre> |
| data = SELECT a, SUM(b) AS b FROM data GROUP BY a             | Use SQL to manipulate a data variable returned from FIND or an array        | <pre>data = FIND "sales_data.xlsx", "A1:B10" <br/> result = SELECT product, SUM(amount) AS total FROM data GROUP BY product <br/> TALK "Query result: " + result.</pre> |
| file = data AS IMAGE                                          | Converts a two-dimensional array into an image file.                        | <pre>file = data AS IMAGE <br/> SAVE file AS "sales_chart.png" <br/> TALK "Chart saved as image."</pre> |
| file = data AS PDF                                            | Converts a two-dimensional array into a PDF file.                           | <pre>file = data AS PDF <br/> SAVE file AS "sales_report.pdf" <br/> TALK "Report saved as PDF."</pre> |
| NEW OBJECT                                                    | Creates a new object to be used with REST calls.                            | <pre>data = NEW OBJECT <br/> data.color = "blue" <br/> TALK "New object created."</pre> |
| NEW ARRAY                                                     | Creates a new array.                                                        | <pre>data = NEW ARRAY <br/> data[0] = "red" <br/> TALK "New array created."</pre> |
| QRCODE                                                         | Creates a QR code from specified text.                                     | <pre>file = QRCODE "https://example.com" <br/> SAVE file AS "qrcode.png" <br/> TALK "QR Code generated."</pre> |
| FORMAT value, format                                          | Formats a value according to the specified format.                          | <pre>d = FORMAT today, "YYYY-MM-dd" <br/> TALK "Formatted date: " + d.</pre> |
| ADD NOTE                                                      | Adds a note to a file named Notes.xls of .gbdata.                           | <pre>ADD NOTE "This is a new note." <br/> TALK "Note added."</pre> |
| ALLOW ROLE                                                    | Check if role specified in People sheet (.gbdata) will have access.        | <pre>ALLOW ROLE "Admin" <br/> TALK "Role access granted."</pre> |

## Web Automation

| Instruction / Usage                                           | Description                                                                 | Example |
| ------------------------------------------------------------- | --------------------------------------------------------------------------- | ------- |
| page = OPEN _url_ [AS #namedSession]                          | Web automation retrieval of a web page, saving the session for reuse.      | <pre>page = OPEN "https://example.com" AS #session1 <br/> TALK "Page opened and session saved."</pre> |
| * _variable_ = GET page, cssSelector, "body > img"             | Retrieves an element within an IFRAME specified by selector.                | <pre>image = GET page, "#profile-picture" <br/> TALK "Profile picture retrieved."</pre> |
| * SET page, cssSelector, value                                | Defines a field to a value on the webpage specified by selector.            | <pre>SET page, "#username", "user123" <br/> TALK "Username set."</pre> |
| * CLICK page, cssSelector                                     | Clicks on an element inside the web page being automated.                   | <pre>CLICK page, "#submit-button" <br/> TALK "Submit button clicked."</pre> |
| * file = DOWNLOAD _url_                                       | Downloads a file from the specified URL.                                   | <pre>file = DOWNLOAD "https://example.com/file.zip" <br/> SAVE file AS "downloads/file.zip" <br/> TALK "File downloaded."</pre> |

## File Management

| Instruction / Usage                                           | Description                                                                 | Example |
| ------------------------------------------------------------- | --------------------------------------------------------------------------- | ------- |
| HEAR _variable_ AS FILE                                       | Returns a file uploaded by the user to be saved.                            | <pre>HEAR file AS FILE <br/> SAVE file AS "uploads/myfile.pdf" <br/> TALK "File uploaded and saved."</pre> |
| HEAR _variable_ AS AUDIO                                      | Returns an audio file uploaded by the user to be saved.                     | <pre>HEAR audio AS AUDIO <br/> SAVE audio AS "recordings/audiofile.mp3" <br/> TALK "Audio received and saved."</pre> |
| INCLUDE file                                                  | Includes a file into .gbdialog.                                             | <pre>INCLUDE "script.gbdialog" <br/> TALK "File included."</pre> |
| UPLOAD file                                                    | Uploads a file to a storage blob, like Azure Storage.                      | <pre>UPLOAD "

path/to/file.pdf" <br/> TALK "File uploaded to cloud storage."</pre> |
| DIR path                                                      | Returns a list of files in the specified directory.                        | <pre>files = DIR "uploads/" <br/> TALK "Files in directory: " + files.</pre> |
| FILL                                                           | Fills data into a Word document to be exported as images.                  | <pre>FILL "template.docx", data <br/> TALK "Document filled and exported."</pre> |
| SAVE _variable_ AS "path/file"                                 | Saves the specified variable as a file at the given path.                   | <pre>SAVE file AS "path/to/save/file.pdf" <br/> TALK "File saved."</pre> |

## Advanced Operations

| Instruction / Usage                                           | Description                                                                 | Example |
| ------------------------------------------------------------- | --------------------------------------------------------------------------- | ------- |
| TABLE name ON connection                                     | Defines a TABLE on the specified storage (database) connection.            | <pre>TABLE "Sales" ON "DBConnection" <br/> TALK "Table defined."</pre> |
| field AS dataType                                             | Defines a field in TABLE. Eg.: name string(50).                             | <pre>field = "price" AS number(10,2) <br/> TALK "Field defined as number."</pre> |
| CONTINUATION TOKEN                                            | Returns the value of the continuation token associated with the current dialog. | <pre>token = CONTINUATION TOKEN <br/> TALK "Continuation token: " + token.</pre> |
| NEW OBJECT                                                    | Creates a new object to be used with REST calls.                            | <pre>data = NEW OBJECT <br/> data.color = "blue" <br/> TALK "New object created."</pre> |
| NEW ARRAY                                                     | Creates a new array.                                                        | <pre>data = NEW ARRAY <br/> data[0] = "red" <br/> TALK "New array created."</pre> |
```


### Internal Variables and Functions.

These are variables that can be used in General Bots BASIC to faster dialog and services faster.
All values from .gbot Config.xlsx are also provided as variables, so it can be acessed directly in dialog.

| Instruction / Usage                                           | Description                                                                  |
| ------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| aadToken() | Auto generated variable that contains Azure AD Token useful for calling Microsoft Web Services.           |




### Options

| Instruction / Usage                                           | Description                                                                  |
| ------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| SET PARAM name AS value                        | Defines a retrievable param in the storage in the scope of the user                         |
| GET PARAM name                                 | Returns a previously user scoped param via SET PARAM from the storage.                      |
| SET HTTP HEADER _key =  _value_                | Defines an HTTP header to be used to next GET call.                                         |
| SET HTTP USERNAME = _value_                    | Defines the HTTP username to be used to next GET call.                                      |
| SET HTTP PASSWORD = _value_                    | Defines the HTTP password to be used to next GET call.                                      |
| * SET HEAR ON "mobile"                         |                                                                                             | 
| SET MAX LINES _value_                          |                                                                                             | 
| SET SCHEDULE "2 * * * * *"                     |                                                                                             | 
| SET LANGUAGE _value_                           |                                                                                             | 
| SET TRANSLATOR [ON or OFF]                     |                                                                                             | 
| SET WHOLE WORD [TRUE or FALSE]                 |                                                                                             | 
| SET THEME "dark" or "white" or "blue"          | Defines the theme to the next content generation (PDF, images, vídeos, etc.)                |
| SET OPERATOR [OR]                              | Defines OR operations on multiple FIND filters separated by comma, eg.: FIND "A1=2", "A3=4" | 
| SET FILTER TYPE [comma separated list of types]| Uses the specified type in next FIND calls, disabling auto detection of filter type, eg.: SET FILTER TYPE date, string | 
| SET PAGED "auto" or "none" | Defines auto pagging for HTTP REST GET calls. | 


* = Work in progress.

## How To

### Use code in Excel 

To reply as code in Excel, start the cell value with /basic followed by the code itself. Eg.:

```
/basic
TALK "Hello."
```


### Use General Bots computer vision

1. Develop a BASIC dialog and publish;

![image](https://user-images.githubusercontent.com/14840374/146782500-26f0dc27-e722-41aa-b79e-619d6403fa0d.png)

2. Test it in the conversation

![image](https://user-images.githubusercontent.com/14840374/146782691-7c28998b-7485-4d34-af33-da87d1b26088.png)

### Using General Bots Web Automation to ask humans about unreadable captchas

```BASIC
mobile = "5521000000000" 

page = GET HTML "https://www.any-website.com/" 
SET page, "#usuario", "user"  
SET page, "#j_password", "xxxxxxxxxxx"   

 
img = GET page, "[name=iCaptcha]", "body > img" 
SEND FILE TO mobile, img 
TALK TO mobile, "Digite o código da imagem para prosseguir:" 
SET HEAR ON mobile 
HEAR captcha  
SET page, "#captcha", captcha 

CLICK page, "#bt-login" 
TALK TO mobile, "Login done, thanks." 
```
### Using General Bots SQL and dynamic image and chart generation

On the fly table as images.

```BASIC
SET MAX LINES 1000 
data = FIND "data.xlsx",  
data = SELECT a, SUM(b) AS b FROM data GROUP BY a 
SET THEME dark 
png = data as IMAGE  
SEND FILE png 
```

On the fly charts

```BASIC
data = [10, 20, 30] 
legends= "Steve;Yui;Carlos"   
img = CHART "pie", data, legends  
SEND FILE img  
SAVE img as "folder/filename.jpg" 
```

### Using General Bots Web Automation to custom notify about Google Calendar

```basic

REM Perform G. Login. 
OPEN "https://accounts.google.com/ServiceLogin" 
SET "#identifierId", "test@gmail.com" 
PRESS ENTER 
WAIT 3 
SET "input[type='password']", "******" 
PRESS ENTER 
WAIT 5 

REM Enter on the Calendar page and capture the calendar grid inside the page. 
OPEN "https://calendar.google.com/calendar/u/0/r?tab=mc&pli=1" 
file = SCREENSHOT "div.K2fuAf" 

REM Notify all team members with the updated calendar image. 
list = FIND "People.xlsx", "Calendar=Y"  
index = 1  
DO WHILE index < ubound(list)  
  row = list[index]  
  TALK TO row.Mobile, "Hello " + row.Name + ", here is your calendar:"  
  SEND FILE TO row.Mobile, file, "Calendar"  
  index = index + 1  
LOOP 
 
```

### Using complete General Bots Conversational Data Analytics

```BASIC
TALK  "General Bots Labs presents FISCAL DATA SHOW BY BASIC" 

TALK "Gift Contributions to Reduce the Public Debt API (https://fiscaldata.treasury.gov/datasets/gift-contributions-reduce-debt-held-by-public/gift-contributions-to-reduce-the-public-debt)" 
 
result = GET "https://api.fiscaldata.treasury.gov/services/api/fiscal_service/v2/accounting/od/gift_contributions?page[size]=500" 
data = result.data 
data = SELECT YEAR(record_date) as Yr, SUM(CAST(contribution_amt AS NUMBER)) AS Amount FROM data GROUP BY YEAR(record_date) 

TALK "Demonstration of Gift Contributions with AS IMAGE keyword" 
SET THEME dark 
png = data as IMAGE  
SEND FILE png 

DELAY 5 
TALK " Demonstration of Gift Contributions CHART keyword" 
 img = CHART "bar", data  
SEND FILE img 
```

![image](https://user-images.githubusercontent.com/14840374/178154826-8188029e-b4f4-48aa-bc0d-126307ce5121.png)


### Using General Bots Office templates

```
data = FIND "Customer.xlsx", "Idade=25" 
doc = TEMPLATE "template.docx" WITH data 
SAVE doc AS "resume.docx" 
SEND EMAIL "noreply@pragmatismo.io", "Subject", doc 
```

### Automating GitHub Issue creation with General Bots Automation

```BASIC

REM Realiza login no GitHub. 
page = GET HTML "https://github.com/login" 
SET page, "#login_field", "username" 
SET page, "#password", "*******" 
PRESS ENTER ON page 

REM Verifica 2FA. 

SET HEAR ON "5521999999999" 
TALK "Digite o código de dupla autenticação enviado..." 
HEAR code 
SET page, "#otp", code 
PRESS ENTER ON page	 

REM Extrai cada Issue da planilha e cria no GitHub. 

list = FIND "issues.xlsx" 
index = 1   
DO WHILE index <38 
 row = list[index]   
 page = GET HTML "https://github.com/GeneralBots/BotServer/issues/new" 
 SET page, "#issue_title", row.title 
 SET page, "#issue_body", row.body 
 CLICK page, "#new_issue > div > div > div.Layout-main > div > div.timeline-comment.color-bg-default.hx_comment-box--tip > div > div.flex-items-center.flex-justify-end.d-none.d-md-flex.mx-2.mb-2.px-0 > button" 
 TALK "Issue '" + row.title + "' criado." 
 WAIT 5 
 index = index + 1   
LOOP 
EXIT 
```



### Using POST data

You can use POST passing a variable as the second param in the POST call. The example
bellow shows how to call POST using an object that is returned from the Excel file.

Given the Excel file with the following contents and saved to the standard .gbdialog folder:

| tokenId | token            | comment |
| ------- | ---------------- | ------- |
| 29187   | AAMkAGEzMWIxMmI5 | Prod1   |
| 98739   | jZWYtNGQ3My1iNmM | Prod2   |

The Word bellow will invoke POST call by using line contents as object attributes:

``` BASIC
obj = FIND "dados.xlsx", "tokenId=29187"
POST "https://server/query", obj
' obj here is {tokenId: 29187, token: "AAMkAGEzMWIxMmI5", comment: "Prod1"}
```

* OAuth2 is being implemented and no modification to previous calls will be necessary
as this configuration will be an administrative conversation to get the token setup.

### Generate a password for the person

```vb


talk "Let's generate a very dificult to guess password for the new bot:"
generate a password
talk "Your password is *" + password + "*. Keep it on a safe place only acessible to you."


```

### Get the list of cloud subscriptions

```vb

hear one of subscriptions with email, password into subscriptionId
talk "The subscription selected was: " + subscriptionId
```


# General Bots Simple and Complex Programs

These are sample programs in General Bots BASIC, each presented with a modern and engaging approach. The first 20 examples are simple, while the next 20 delve into more advanced concepts. Check the list
of [templates](https://github.com/GeneralBots/BotServer/tree/main/templates)

The set of 20 advanced General Bots BASIC programs that integrate web services, web automation, file handling, and dynamic interactions. These samples are designed to showcase the full potential of General Bots BASIC for advanced users. These advanced samples illustrate a range of functionalities that can be implemented with General Bots BASIC, from data manipulation and web automation to dynamic content generation and complex file handling.


## 1. **Retrieve and Save Web Data to Excel**
```basic
GET "https://api.example.com/data"
data = result.data
SAVE "data.xlsx", "A1:A" + UBOUND(data), data
TALK "Data retrieved and saved to data.xlsx successfully!"
```

## 2. **Automated Web Form Submission**
```basic
OPEN "https://example.com/form"
SET page, "#name", "John Doe"
SET page, "#email", "john.doe@example.com"
SET page, "#message", "This is a test message."
CLICK page, "#submit"
TALK "Form submitted successfully!"
```

## 3. **Generate and Save Dynamic Report as PDF**
```basic
data = FIND "report_data.xlsx", "A1:C10"
pdf = data AS PDF
SAVE pdf AS "report.pdf"
TALK "Dynamic report generated and saved as report.pdf!"
```

## 4. **Create and Upload Image from Data**
```basic
data = [10, 20, 30, 40]
labels = "Q1;Q2;Q3;Q4"
img = CHART "bar", data, labels
UPLOAD img
TALK "Chart image generated and uploaded!"
```

## 5. **Automate GitHub Issue Creation from Spreadsheet**
```basic
list = FIND "issues.xlsx"
index = 1
DO WHILE index <= UBOUND(list)
    row = list[index]
    page = GET HTML "https://github.com/GeneralBots/BotServer/issues/new"
    SET page, "#issue_title", row.title
    SET page, "#issue_body", row.body
    CLICK page, "#new_issue > div > div > div.Layout-main > div > div.timeline-comment.color-bg-default.hx_comment-box--tip > div > div.flex-items-center.flex-justify-end.d-none.d-md-flex.mx-2.mb-2.px-0 > button"
    TALK "Issue '" + row.title + "' created."
    WAIT 5
    index = index + 1
LOOP
```

## 6. **Extract and Save Web Page Content**
```basic
OPEN "https://example.com/page"
content = GET page, "body"
SAVE "page_content.txt", content
TALK "Page content saved as page_content.txt!"
```

## 7. **Interactive Poll Results Analysis**
```basic
HEAR poll_data AS FILE
data = LOAD poll_data
analysis = SELECT question, COUNT(*) AS responses FROM data GROUP BY question
SAVE "poll_analysis.xlsx", "A1:C" + UBOUND(analysis), analysis
TALK "Poll results analyzed and saved to poll_analysis.xlsx!"
```

## 8. **Send User-Specific Notifications**
```basic
list = FIND "users.xlsx", "Notify=Y"
index = 1
DO WHILE index <= UBOUND(list)
    row = list[index]
    SEND MAIL row.email, "Notification", "Hello " + row.name + ", you have a new notification!"
    index = index + 1
LOOP
TALK "Notifications sent to all users."
```

## 9. **Automate Data Entry into Web Application**
```basic
OPEN "https://example.com/data-entry"
SET page, "#field1", "Value1"
SET page, "#field2", "Value2"
SET page, "#field3", "Value3"
CLICK page, "#submit"
TALK "Data entry completed successfully!"
```

## 10. **Generate and Save QR Codes for Multiple URLs**
```basic
urls = ["https://example1.com", "https://example2.com", "https://example3.com"]
index = 1
DO WHILE index <= UBOUND(urls)
    file = QRCODE urls[index]
    SAVE file AS "qrcode_" + index + ".png"
    index = index + 1
LOOP
TALK "QR codes generated and saved!"
```

## 11. **Automate Google Calendar Event Creation**
```basic
OPEN "https://calendar.google.com/calendar/u/0/r?tab=mc&pli=1"
HEAR event_date AS DATE
HEAR event_details AS STRING
SET "#title", "New Event"
SET "#details", event_details
SET "#date", event_date
CLICK "#save"
TALK "Event created on Google Calendar for " + event_date
```

## 12. **Send Customized Reports to a List of Recipients**
```basic
data = FIND "reports.xlsx"
index = 1
DO WHILE index <= UBOUND(data)
    row = data[index]
    report = TEMPLATE "report_template.docx" WITH row
    SEND MAIL row.email, "Your Report", report
    index = index + 1
LOOP
TALK "Reports sent to all recipients."
```

## 13. **Create and Save Dynamic Chart with User Input**
```basic
HEAR user_data AS "10,20,30,40"
data = SPLIT(user_data, ",")
img = CHART "line", data
SAVE img AS "dynamic_chart.png"
TALK "Dynamic chart created and saved as dynamic_chart.png!"
```

## 14. **Extract and Save Image Metadata**
```basic
SEE TEXT OF "https://example.com/image.jpg" AS metadata
SAVE "image_metadata.txt", metadata
TALK "Image metadata extracted and saved as image_metadata.txt!"
```

## 15. **Automate Form Filling Based on Data from Excel**
```basic
data = FIND "form_data.xlsx", "A1:C1"
OPEN "https://example.com/form"
SET page, "#name", data[0].name
SET page, "#email", data[0].email
SET page, "#message", data[0].message
CLICK page, "#submit"
TALK "Form filled and submitted based on Excel data!"
```

## 16. **Generate PDF from Dynamic SQL Query Results**
```basic
data = FIND "database.xlsx", "A1:C100"
query = SELECT name, age, city FROM data WHERE age > 30
pdf = query AS PDF
SAVE pdf AS "filtered_data_report.pdf"
TALK "PDF report generated and saved!"
```

## 17. **Capture and Save Web Page Screenshot with Timestamp**
```basic
timestamp = FORMAT NOW(), "YYYY-MM-DD_HH-MM-SS"
OPEN "https://example.com"
file = SCREENSHOT "body"
SAVE file AS "screenshot_" + timestamp + ".png"
TALK "Screenshot captured and saved with timestamp!"
```

## 18. **Handle and Save User-Uploaded Files**
```basic
HEAR user_file AS FILE
SAVE user_file AS "uploads/user_file_" + FORMAT NOW(), "YYYY-MM-DD_HH-MM-SS" + ".pdf"
TALK "File uploaded and saved successfully!"
```

## 19. **Extract Data from Web Page and Save to Excel**
```basic
OPEN "https://example.com/data-page"
data = GET page, "#data-table"
SAVE "web_data.xlsx", "A1:A" + UBOUND(data), data
TALK "Data extracted from web page and saved to web_data.xlsx!"
```

## 20. **Perform Complex Data Analysis and Save Results**
```basic
data = FIND "complex_data.xlsx", "A1:D100"
analysis = SELECT category, SUM(amount) AS total FROM data GROUP BY category
SAVE "data_analysis.xlsx", "A1:B" + UBOUND(analysis), analysis
TALK "Data analysis completed and saved to data_analysis.xlsx!"
```


And even more simple examples can be seen in this list as begginers use BASIC 
to understand code:

## 1. Welcome Message
```basic
HEAR name AS NAME
TALK "Hey " + name + ", welcome to our awesome service! 🎉"
```

## 2. Simple Password Generator
```basic
GENERATE A PASSWORD
TALK "Your new password is: " + password
```

## 3. Remind User to Take a Break
```basic
WAIT 3600
TALK "You've been working for an hour! Remember to take a break and stretch! 💪"
```

## 4. Get User's Favorite Fruit
```basic
HEAR fruit AS "Apple", "Banana", "Cherry"
TALK "Nice choice! " + fruit + " is a great fruit! 🍓"
```

## 5. Send a Calendar Invite
```basic
HEAR email AS EMAIL
HEAR date AS DATE
TALK "Sending a calendar invite for " + date + " to " + email
SEND MAIL email, "Calendar Invite", "You are invited to an event on " + date
```

## 6. Generate and Send QR Code
```basic
HEAR url AS "https://example.com"
file = QRCODE url
SEND FILE file
TALK "Here is your QR code for the URL: " + url
```

## 7. Weather Update
```basic
GET "https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=YOUR_LOCATION"
data = result.current
TALK "The current temperature is " + data.temp_c + "°C with " + data.condition.text
```

## 8. Todo List Reminder
```basic
HEAR task AS STRING
TALK "Got it! I'll remind you about: " + task
```

## 9. Send Motivational Quote
```basic
quotes = ["Keep going!", "You got this!", "Believe in yourself!"]
index = RANDOM(0, 2)
TALK quotes[index]
```

## 10. Capture and Send Screenshot
```basic
OPEN "https://example.com"
file = SCREENSHOT "body"
SEND FILE file
TALK "Here's a screenshot of the page."
```

## 11. Daily Affirmation
```basic
HEAR user AS NAME
TALK "Good morning " + user + "! Remember, today is going to be amazing! 🌟"
```

## 12. Send a Joke
```basic
jokes = ["Why don’t scientists trust atoms? Because they make up everything!", "Why did the scarecrow win an award? Because he was outstanding in his field!"]
index = RANDOM(0, 1)
TALK jokes[index]
```

## 13. User Poll
```basic
HEAR choice AS "Option 1", "Option 2", "Option 3"
TALK "You selected " + choice + ". Thanks for your input! 🗳️"
```

## 14. Image Caption Extraction
```basic
SEE CAPTION OF "https://example.com/image.jpg" AS caption
TALK "The caption of the image is: " + caption
```

## 15. Send Reminder Email
```basic
HEAR email AS EMAIL
HEAR reminder AS STRING
SEND MAIL email, "Reminder", "Just a friendly reminder: " + reminder
```

## 16. Capture Text from Image
```basic
SEE TEXT OF "https://example.com/image-with-text.jpg" AS text
TALK "The text from the image is: " + text
```

## 17. Add a Note
```basic
HEAR note AS STRING
ADD NOTE note
TALK "Note added: " + note
```

## 18. Generate Dynamic Chart
```basic
data = [5, 15, 25]
labels = "Red;Green;Blue"
img = CHART "bar", data, labels
SEND FILE img
TALK "Here’s your dynamic chart!"
```

## 19. Create and Send PDF Report
```basic
data = FIND "data.xlsx", "A1:B10"
pdf = data AS PDF
SEND FILE pdf
TALK "Here's your report in PDF format."
```

## 20. Interactive Game
```basic
TALK "Guess a number between 1 and 10."
HEAR guess AS INTEGER
IF guess == 7
    TALK "Congratulations! You guessed the right number! 🎉"
ELSE
    TALK "Oops! Try again next time!"
```
These examples demonstrate various capabilities of the language, from simple text manipulation to more complex tasks like image processing.
