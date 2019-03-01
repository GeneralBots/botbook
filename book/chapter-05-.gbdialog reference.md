# .gbdialog Reference

## Using Conversational BASIC

## General Bots BASIC reference

| Instruction                      | Description                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| hear *variable*                  | Hears something from the person into a *variable* for later use.            |
| talk *message*                   | Talk the specified *message* to the person.                                 |
| generate a password              | Creates a new password into the system variable **password** for later use. |
| create a bot farm using *params* | Deploys a new bot farm to the cloud.                                        |
| wait *seconds*                   | Wait a number of seconds before continuing the conversation.                |

## How To

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
