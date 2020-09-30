# About Packages

Packages can be stored as folders in the file system, synced with cloud storages and
content management systems like SharePoint and even sent like .zip files on a e-mail.
Just to increse bot knowledge, intelligence and how they look to us. So working on a
General Bots project is like to split the work on several packages if needed and work
on a package at once or even share the work with collegues, agencies or development
companies to more advanced package building.composite packages on GeneralBots:

 .gbai
 .gbapp
 .gbot
 .gbtheme
 .gbkb
 .gblib



## How To

### Configure the server to deploy specific directory

1. Create/Edit the .env file and add the ADDITIONAL_DEPLOY_PATH key pointing to the .gbai local parent folder of .gbapp, .gbot, .gbtheme, .gbkb package directories.
2. Specify STORAGE_SYNC to TRUE so database sync is run when the server is run.
3. In case of Microsoft SQL Server add the following keys: STORAGE_SERVER, STORAGE_NAME, STORAGE_USERNAME, STORAGE_PASSWORD, STORAGE_DIALECT to `mssql`.

Note:

- You can specify several bots separated by semicolon, the BotServer will serve all of them at once.

## Description of packages

### .gbai

Embraces all packages types (content, logic & conversation) into a pluggable bot
directory. [A sample .gbai is available](https://github.com/pragmatismo-io/IntranetBotQuickStart.gbai).

### .gbapp

The artificial intelligence extensions in form of pluggable apps. Dialogs,
Services and all model related to data. A set of interactions, use cases,
integrations in form of conversationals dialogs.
The .gbapp adds the General Bot base library (botlib) for building Node.js TypeScript Apps packages.

Four components builds up a General Bot App:

- dialogs
- models
- services
- tests

#### Dialogs

All code contained in a dialog builds the flow to custom conversations in
built-in and additional packages .

#### Models

Models builds the foundation of data relationships in form of entities.

#### Services

Services are a façade for bot back-end logic and other custom processing.

#### Tests

Tests try to automate code execution validation before crashing in production.

### .gbot

An expression of an artificial inteligence entity. A .gbot file defines
all bots dependencies related to services and other resources.

### .gbtheme

A theme of a bot at a given time. CSS files & images that can compose all UI
presentation and using it a branding can be done. [A sample .gbtheme is available](https://github.com/pragmatismo-io/Office365.gbtheme)

### .gbkb

A set of subjects that bot knows in a form of hierarchical menu-based QnA. [A sample .gbkb is available](https://github.com/pragmatismo-io/ProjectOnline.gbkb).

### .gblib

Shared code that can be used across bot apps.

## System Package Quick Reference

|Whatsapp|Web|Core|KB|
|----|-----|----|----|
|[whatsapp.gblib](https://github.com/pragmatismo-io/BotServer/tree/master/packages/whatsapp.gblib)|[default.gbui](https://github.com/pragmatismo-io/BotServer/tree/master/packages/default.gbui)|[core.gbapp](https://github.com/pragmatismo-io/BotServer/tree/master/packages/core.gbapp)|[kb.gbapp](https://github.com/pragmatismo-io/BotServer/tree/master/packages/kb.gbapp)|
