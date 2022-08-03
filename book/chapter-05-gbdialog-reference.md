# .gbdialog Reference
![generalbots-2018](https://user-images.githubusercontent.com/65977273/94922431-949c3900-0490-11eb-800a-6b478d689f2a.png)

General Bots BASIC using HEAR and TALK keywords provides a easy to write bot language accessible to everyone and used as incomer for people willing to make their own bot.

## Using Conversational BASIC

The following file types are loaded from a .gbdialog package: `.vbs`, `.vb`, `.basic` and `.bas`.

## General Bots BASIC reference

| Instruction / Usage                                           | Description                                                                 | Example |
| ------------------------------------------------------------- | --------------------------------------------------------------------------- |----|
| HEAR _variable_                                               | Hears something from the person into a _variable_ for later use.            | <pre>HEAR name <br/>TALK "Your name is " + name.<br/></pre>|
| confirm _variable_ (Comming soon)                             | Waits for confirmation like 'yes', 'y', 'yeah' and return true or false     |
| TALK _message_                                                | Talk the specified _message_ to the person.                                 | <pre>TALK "Hello world." </pre>| 
| GENERATE A PASSWORD                                           | Creates a new password into the system variable **password** for later use. |
| CREATE A BOT FARM USING _params_                              | Deploys a new bot farm to the cloud.                                        |
| WAIT _seconds_                                                | Wait a number of seconds before continuing the conversation.                |
| _variable_ = GET "_file_.xlsx", "_A1:A1_"                     | Gets the value of the cell specified in range address                       |
| SET "_file_.xlsx", "_A1:A1_", 42                              | Gets the value of the cell specified in range address                       |
| _variable_ = GET "https://server/query"                       | Gets the value of the cell specified in range address                       |
| POST "https://", _data_                                       | Gets the value of the cell specified in range address                       |
| wait _seconds_                                                | Wait a number of seconds before continuing the conversation.                |
| HEAR _variable_ AS EMAIL                                      | |
| HEAR _variable_ AS DATE                                       | |
| HEAR _variable_ AS NAME                                       | |
| HEAR _variable_ AS INTEGER                                    | eg.: HEAR approve as Boolean. |
| HEAR _variable_ AS BOOLEAN                                    | |
| HEAR _variable_ AS HOUR                                       | |
| HEAR _variable_ AS MONEY                                      | |
| HEAR _variable_ AS MOBILE                                     | |
| * HEAR _variable_ AS FILE                                       | Returns a file uploaded by user to be saved with SAVE _variable_ AS "folder/folder/file" on .gbdrive. |
| HEAR _variable_ AS AUDIO                                      | Returns a audio uploaded by user to be saved with SAVE. |
| HEAR _variable_ AS ZIPCODE                                    | |
| HEAR _variable_ AS "Abacate", "Maçã", "Morango"               | Displays the specified menu and waits for this input until user select one of them. | 
| HEAR _variable_ AS LANGUAGE                                   | |
| HEAR _variable_ AS LOGIN (internal)                           | Waits for Active Directoy login integration before proceeding with the dialog .     |
| GO TO [number,] dialogName                                    | Transfers the conversation to a next dialog for the specificed number or as last command, transfers the context to this dialog.              |
| SEE CAPTION OF _url_ AS _variable_                      | Extracts an caption, using a pre-trained neural network, from a image. | 
| SEE TEXT OF _url_ AS _variable_                      | Extracts text from the image in a OCR (Optical Character Recognition) feature. | 
| * data = SELECT a, SUM(b) AS b FROM data GROUP BY a    | Use SQL to manipulate a data variable returned from FIND or an array | _variable_ = CHART "pie", data| Generates a chart from data. |
| * file = data AS IMAGE| Converts a two dimension array into an image file, ready to be used with SAVE AS or SEND FILE.|
| * file = data AS PDF| Converts a two dimension array into an PDF file, ready to be used with SAVE AS or SEND FILE.|
| * page = GET PAGE _url_ | Web automation retrival of a web page.|
| * _variable_ = GET page, cssSelector, "body > img" | Retrives an element within an IFRAME specified by selector eg.: "[name=iFrameName]", to be used later. | 
| * SET page, cssSelector, value  | Define an field to value eg. "value 123" on the webpage specified by selector eg. "#id". | 
| * CLICK page, cssSelector | Clicks on an element inside the web page being automated by General Bots. | 
| * file = DOWNLOAD _url_ |  |
|NEW OBJECT| Creates a new object to be used with REST calls for example. <br>```data = NEW OBJECT``` <br> ```data.color = "blue"``` |
|NEW ARRAY| Creates a new array. <br>```data = NEW ARRAY``` <br> ```data[0] = "blue"``` |

* = Work in progress.

### Options

| Instruction / Usage                                           | Description                                                                 |
| ------------------------------------------------------------- | --------------------------------------------------------------------------- |
| SET HTTP HEADER _key =  _value_                         | Defines an HTTP header to be used to next GET call. |
| SET HTTP USERNAME = _value_                             | Defines the HTTP username to be used to next GET call. |
| SET HTTP PASSWORD = _value_                             | Defines the HTTP password to be used to next GET call. |
| * SET HEAR ON "mobile"| | 
| SET MAX LINES _value_ | | 
| SET SCHEDULE "2 * * * * *" | | 
| SET LANGUAGE _value_ | | 
| SET TRANSLATOR [ON or OFF]| | 
| SET WHOLE WORD [TRUE or FALSE]| | 
| SET THEME "dark" or "white" or "blue" | Defines the theme to the next content generation (PDF, images, vídeos, etc.)|
| SET OPERATOR [OR] | Defines OR operations on multiple FIND filters separated by comma, eg.: FIND "A1=2", "A3=4" | 

* = Work in progress.

## How To

### Use General Bots computer vision

1. Develop a BASIC dialog and publish;

![image](https://user-images.githubusercontent.com/14840374/146782500-26f0dc27-e722-41aa-b79e-619d6403fa0d.png)

2. Test it in the conversation

![image](https://user-images.githubusercontent.com/14840374/146782691-7c28998b-7485-4d34-af33-da87d1b26088.png)

### Using General Bots Web Automation

```
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

```
SET MAX LINES 1000 
data = FIND "data.xlsx",  
data = SELECT a, SUM(b) AS b FROM data GROUP BY a 
SET THEME dark 
png = data as IMAGE  
SEND FILE png 
```

On the fly charts

```
data = [10, 20, 30] 
legends= "Steve;Yui;Carlos"   
img = CHART "pie", data, legends  
SEND FILE img  
SAVE img as "folder/filename.jpg" 
```

### Using complete General Bots Conversational Data Analytics

```
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
