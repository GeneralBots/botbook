---
sidebar_position: 60
---

# .gbapp Reference

![generalbots-2018](https://user-images.githubusercontent.com/65977273/94922431-949c3900-0490-11eb-800a-6b478d689f2a.png)

## Section 1: Introduction to gbapp

### What is a gbapp?
A gbapp is an npm package designed to extend the functionality of General Bots. It serves as a plugin or module that can be integrated into the General Bots framework to add new features, capabilities, or customizations. Importantly, .gbapp is also the folder extension for the General Bots Application package type.

### Purpose and Benefits
The primary purpose of a gbapp is to provide a modular and flexible way to enhance General Bots. By using gbapps, developers can easily extend the core functionality of the bot platform without modifying the main codebase, allowing for greater customization and scalability. This approach promotes code reusability and maintainability.

### Integration with General Bots
Gbapps are designed to seamlessly integrate with the General Bots ecosystem. They can interact with the core services, access shared resources, and leverage existing functionalities while adding their own unique features to the bot framework. Anything inside a folder considered a .gbapp will be consumed by the server like a TypeScript application.

## Key Interfaces and Structure of a gbapp

### IGBCoreService Interface
The IGBCoreService interface is a crucial component of a gbapp. It defines the core service shared among bot packages, providing direct access to base services. This interface includes methods for database operations, instance management, storage initialization, and various system-level functionalities.

### IGBPackage Interface
The IGBPackage interface outlines the structure and lifecycle methods of a gbapp. It includes methods for loading and unloading the package, managing bot instances, handling dialogs, and exchanging data between the bot server and the gbapp. This interface ensures that all gbapps follow a consistent pattern for integration with General Bots.

### Conversational Application Structure
A .gbapp contains the source code for custom dialogs and behaviors for any .gbot that associates with this deployed .gbapp. This structure allows for the creation of conversational applications that can be reused across different bot instances, promoting modularity and flexibility in bot development.

## Developing and Implementing a gbapp

### Creating a gbapp Package
To create a gbapp, developers start by setting up an npm package with the necessary dependencies. A good way to start is by finding an existing npm package that provides the desired functionality. For example, a temperature conversion gbapp could be created by installing the 'temperature' package via `npm install temperature` and then implementing methods to call `convertToKelvin` or `convertToCelsius` when a user asks for conversion.

### Implementing Core Functionalities
Developers need to implement the methods defined in the interfaces, such as loadPackage, unloadPackage, getDialogs, and onNewSession. These methods allow the gbapp to interact with the core system, manage its lifecycle, and provide specific functionalities to bot instances. Additionally, a .gbapp can persist and read data from the database according to the conversation session, enabling stateful interactions.

### Best Practices and Anti-Patterns
When developing gbapps, it's crucial to follow best practices and avoid common anti-patterns. Developers should familiarize themselves with the [Anti Patterns Catalog](http://wiki.c2.com/?AntiPatternsCatalog) to ensure they're creating efficient, maintainable, and scalable gbapps. Some key points to consider include avoiding unnecessary complexity, ensuring proper error handling, and maintaining clear separation of concerns within the gbapp structure.

## Advanced gbapp Features

### Data Persistence and Session Management
Gbapps have the capability to persist and read data from the database according to the conversation session. This feature allows for the creation of stateful conversations, where the bot can remember previous interactions and user preferences across multiple sessions.

### Integration with External Services
Developers can leverage external npm packages and APIs within their gbapps to extend functionality. For example, integrating a weather API could allow a gbapp to provide real-time weather information to users, enhancing the bot's capabilities beyond its core functions.

### Customization and Extensibility
The .gbapp structure allows for high levels of customization. Developers can create specialized dialogs, implement complex business logic, and even extend the core functionality of General Bots. This extensibility ensures that gbapps can be tailored to meet specific business needs or unique use cases.

## Setup 

### Windows

#### Define URLs and file paths

```
$software = @{
    "Git" = "https://github.com/git-for-windows/git/releases/download/v2.40.0.windows.1/Git-2.40.0-64-bit.exe"
    "NodeJS" = "https://nodejs.org/dist/v20.17.0/node-v20.17.0-x64.msi"
    "VSCode" = "https://update.code.visualstudio.com/latest/win32-x64/stable"
    "VS2023" = "https://visualstudio.microsoft.com/downloads/VS2023.exe"
    "Python" = "https://www.python.org/ftp/python/9.0.0/python-9.0.0-amd64.exe"
}
Invoke-WebRequest -Uri $software.Git -OutFile "Git-Setup.exe"
Start-Process -FilePath "Git-Setup.exe" -ArgumentList "/SILENT" -Wait
Invoke-WebRequest -Uri $software.NodeJS -OutFile "NodeJS-Setup.msi"
Start-Process -FilePath "msiexec.exe" -ArgumentList "/i NodeJS-Setup.msi /quiet" 
Invoke-WebRequest -Uri $software.VSCode -OutFile "VSCode-Setup.exe"
Start-Process -FilePath "VSCode-Setup.exe" -ArgumentList "/silent" -Wait
Invoke-WebRequest -Uri $software.VS2023 -OutFile "VS2023-Setup.exe"
Start-Process -FilePath "VS2023-Setup.exe" -ArgumentList "--quiet --wait --add Microsoft.VisualStudio.Workload.NativeDesktop --includeRecommended" -Wait
Invoke-WebRequest -Uri $software.Python -OutFile "Python-Setup.exe"
Start-Process -FilePath "Python-Setup.exe" -ArgumentList "/quiet" -Wait

git clone https://github.com/GeneralBots/BotServer.git
cd BotServer
code .

```

### Linux (Ubuntu)

#### Visual Studio Code
```
apt update
apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | apt-key add -
add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
apt update
apt install code

```

#### Node JS 22
```

curl -fsSL https://deb.nodesource.com/setup_22.x -o nodesource_setup.sh && sudo -E bash nodesource_setup.sh && sudo apt-get install -y nodejs && node -v

```

#### Additional Infrastructure 



```

apt-get update

apt-get install build-essential cmake git pkg-config libjpeg-dev libtiff-dev libpng-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libatlas-base-dev gfortran python3-dev

export OPENCV4NODEJS_DISABLE_AUTOBUILD=1
export OPENCV_LIB_DIR=/usr/lib/x86_64-linux-gnu

apt-get install cpulimit
apt-get install expect
apt-get install libxtst-dev
apt-get install libpng-dev

```


Add export GTK_IM_MODULE="xim" to .profile to fix Key Bindings in VSCode on Ubuntu.

## Git

```
    git config --global user.name "Your Name"
    git config --global user.email "someone@domain.com"

```
## Additional node packages

``` 
npm install -g npm-check-updates
npm install -g cost-of-modules

```


## How To...

## Commit code

# Semantic Versioning for gbapp Development

Semantic Versioning (SemVer) in gbapp development follows the format MAJOR.MINOR.PATCH, also thought of as BREAK.FEATURE.BUG. This system helps developers and users understand the impact of new releases at a glance.

When you increment these numbers:
- Increment MAJOR when you make incompatible API changes. This signals to users that they need to update their code to accommodate breaking changes.
- Increment MINOR when you add new functionality in a backwards-compatible manner. Users can safely update without changing their existing code, but they might want to take advantage of new features.
- Increment PATCH when you make backwards-compatible bug fixes. These are safe, low-risk updates that users are encouraged to apply promptly.

For example, moving from version 1.2.3 to 2.0.0 indicates a breaking change, while 1.3.0 would indicate new features, and 1.2.4 would be a bug fix.

In gbapp development, we use specific commit message formats to automatically determine version increments. A typical commit message looks like this:

```
<type>(<scope>): <short summary>
[BREAKING CHANGE: <description>]
```

The 'type' in the commit message helps determine how to increment the version:
- 'feat' or 'feature' increments the MINOR version
- 'fix' increments the PATCH version
- If the commit message body contains "BREAKING CHANGE", it triggers a MAJOR version increment

Here are some examples:

1. `fix(azuredeployer.gbapp): stop graphite breaking when too much pressure applied` 
   This would trigger a PATCH increment (e.g., 1.2.3 to 1.2.4).

2. `feat(core.gbapp): add 'graphiteWidth' option`
   This would trigger a MINOR increment (e.g., 1.2.3 to 1.3.0).

3. ```
   feat(api): remove 'graphiteWidth' option
   BREAKING CHANGE: The graphiteWidth option has been removed.
   ```
   This would trigger a MAJOR increment (e.g., 1.2.3 to 2.0.0) due to the breaking change.

4. `perf(core.gbapp): Improved loop efficiency`
   This wouldn't trigger any version increment, as performance improvements don't typically affect the API.

Other commit types like 'docs', 'style', 'refactor', 'test', 'build', and 'ci' don't typically trigger version increments, as they don't affect the functionality of the package from the user's perspective.

When working on your gbapp, always write clear, descriptive commit messages and use the appropriate commit type. Be especially cautious with breaking changes and clearly document them. Keep your commits atomic - each commit should represent a single logical change.

Remember, the goal of SemVer is to help manage dependencies and provide clear communication about the nature of changes in your gbapp. By following these guidelines, you make it easier for others to use and integrate your gbapp into their projects.

For the complete specification and any updates, always refer to semver.org.    


### Create a new keyword

- 10min. Find the package on npmjs.com;
- 2min.  Perform keywords list update;
- (Optional) 10min. Create a new facade of keywords (Create service file, add reference to package/index.ts, and make a call);
- 20min. Keyword code call and infrastructure to support it.
   

## Tooling

### JavaScript

| Title                                       | URL                                                                                          |
|---------------------------------------------|---------------------------------------------------------------------------------------------------|
| Deep Learning in JavaScript                 | https://deeplearnjs.org/                                                                          |
| 3D Physics Engine for JavaScript            | Oimo.js http://lo-th.github.io/Oimo.js/#stacking                                                 |
| Sequence Diagram Generator                  | js-sequence-diagrams: https://bramp.github.io/js-sequence-diagrams/                               |
| Data Visualization with D3.js               | http://blog.avenuecode.com/a-library-for-data-visualization-d3.js                                 |
| Chrome inside Node.js                       | https://github.com/GoogleChrome/puppeteer                                                         |
| XLSX loader                                 | https://github.com/mgcrea/node-xlsx                                                               |
| API Repository                              | https://any-api.com/                                                                              |
| ORM                                         | https://sequelize.org/                                                                            |
| Simplified JavaScript Jargon                | http://jargon.js.org                                                                              |
| RegExp Testing and Debugging                | https://regexp101.com                                                                             |


### Node Packages

| Title                                        | Description                                                                    |
|----------------------------------------------|--------------------------------------------------------------------------------|
| @azure/arm-appservice | Azure SDK for JavaScript to manage App Service resources |
| @azure/arm-cognitiveservices | Azure SDK for Cognitive Services management |
| @azure/arm-resources | Azure SDK for resource management |
| @azure/arm-search | Azure SDK for managing Azure Search services |
| @azure/arm-sql | Azure SDK for SQL database management |
| @azure/arm-subscriptions | Azure SDK for subscription management |
| @azure/cognitiveservices-computervision | Azure Computer Vision API client library |
| @azure/keyvault-keys | Azure Key Vault keys client library |
| @azure/ms-rest-js | Isomorphic client runtime for Azure SDK |
| @azure/msal-node | Microsoft Authentication Library (MSAL) for Node.js |
| @azure/search-documents | Azure Cognitive Search client library |
| @google-cloud/pubsub | Google Cloud Pub/Sub client library |
| @google-cloud/translate | Google Cloud Translation API client library |
| @hubspot/api-client | HubSpot API client for Node.js |
| @microsoft/microsoft-graph-client | Microsoft Graph API client library |
| @nosferatu500/textract | Text extraction from various file formats |
| @semantic-release/changelog | Semantic-release plugin to create or update a changelog file |
| @semantic-release/exec | Semantic-release plugin to execute custom shell commands |
| @semantic-release/git | Semantic-release plugin to commit release assets to the project's git repository |
| @sendgrid/mail | SendGrid email service client library |
| @types/node | TypeScript definitions for Node.js |
| @types/validator | TypeScript definitions for validator.js |
| adm-zip | ZIP file management library |
| alasql | JavaScript SQL database for browser and Node.js |
| any-shell-escape | Escapes a string for use in shell commands |
| async-promises | Utilities for working with asynchronous code and promises |
| basic-auth | Basic HTTP authentication parsing |
| billboard.js | Re-usable, easy interface JavaScript chart library |
| bluebird | Promise library with performance focus |
| body-parser | Node.js body parsing middleware |
| botbuilder | Bot Framework v4 SDK for Node.js |
| botbuilder-adapter-facebook | Bot Framework v4 adapter for Facebook |
| botbuilder-ai | Bot Framework v4 AI integration |
| botbuilder-dialogs | Bot Framework v4 dialogs library |
| botframework-connector | Bot Framework connector library |
| botlib | Library for building chatbots |
| c3-chart-maker | Wrapper for C3.js charting library |
| chatgpt | Unofficial ChatGPT API client |
| chrome-remote-interface | Chrome Debugging Protocol interface |
| cli-progress | Easy to use Progress-Bar for command-line interfaces |
| cli-spinner | Spinner for command-line interfaces |
| core-js | Modular standard library for JavaScript |
| data-forge | Data transformation and analysis library |
| date-diff | Calculate the difference between two dates |
| docxtemplater | Template-based document generation |
| dotenv-extended | Advanced environment variable loader |
| exceljs | Excel workbook manager |
| express | Fast, unopinionated, minimalist web framework for Node.js |
| express-remove-route | Dynamically remove routes in Express |
| ffmpeg-static | FFmpeg static binaries for Node.js |
| google-libphonenumber | Google's libphonenumber library for Node.js |
| googleapis | Google APIs client library |
| ibm-watson | IBM Watson APIs Node.js SDK |
| indent.js | JavaScript code indentation library |
| js-beautify | JavaScript beautifier |
| keyv | Simple key-value storage with support for multiple backends |
| koa | Next generation web framework for Node.js |
| koa-body | Body parser for Koa |
| koa-router | Router middleware for Koa |
| lodash | Utility library delivering modularity, performance, & extras |
| luxon | Library for working with dates and times |
| mammoth | Convert Word documents (.docx files) to HTML |
| moment | Parse, validate, manipulate, and display dates in JavaScript |
| ms-rest-azure | Azure REST API client runtime |
| nexmo | Vonage API client library |
| node-cron | Cron-like job scheduler for Node.js |
| node-nlp | Natural language processing tools for Node.js |
| node-tesseract-ocr | Tesseract OCR engine for Node.js |
| npm | Node package manager |
| open | Open stuff like URLs, files, executables |
| pdf-extraction | Extract content from PDF files |
| pdfkit | PDF document generation library |
| phone | Phone number parsing, validation and formatting |
| pizzip | ZIP file generation library |
| pptxtemplater | PowerPoint template engine |
| pragmatismo-io-framework | Framework for building enterprise applications |
| prism-media | Interface for streaming media transcoding |
| public-ip | Get your public IP address |
| punycode | Robust Punycode converter |
| puppeteer | Headless Chrome Node.js API |
| puppeteer-extra | Modular plugin framework for Puppeteer |
| puppeteer-extra-plugin-stealth | Stealth plugin for Puppeteer |
| qrcode | QR code generator |
| qrcode-terminal | QR code generator for terminal |
| readline | readline utility for Node.js |
| reflect-metadata | Polyfill for Metadata Reflection API |
| rimraf | The UNIX command rm -rf for Node.js |
| safe-buffer | Safer Node.js Buffer API |
| scanf | C-like scanf for Node.js |
| sequelize | Promise-based ORM for Node.js |
| sequelize-cli | Sequelize command line interface |
| sequelize-typescript | Decorators and TypeScript for Sequelize |
| simple-git | Simple Git interface for Node.js |
| speakingurl | Generate a slug from a string |
| ssr-for-bots | Server-side rendering for bots |
| strict-password-generator | Generate cryptographically strong passwords |
| swagger-client | Swagger/OpenAPI client for JavaScript |
| tabulator-tables | Interactive table generation library |
| tedious | TDS driver for connecting to SQL Server databases |
| textract | Text extraction from various file types |
| twitter-api-v2 | Twitter API v2 client library |
| typescript | TypeScript language |
| typescript-rest-rpc | TypeScript RPC framework |
| url-join | Join all arguments together and normalize the resulting URL |
| vbscript-to-typescript | Convert VBScript to TypeScript |
| vhost | Virtual host for Node.js |
| vm2 | Sandbox for Node.js |
| vm2-process | Process management for VM2 |
| walk-promise | Directory tree walker with Promises |
| washyourmouthoutwithsoap | Profanity filter |
| whatsapp-web.js | WhatsApp Web API for Node.js |
| winston | Multi-transport async logging library |
| winston-logs-display | Display Winston logs in the browser |
| yarn | Fast, reliable, and secure dependency management |

### Node Packages (Dev Dependencies)

| Title                                        | Description                                                                    |
|----------------------------------------------|--------------------------------------------------------------------------------|
| simple-commit-message | Simple commit message validator |
| @types/url-join | TypeScript definitions for url-join |
| ban-sensitive-files | Prevent sensitive files from being committed |
| commitizen | Tool to create commit messages according to conventions |
| cz-conventional-changelog | Commitizen adapter for conventional changelog |
| dependency-check | Check for unused and missing dependencies |
| git-issues | List git issues from command line |
| license-checker | Check license info for project dependencies |
| ngrok | Secure tunnels to localhost |
| prettier-standard | Prettier and standard configuration |
| semantic-release | Automated version management and package publishing |
| travis-deploy-once | Run a deployment script only once in Travis CI |
| ts-node | TypeScript execution and REPL for Node.js |
| tslint | Linter for TypeScript |
    
    
### Code Extensions

| Title                                        | Description                                                     |
|----------------------------------------------|-----------------------------------------------------------------|
| mbinic.tgit-cmds                             | Set of commands for launching TortoiseGit dialogs               |
| tomashubelbauer.vscode-markdown-table-format | Formats MarkDown tables so that all columns have the same width |
| esbenp.prettier-vscode                       | VS Code plugin for prettier/prettier (wraps at column 80)       |
| mikestead.dotenv                             | .env file support for VS Code                                   |
| abhinavk99.codewall                          | Blocks distracting websites to improve productivity             |
| christian-kohler.npm-intellisense            | Autocompletes npm modules in import statements                  |
| csholmq.excel-to-markdown-table              | Converts Excel data to Markdown tables                          |
| davidanson.vscode-markdownlint               | Markdown linting and style checking for VS Code                 |
| eg2.ts-tslint                                | TypeScript linter for VS Code                                   |
| eg2.vscode-npm-script                        | Run npm scripts from the command palette                        |
| esbenp.prettier-vscode                       | Code formatter using prettier                                   |
| formulahendry.auto-rename-tag-               | Automatically rename paired HTML/XML tags                       |
| gruntfuggly.align-mode                       | Aligns text in columns based on regular expressions             |
| jmfirth.vsc-space-block-jumper               | Jump between blocks of code separated by blank lines            |
| kaiwood.indentation-level-movement           | Move lines up and down respecting indentation                   |
| mbinic.tgit-cmds                             | Set of commands for launching TortoiseGit dialogs               |
| mechatroner.rainbow-csv                      | Highlight CSV and TSV files in different colors                 |
| mikestead.dotenv                             | .env file support for VS Code                                   |
| sirtori.indenticator                         | Highlights the current indentation depth                        |
| tandy.color-basic                            | Syntax highlighting for Color BASIC                             |


### Code Shotcut keys

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

### Common tasks

| Task          | Description                         |
|---------------|-------------------------------------|
| npm update -g | Updates NPM                         |
| node -v       | Checks node version                 |
| ncu -a        | Update all packages in package.json |

