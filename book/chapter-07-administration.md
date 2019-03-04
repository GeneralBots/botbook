# General Bots Administration

## Commands

General Bot can be controlled by the same chat window people talk to, so
here is a list of admin commands related to deploying .gb* files.

| Command         | Description                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------|
| deployPackage   | Deploy a KB package. Usage **deployPackage** [package-name]. Then, you need to run rebuildIndex.                |
| undeployPackage | Undeploy a KB. Usage **undeployPackage** [package-name].                                                        |
| redeployPackage | Undeploy and then deploys the KB. Usage **redeployPackage** [package-name]. Then, you need to run rebuildIndex. |
| setupSecurity   | Setup connection to user directories.                                                                           |

Discontinued commands:

| Command      | Description                                                                               | Reason                         |
|--------------|-------------------------------------------------------------------------------------------|--------------------------------|
| rebuildIndex | Rebuild Azure Search indexes, must be run after **deployPackage** or **redeployPackage**. | Now it is called automatically |

## How to

### Move to production (Azure)

* Update bot endpoint;

## Bot Analytics

## Cloud Internals