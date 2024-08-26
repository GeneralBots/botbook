---
sidebar_position: 10
---

# Run and Talk

### Bot Development Stack

![General Bot Logo](https://github.com/GeneralBots/BotServer/blob/main/docs/images/general-bots-stack.png)

### Diagram Description

1. **gbapp** and **gblib** are folder extensions within the GeneralBots package type, responsible for GeneralBots services in a back-end development environment. A General Bot App comprises four components: dialogs, models, services, and tests.

2. The **.gbui** extension pertains to the GeneralBots front-end development environment. Angular, Riot, React, and HTML enable dynamic functionality for GeneralBots services.

3. The **.gtheme** extension is utilized by GeneralBots designers using CSS and PS technologies. A theme consists of CSS files and images.

4. **.gbDialog** is an extension responsible for GeneralBots' communication with end-users through bot services. **.gbkb** is a package for executing various types of media.

5. The **.gbot** extension refers to the GeneralBots service product.

6. **.gbai** denotes the architecture construction of the GeneralBots application.

### The Bot Factory

![General Bots Block Architecture](https://raw.githubusercontent.com/pragmatismo-io/BotServer/master/docs/images/general-bots-block-architecture.png)

GeneralBots aims to deliver bots on Azure in an easy and efficient manner. Utilize office tools like Word or Excel for editing your bot, leveraging code (JavaScript or TypeScript) only for custom requirements.

## How To

### Running the Server Locally

1. Install [Node.js](https://www.npmjs.com/get-npm), the current-generation General Bot code execution platform.
2. Open a **Terminal** on Linux and Mac, or a **Command Prompt** or PowerShell window on Windows.
3. Type `npm install -g botserver` and press **ENTER**.
4. Type `gbot` to start the server core.

### Notes:

- [*nodejs.install* Chocolatey Package](https://chocolatey.org/packages/nodejs.install) is also available (Chocolatey is a Windows package manager).
- The zip source code for General Bot is available for [Download](https://codeload.github.com/pragmatismo-io/BotServer/zip/master).

### Running Unit Tests

1. Navigate to the BotServer root folder.
2. Execute tests with `npm test`.

### Copying Source Code to Your Machine

1. [Download](https://codeload.github.com/pragmatismo-io/BotServer/zip/master) the zip file.

## Omnichannel

Omnichannel allows conversations to flow seamlessly regardless of the channel, as all interactions are recorded, preserving the consumer's history and profile.

## Spell Checker

GeneralBots performs spell-checking to identify and correct typographical errors.

## Speech to Text

Enable user speech recognition directly with GeneralBots.

## Branding

Branding encompasses all aspects of a company's identity management, including its name and corporate visual elements.
processing, and output through natural language.

---
