# .gbapp Guide
![generalbots-2018](https://user-images.githubusercontent.com/65977273/94922431-949c3900-0490-11eb-800a-6b478d689f2a.png)

## Introduction

.gbapp is the folder extension for the General Bots Application package type.
Anything inside a folder considered a .gbapp will be consumed by the server
like a TypeScript application. This conversational application will contain
the source code for custom dialogs and behaviour for any .gbot that associate
this deployed .gbapp.

A good way to start a .gbapp is to find a NPM package to create a .gbapp that
asks for data and output the result. For example, a temperature package can
be installed via `npm install temperature` and then have its methods
convertToKelvin or convertToCelsius called when user asks for conversion. A
.gbapp can persist and read data from database according to the conversation
session.

## Preparing Environment

General procedures:

1. Get SubscriptionId, username and password;
2. Create AppId and Secret;
3. Deploy General Bots;
4. /setupSecurity to get access to Bot Drive;
5. /publish to publish packages on root bot.

### Windows

#### PowerShell Script

Copy and paste on a PowerShell prompt with elavated privileges and when VSCode is opened just press F5 to run the development server. 
Please ensure that Node.js is not installed.

``` powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

cinst git --confirm
cinst nodejs --confirm --version=19.3.0
cinst vscode --confirm

Install Python: https://www.python.org/downloads/release/python-2718/


Enter your Source Directory:

&"C:\Program Files\Git\bin\git.exe" clone https://github.com/GeneralBots/BotServer.git
cd BotServer
&"C:\Program Files\Microsoft VS Code\bin\code.cmd" .

```

### Linux (Ubuntu)

Visual Studio Code
```
sudo apt update
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update
sudo apt install code

```

Node JS 14
```

curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs
node -v
sudo apt install npm 
npm -v

```

Additional Infrastructure 
```
sudo apt-get install libxtst-dev
apt-get install libpng-dev
sudo apt-get install python g++ build-essential
npm install -g node-gyp

```
### Setup git

```
    git config --global user.name "Your Name"
    git config --global user.email "someone@domain.com"
```

### Commands to check version of Node.js and NPM.
![verificar](https://user-images.githubusercontent.com/65977273/95104867-bace0d00-070c-11eb-9699-66d3b6134ea5.png)


#### Manual steps.

1. Install [Chocolatey](https://chocolatey.org/install), a Windows Package Manager; 
2. Install [git]( `https://git-scm.com/` ), a Software Configuration Management (SCM) and TortoiseGit; 
3. Install [Node.js](https://npmjs.com/get-npm), a [Runtime system](https://en.wikipedia.org/wiki/Runtime_system); 
4. Install Visual Studio Code Insiders, Brackets or Atom as an editor of your choice;
5. Fork the repository by visiting https://github.com/pragmatismo-io/BotServer/fork;
6. Clone the just forked repository by running `git clone <your-forked-repository-url>/BotServer.git` ; 
7. Run the bot server by `gbot.cmd` .


#### Common Errors

- The subscription is not registered to use namespace 'Microsoft.Web'. See https://aka.ms/rps-not-found for how to register subscriptions.
-- Enter Azure | <Subscription> | Resource providers | Find Microsoft.Web and check it.


* Required packages

``` cmd

cinst git --confirm
cinst nodejs --confirm
npm install windows-build-tools -g
cinst tortoisegit --confirm

```

* Optional packages

``` 

cinst 7zip.install --confirm
cinst tortoisegit --confirm
cinst winscp --confirm
cinst sysinternals --confirm
cinst putty --confirm
cinst pandoc --confirm
cinst curl --confirm
cinst micro --confirm
cinst ccleaner --confirm
cinst notepadplusplus --confirm
cinst sql-server-management-studio --confirm

```

* node packages

``` 

npm install -g npm-check-updates
npm install -g cost-of-modules

```

Linux
    
```
# MS Remote Desktop Connection (RDP Client) 
    
sudo apt-add-repository ppa:remmina-ppa-team/remmina-next
sudo apt update
sudo apt install remmina remmina-plugin-rdp remmina-plugin-secret

```

# File compression
    
``` 

    Compressing a directory in Linux:
    
    tar -cvzf my_archive.tar.gz input_dir
    
    Expanding an archive in Linux:
    
    tar -xf my_archive.tar.gz 
    
```
    
    
![General Bots Inside Visual Studio Code provides a complete artificial intelligence based conversational platform](https://raw.githubusercontent.com/pragmatismo-io/BotServer/master/docs/images/general-bots-inside-visual-studio-code-provides-a-complete-artificial-intelligence-based-conversational-platform.png)

## Specifications 

## Dialogs

The dialog is built by specifing series of methods, disposed as an array as seen
on Figure 1. Each dialog has also an identifier that can be called by several
engines like kb.gbapp, which handles cloud based search for documents and other
knowledge base information and also routes for the natural language processing
(NLP) engine.

``` typescript

static getDialogs(bot: BotAdapter, min: GBMinInstance) {
    return [{name:"/convertTemperature", waterfall: [
        async step => {
        },
        async step => {
        },
        async step => {
        }]
    },{name:"/convertCurrency", waterfall: [
        async step => {
        },
        async step => {
        },
        async step => {
        }]
    }
    ]
```

    *Figure 1 - How to build dialogs in General Bots using TypeScript*


## Fork concept

Is the implementation of new software based on existing software. The branch takes advantage of the data already used in other software to generate a new one.
This in some way contributes to a better understanding of how it works.

## How To...

### Debugging .gbapp deployed on Azure

1. Visit https://<SITENAME>.scm.azurewebsites.net/api/vfs/LogFiles/Application/index.html

## Commit code
    
See https://semver.org/.

### Numbering

1.0.0
MAJOR.MINOR.PATCH
(BREAK.FEATURE.BUG)

### Messsages

- A fix in the code:

```
fix(azuredeployer.gbapp): stop graphite breaking when too much pressure applied Patch Fix Release 
```

- A new feature

```
feat(core.gbapp): add 'graphiteWidth' option 
```

- A commit without incrementing version number:

```
BREAKING CHANGE: The graphiteWidth option has been removed.
```

or

```
perf(core.gbapp): Improved loop.
```
    
    
### Rules

- BREAK: If the body contains the text “BREAKING CHANGE” then MAJOR version is incremented.
- FEATURE: If the type contains feat/feature, then MINOR version is incremented.
- BUG If the type contains fix, then PATCH version is incremented.

And finally, if the type contains refactor/style/perf/doc/test/chore, then nothing is increment and no release is made.

Source: https://medium.com/agoda-engineering/automating-versioning-and-releases-using-semantic-release-6ed355ede742
    
## Tooling

### JavaScript

| Título                                      | Endereço                                                                                          |
|---------------------------------------------|---------------------------------------------------------------------------------------------------|
|                                             | https://deeplearnjs.org/                                                                          |
|                                             | Oimo.js http://lo-th.github.io/Oimo.js/\#stacking                                                 |
|                                             | js-sequence-diagrams: https://bramp.github.io/js-sequence-diagrams/                               |
|                                             | http://blog.avenuecode.com/a-library-for-data-visualization-d3.js                                 |
| Chrome inside Node.js                       | https://github.com/GoogleChrome/puppeteer                                                         |
| XLSX loader                                 | https://github.com/mgcrea/node-xlsx                                                               |
| Node.js bindings for CNTK                   | https://github.com/nadavbar/node-cntk                                                             |
| API Repository                              | https://any-api.com/                                                                              |
| ORM                                         |                                                                                                   |
| Migração de . NET para JavaScript (Node.js) | https://www.reddit.com/r/webdev/comments/2val7s/as_a_net_developer_do_i_need_to_care_about_nodejs |
| Simplified JavaScript Jargon                | http://jargon.js.org                                                                              |
| RegExp | https://regexp101.com |

### Packages

| Título | Descrição                        | URL                                |
|--------|----------------------------------|------------------------------------|
| MSAL   | Microsoft Authentication Library | https://www.npmjs.com/package/msal |

### Visual Studio Code Shotcut keys

| Key                      | Description                                                                   |
|--------------------------|-------------------------------------------------------------------------------|
| F8                       | Next error.                                                                   |
| F12                      | Go to symbol definition.                                                      |
| F5                       | Run.                                                                          |
| CTRL + .                 | Auto refactoring (Fix).                                                       |
| ALT + SHIFT + DOWN ARROW | Duplicate the line code.                                                      |
| CTRL + SHIFT + H         | Replace all followed by CTRL + ALT + ENTER on replace text box.               |
| CTRL + SHIFT + B         | Compile inside VSCode, you can also open an external terminal and run tsc -w. |
| CTRL + G                 | Go to the specified line.                                                     |
| CTRL + SHIFT + G         | Goes to Git.                                                                  |
| CTRL + SHIFT+P           | Opens the Command Palette                                                     |
| CTRL + ALT+UP/DOWN ARROW | Enter the Vertical Selection mode                                             |
| ALT + UP/DOWN ARROW      | Move lines                                                                    |

### Node Packages

| Title                                        | Description                                                                    |
|----------------------------------------------|--------------------------------------------------------------------------------|
| @azure/arm-appservice | |
| @azure/arm-cognitiveservices | |
| @azure/arm-resources | |
| @azure/arm-search | |
| @azure/arm-sql | |
| @azure/arm-subscriptions | |
| @azure/cognitiveservices-computervision | |
| @azure/keyvault-keys | |
| @azure/ms-rest-js | |
| @azure/msal-node | |
| @azure/search-documents | |
| @google-cloud/pubsub | |
| @google-cloud/translate | |
| @hubspot/api-client | |
| @microsoft/microsoft-graph-client | |
| @nosferatu500/textract | |
| @semantic-release/changelog | |
| @semantic-release/exec | |
| @semantic-release/git | |
| @sendgrid/mail | |
| @types/node | |
| @types/validator | |
| adm-zip | |
| alasql | |
| any-shell-escape | |
| async-promises | |
| basic-auth | |
| billboard.js | |
| bluebird | |
| body-parser | |
| botbuilder | |
| botbuilder-adapter-facebook | |
| botbuilder-ai | |
| botbuilder-dialogs | |
| botframework-connector | |
| botlib | |
| c3-chart-maker | |
| chatgpt | |
| chrome-remote-interface | |
| cli-progress | |
| cli-spinner | |
| core-js | |
| data-forge | |
| date-diff | |
| docxtemplater | |
| dotenv-extended | |
| exceljs | |
| express | |
| express-remove-route | |
| ffmpeg-static                                | Converts multiple video/audio format, wrapper to [ffpmeg](https://ffmpeg.org/). |
| google-libphonenumber | |
| googleapis | |
| ibm-watson | |
| indent.js | |
| js-beautify | |
| keyv | |
| koa | |
| koa-body | |
| koa-router | |
| lodash | |
| luxon | |
| mammoth | |
| moment | |
| ms-rest-azure | |
| nexmo | |
| node-cron | |
| node-nlp | |
| node-tesseract-ocr | |
| npm | |
| open | |
| pdf-extraction | |
| pdfkit | |
| phone | |
| pizzip | |
| pptxtemplater | |
| pragmatismo-io-framework | |
| prism-media | |
| public-ip | |
| punycode | |
| puppeteer | |
| puppeteer-extra | |
| puppeteer-extra-plugin-stealth | |
| qrcode | |
| qrcode-terminal | |
| readline | |
| reflect-metadata | |
| rimraf | |
| safe-buffer | |
| scanf | |
| sequelize | |
| sequelize-cli | |
| sequelize-typescript | |
| simple-git | |
| speakingurl | |
| ssr-for-bots" | |
| strict-password-generator | |
| swagger-client | |
| tabulator-tables | |
| tedious | |
| textract | |
| twitter-api-v2 | |
| typescript | |
| typescript-rest-rpc | |
| url-join | |
| vbscript-to-typescript | |
| vhost | |
| vm2 | |
| vm2-process | |
| walk-promise | |
| washyourmouthoutwithsoap | |
| whatsapp-web.js | |
| winston | |
| winston-logs-display | |
| yarn | |

### Node Packages (Dev Dependencies)

| Title                                        | Description                                                                    |
|----------------------------------------------|--------------------------------------------------------------------------------|
| simple-commit-message | |
| @types/url-join | |
| ban-sensitive-files | |
| commitizen | |
| cz-conventional-changelog | |
| dependency-check | |
| git-issues | |
| license-checker | |
| ngrok | |
| prettier-standard | |
| semantic-release | |
| travis-deploy-once | |
| ts-node | |
| tslint | |

    
    
### Visual Studio Code Extensions

| Title                                        | Description                                                     |
|----------------------------------------------|-----------------------------------------------------------------|
| mbinic.tgit-cmds                             | Set of commands for launching TortoiseGit dialogs               |
| tomashubelbauer.vscode-markdown-table-format | Formats MarkDown tables so that all columns have the same width |
| esbenp.prettier-vscode                       | VS Code plugin for prettier/prettier (wraps at column 80)       |
| mikestead.dotenv                             | .env support                                                    |
| abhinavk99.codewall                          | Description here                                                |
| christian-kohler.npm-intellisense            | Description here                                                |
| csholmq.excel-to-markdown-table              | Description here                                                |
| davidanson.vscode-markdownlint               | Description here                                                |
| eg2.ts-tslint                                | Description here                                                |
| eg2.vscode-npm-script                        | Description here                                                |
| esbenp.prettier-vscode                       | Description here                                                |
| formulahendry.auto-rename-tag-               | Description here                                                |
| gruntfuggly.align-mode                       | Description here                                                |
| jmfirth.vsc-space-block-jumper               | Description here                                                |
| kaiwood.indentation-level-movement           | Description here                                                |
| mbinic.tgit-cmds                             | Description here                                                |
| mechatroner.rainbow-csv                      | Description here                                                |
| mikestead.dotenv                             | Description here                                                |
| sirtori.indenticator                         | Description here                                                |
| tandy.color-basic                            | Description here                                                |

## Common tasks

| Task          | Description                         |
|---------------|-------------------------------------|
| npm update -g | Updates NPM                         |
| node -v       | Checks node version                 |
| ncu -a        | Update all packages in package.json |

## Useful documentation 
-https://www.typescriptlang.org/docs/handbook (TypeScript Documentation).
