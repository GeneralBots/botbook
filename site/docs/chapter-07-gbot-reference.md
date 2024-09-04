---
sidebar_position: 70
---

# .gbot Reference

## Instance custom params

## Commands

General Bot can be controlled by the same chat window people talk to, so
here is a list of admin commands related to deploying .gb* files.

| Command         | Description                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------|
| /edit           | Sends a link to the Bot Storage so package folders like .gbdialog, .gbkb, .gbot and others can be edited.       |
| /setupSecurity [tokenName]   | Setup connection between General Bots and the Cloud, so the bot drive can be accessed by BotServer during publishing and direct access like the FIND keyword. Or using tokenName, setups a connection defined in Config.xlsx.|
| /publish [extension]  | Deploy the package to the bot storage. When ommited, the command will publish the package named (botId).gbkb by default. |

# Config.xlsx (.gbot) Configuration
  
| Name                        | Description|
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Admin Notify E-mail         | E-mail used to notify administrators. |
| Answer Mode                 | How LLM is used.  Can be "direct", "document", "document-ref", "sql", "tool". |
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

## Config in Detail

### Admin Notify E-mail
The "Admin Notify E-mail" setting specifies the email addresses that will receive notifications regarding the bot’s activities and administrative updates. This feature ensures that administrators are promptly informed about any critical events or issues related to the bot's operation, allowing them to take necessary actions swiftly.

### Answer Mode

In a bot factory configuration, the integration of a Language Learning Model (LLM) is pivotal in enhancing the functionality and efficiency of the bots. The LLM can be employed in various modes depending on the requirements of the bot system. These modes include "direct," "document," "document-ref," "sql," and "tool," each offering a unique method of interaction and data handling. For instance, in the "direct" mode, the LLM is used to generate responses or actions based on real-time user input, providing immediate and contextually relevant replies. This approach is particularly useful for creating conversational agents that can handle a wide range of user queries effectively.
In the "document" mode, the LLM processes and generates responses based on pre-existing documents or content. This mode is ideal for scenarios where the bot needs to reference detailed information or provide insights derived from specific documents. The LLM analyzes the content of the documents to deliver accurate and contextually appropriate information, thereby enhancing the bot's ability to offer valuable and precise responses. This approach is particularly beneficial for applications that require in-depth knowledge or detailed guidance based on existing resources.
The "document-ref" mode builds on the document-based approach by allowing the LLM to reference and extract information from multiple documents to generate comprehensive responses. This mode is advantageous when the bot needs to synthesize information from various sources to provide well-rounded answers or perform complex tasks. In contrast, the "sql" mode leverages structured query language to interact with databases, enabling the LLM to retrieve and manipulate data based on specific queries. Lastly, the "tool" mode integrates the LLM with external tools or services, allowing the bot to extend its functionality by interacting with other applications or systems. Each mode offers a distinct advantage, allowing the bot factory to tailor its approach based on the specific needs and objectives of the bot system.

### Avatar Logo
The "Avatar Logo" is the URL of the bot's logo that represents it visually. This logo is used in user interfaces and communications to create a recognizable identity for the bot, enhancing its brand presence and user engagement.

### Can Publish
The "Can Publish" setting is a comma-separated list of mobile numbers that have the authority to publish content directly. This feature ensures that only authorized individuals can contribute or update content, maintaining control over the bot's published material.

### Description
The "Description" provides a brief overview of the bot, including its purpose, functionalities, and key features. This description helps users understand what the bot does and what to expect from its interactions.

### Enable Audio Hearing
The "Enable Audio Hearing" option indicates whether the bot can process and understand audio inputs. When set to TRUE, the bot is capable of receiving and interpreting spoken language, enhancing its interaction capabilities.

### Enable Audio Talking
The "Enable Audio Talking" setting specifies if the bot can generate and deliver spoken responses. Enabling this feature allows the bot to communicate with users through audio, making interactions more dynamic and engaging.

### Enable Spelling Checker
The "Enable Spelling Checker" option determines whether the bot should automatically check and correct spelling errors in user inputs. When set to TRUE, this feature helps maintain the quality and accuracy of interactions by addressing spelling mistakes.

### Enable Worldwide Translator
The "Enable Worldwide Translator" setting allows the bot to support multiple languages and perform translation tasks. When enabled, the bot can interact with users in various languages, catering to a global audience.

### Default User Language
The "Default User Language" specifies the language that users will encounter by default when interacting with the bot. This setting ensures that the bot communicates in the preferred language of the user, enhancing their experience.

### Default Content Language
The "Default Content Language" defines the language in which content files, such as .gbkb and .gbdialog, are written. This setting ensures consistency in content creation and processing within the bot's system.

### Language Detector
The "Language Detector" feature enables the bot to automatically identify the language of user inputs. When activated, the bot can adapt its responses based on the detected language, improving communication accuracy.

### NLP Score
The "NLP Score" is a numerical value between 0 and 1 used to assess the relevance and quality of text for Natural Language Processing (NLP) neural networks. This score helps in classifying and processing text more effectively.

### Search Score
The "Search Score" is a value between 0 and 1 that influences the consideration of Full Text Search as a content retrieval method. A higher score indicates a greater emphasis on search-based content retrieval.

### Transfer To
The "Transfer To" setting is a comma-separated list of mobile numbers to which the bot will transfer chats from WhatsApp. This feature facilitates the rerouting of conversations to designated contacts or support agents.

### WhatsApp Admins
The "WhatsApp Admins" field is a comma-separated list of mobile numbers designated as administrators for the bot. These individuals have elevated access and control over the bot’s settings and operations.

