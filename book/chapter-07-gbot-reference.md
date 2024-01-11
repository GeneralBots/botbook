# General Bots Administration

## Instance custom params

## Commands

General Bot can be controlled by the same chat window people talk to, so
here is a list of admin commands related to deploying .gb* files.

| Command         | Description                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------|
| /edit           | Sends a link to the Bot Storage so package folders like .gbdialog, .gbkb, .gbot and others can be edited.       |
| /setupSecurity [tokenName]   | Setup connection between General Bots and the Cloud, so the bot drive can be accessed by BotServer during publishing and direct access like the FIND keyword. Or using tokenName, setups a connection defined in Config.xlsx.|
| /publish [extension]  | Deploy the package to the bot storage. When ommited, the command will publish the package named <botId>.gbkb by default. |

# Config.xlsx (.gbot) Configuration
  
| Name                        | Description|
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Admin Notify E-mail         | E-mail used to notify administrators. |
| Avatar Logo                 | Bot logo URL.                                                                                      |
| Can Publish                 | Comma separeted list of mobile numbers that can publish directly. |
| Description                 | Description of the Bot.                                                                            |
| Enable Audio Hearing        | TRUE if the Bot can hear.                                                                          |
| Enable Audio Talking        | TRUE if the Bot can talk.                                                                          |
| Enable Spelling Checker     | TRUE if everything input by user should be spell checked.                                          |
| Enable Worldwide Translator | TRUE if the Bot should be polyglot.                                                                |
| Default User Language       | Language (eg.: en or pt) that user will be presented by the Bot.                                   |
| Default Content Language    | Language (eg.: en or pt) that content files in .gbkb, .gbdialog and so on are written.             |
| Language Detector           | TRUE if Bot should get the language automatically.                                                 |
| NLP Score                   | Number between 0 and 1 that will be used to classify text to use NLP neural network. |
| Search Score                | Number between 0 and 1 that will be used to consider Full Text Search as content retrieval method. |
| Transfer To                 | Comma separeted list of mobile numbers that Bot will use to tranfer chats from WhatsApp.           |
| WhatsApp Admins             | Comma separeted list of mobile numbers that will be admin. |
| Feedback Improve.Message    | Message to user when the Bot was unable to find something. |
| Keep Text                   | Comma separeted list of words that should be keep intact between Bot understanding process.                                                                                                                                                  |
| Start Dialog                | Name of .docx (without the Extension) that will be used as Dialog entry point.                                                                                                                                             |
| HelloGoodX                  | TRUE if Bot should give hello. |
| XRM Key                     | String key of HubSpot (currently) API. |
| WhatsApp Group Name         | WhatsApp group name that this Bot belongs to. | 
| WhatsApp Group Shortcuts |   Space separeted list of triggers in text that will active Bot in groups.|
| Bot Admin Number |   Administration mobile number which will receive Debug screenshots and other notifications.|  
| WhatsApp Group ID |   Group ID (accessible only in internal log) used to connect the Bot to a WhatsApp group.|
| Debug Web Automation |   TRUE if Bot Admin Number will receive an screenshot to each web automation step.|
| .gbapp List |   List of associated .gbapp packages to this .gbot. |
| Group Spell |  Enable spell checker for groups. |
| Synchronize Database | TRUE if TABLE keyword should *MODIFY* database. Be careful in Production storage this value should be FALSE (default). |

Note that this variables are available in every .gbdialog code, automatically.
  
## Enviroment Variables Reference

| Name                   | Sample Value                                     | Description |
|------------------------|--------------------------------------------------|-------------|
| ADDITIONAL_DEPLOY_PATH | D:\data\gbai                                     | Deploy folder to look for packages (Just one folder). 
| ADMIN_PASS             | E732+!#xJ3a_*!                                   | Administration password for the conversational interface.
| CLOUD_SUBSCRIPTIONID   | 622e5037-f7f1-49f6-a9c4-28babbb0fs               | Cloud subscription ID used to deploy new bots.
| CLOUD_LOCATION         | westus                                           | Cloud location used to deploy new bots.
| CLOUD_GROUP            | newassistant                                     | Cloud group used to deploy new bots.
| CLOUD_USERNAME         | someone@domain                                   | Cloud username used to deploy new bots.
| CLOUD_PASSWORD         | <use a password generator>                       | Cloud password used to deploy new bots.
| MARKETPLACE_ID         | 9c90ff1c3-101b-4f0d-85cd-4bada2226fe3            | Martplace identifier associated to the boot bot.
| MARKETPLACE_SECRET     | nzrNUUG6214%raqzYWQ8(+%                          | Martplace password associated to the boot bot.
| STORAGE_DIALECT        | mssql                                            | The bot database dialect configuration value. Can be MSSQL or SQLITE.
| STORAGE_SERVER         | newassistant-storage-server.database.windows.net | The bot database server name configuration value.
| STORAGE_NAME           | newassistant-storage                             | The bot database name configuration value.
| STORAGE_USERNAME       | sahaaksfqiehke                                   | The bot database security username configuration value.
| STORAGE_PASSWORD       | <use a password generator>                       | The bot database security password configuration value.
| STORAGE_SYNC           | true                                             | If the bot server should sync database before running.
| PRIVACY_STORE_MESSAGES | true                                             | If the bot server should store message logs in the database.
| TEST_MESSAGE           | /publish                                         | If the bot server should auto send a message for test.
| TEST_SHELL             | rm work/..                                       | If the user needs to continuously remove an archive.
| GBDIALOG_GBDATABOT     | Shared.gbai/Shared.gbdata                        | If defined, BotServer will use this .gbdata instead of default location.
## How to

### Move to production (Azure)

* Update bot endpoint;

## Bot Analytics

## Cloud Internals


