# .gbdialog Reference
![generalbots-2018](https://user-images.githubusercontent.com/65977273/94922431-949c3900-0490-11eb-800a-6b478d689f2a.png)

 All direct communication from GeneralBots to the end user is made up of the .gbDialog extension. It can be composed of speech or writing directly with the bot.
 This extension facilitates support related to dialogues, as the system is divided by each service extension.
 
## Importance of dialogue services.

Communication or dialogue between the end user is one of the most important services of a software, because the smooth functioning of the dialogue directly reflects the functioning for the user.

## Using Conversational BASIC

The following file types are loaded from a .gbdialog package: `.vbs`, `.vb`, `.basic` and `.bas`.

## General Bots BASIC reference

| Instruction / Usage                                           | Description                                                                 |
| ------------------------------------------------------------- | --------------------------------------------------------------------------- |
| HEAR _variable_                                               | Hears something from the person into a _variable_ for later use.            |
| confirm _variable_ (Comming soon)                             | Waits for confirmation like 'yes', 'y', 'yeah' and return true or false     |
| TALK _message_                                                | Talk the specified _message_ to the person.                                 |
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
| HEAR _variable_ AS INTEGER                                    | |
| HEAR _variable_ AS BOOLEAN                                    | |
| HEAR _variable_ AS HOUR                                       | |
| HEAR _variable_ AS MONEY                                      | |
| HEAR _variable_ AS MOBILE                                     | |
| HEAR _variable_ AS ZIPCODE                                    | |
| HEAR _variable_ AS "Abacate", "Maçã", "Morango"               | Displays the specified menu and waits for this input until user select one of them. | 
| HEAR _variable_ AS LANGUAGE                                   | |
| HEAR _variable_ AS LOGIN (internal)                           | Waits for Active Directoy login integration before proceeding with the dialog .     |
| GO TO [number,] dialogName                                    | Transfers the conversation to a next dialog for the specificed number.              |

## How To

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