### Feedback Improve.Message
The "Feedback Improve.Message" is a predefined message that the bot will send to users when it fails to find the requested information. This message encourages users to provide feedback or try different queries.

### Keep Text
The "Keep Text" setting is a comma-separated list of words or phrases that should remain unchanged during the bot’s understanding process. This feature ensures that specific terms are preserved and accurately recognized.

### Start Dialog
The "Start Dialog" specifies the name of the .docx file (without the extension) that serves as the entry point for the bot’s dialog. This document outlines the initial interactions and flow of the conversation.

### HelloGoodX
The "HelloGoodX" option determines whether the bot should greet users with a welcome message. When set to TRUE, the bot will initiate interactions with a friendly hello.

### XRM Key
The "XRM Key" is a string key used to authenticate and access the HubSpot API. This key is essential for integrating the bot with HubSpot services and functionalities.

### WhatsApp Group Name
The "WhatsApp Group Name" is the name of the WhatsApp group to which the bot belongs. This setting helps in identifying and organizing the bot’s presence within specific groups.

### WhatsApp Group Shortcuts
The "WhatsApp Group Shortcuts" are space-separated triggers in text that activate the bot within WhatsApp groups. These shortcuts enable users to engage with the bot using predefined commands or keywords.

### Bot Admin Number
The "Bot Admin Number" is the mobile number that receives debug screenshots and other notifications related to the bot’s operation. This contact is crucial for monitoring and troubleshooting the bot.

### WhatsApp Group ID
The "WhatsApp Group ID" is a unique identifier used to connect the bot to a specific WhatsApp group. This ID is accessible only in internal logs and is essential for group integration.

### Debug Web Automation
The "Debug Web Automation" setting indicates whether the Bot Admin Number should receive screenshots of each web automation step. Enabling this feature provides detailed visibility into web automation processes.

### .gbapp List
The ".gbapp List" is a collection of associated .gbapp packages linked to the .gbot. This list helps in managing and organizing the bot’s application packages.

### Group Spell
The "Group Spell" option enables the spell checker for group interactions. When activated, the bot will check and correct spelling errors in group chat messages.

### Synchronize Database
The "Synchronize Database" setting determines whether the TABLE keyword should modify the database. Setting this to TRUE allows changes to the database schema, while FALSE should be used in production environments to prevent unintended modifications.

---

Each title and description has been crafted to clarify the purpose and functionality of the respective configuration setting.


## Enviroment Variables Reference

| Name                   | Sample Value                                     | Description |
|------------------------|--------------------------------------------------|-------------|
| ADDITIONAL_DEPLOY_PATH | D:\data\gbai                                     | Deploy folder to look for packages (Just one folder). 
| ADMIN_PASS             | E732+!#xJ3a_*!                                   | Administration password for the conversational interface.
| CLOUD_SUBSCRIPTIONID   | 622e5037-f7f1-49f6-a9c4-28babbb0fs               | Cloud subscription ID used to deploy new bots.
| CLOUD_LOCATION         | westus                                           | Cloud location used to deploy new bots.
| CLOUD_GROUP            | newassistant                                     | Cloud group used to deploy new bots.
| CLOUD_USERNAME         | someone@domain                                   | Cloud username used to deploy new bots.
| CLOUD_PASSWORD         | (use a password generator)                       | Cloud password used to deploy new bots.
| MARKETPLACE_ID         | 9c90ff1c3-101b-4f0d-85cd-4bada2226fe3            | Martplace identifier associated to the boot bot.
| MARKETPLACE_SECRET     | nzrNUUG6214%raqzYWQ8(+%                          | Martplace password associated to the boot bot.
| STORAGE_DIALECT        | mssql                                            | The bot database dialect configuration value. Can be MSSQL or SQLITE.
| STORAGE_SERVER         | newassistant-storage-server.database.windows.net | The bot database server name configuration value.
| STORAGE_NAME           | newassistant-storage                             | The bot database name configuration value.
| STORAGE_USERNAME       | sahaaksfqiehke                                   | The bot database security username configuration value.
| STORAGE_PASSWORD       | (use a password generator)                       | The bot database security password configuration value.
| STORAGE_SYNC           | true                                             | If the bot server should sync database before running.
| PRIVACY_STORE_MESSAGES | true                                             | If the bot server should store message logs in the database.
| TEST_MESSAGE           | /publish                                         | If the bot server should auto send a message for test.
| TEST_SHELL             | rm work/..                                       | If the user needs to continuously remove an archive.
| GBDIALOG_GBDATABOT     | Shared.gbai/Shared.gbdata                        | If defined, BotServer will use this .gbdata instead of default location.
## How to

### Move to production (Azure)

* Update bot endpoint;
* 

### WhatsApp Procedures

#### Register Phone Number

1. Open [Facebook App Dashboard](https://developers.facebook.com/apps) and register the App;
2. Go to WhatsApp, API Setup and register the phone and save the Phone number ID to update the WhatsAppServiceNumer in GuaribasInstance.
3. Generate a System User and associate it to the App;
4. Get the token from User and update the WhatsAppServiceKey;

#### Register PIN.
```
https://graph.facebook.com/v18.0/999996037087713/
{"pin" : "999999"}
```

##### Register Account.
```
https://graph.facebook.com/v18.0/999997245497156/register
{
    "messaging_product": "whatsapp", "pin":999999
}
```

##### Define message in profile.
```
https://graph.facebook.com/v18.0/99999792462862/whatsapp_business_profile
{
"messaging_product": "whatsapp",
"about": "Online"
}
```

## Bot Analytics

## Cloud Internals

