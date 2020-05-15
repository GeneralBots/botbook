# .gbkb Reference

## Media Types

There are several media types that can be used in .gbkb package folder.
The table below shows the description of each one of them:

| Folder   | File description                                                                                   |
|----------|----------------------------------------------------------------------------------------------------|
| tabular  | .csv, .tsv or any tabular file used as an pair of question/answer and an optional hierarchy.       |
| images   | Images that can be used to enrich the answer to the user in the [Projector](glossary.md#projector) |
| videos   | Videos used to answer questions made by users.                                                     |
| subjects | List of images of subjects that can be trated by the bot.                                          |
| articles | Articles in .md that will be presented instead of text-only answers.                               |

## Presenting Answers

## With text

To answer with a text phrase, just type the answer in the Answer column. Whenever the
search engine elects the answer as the next thing to say, the text present in this
column will be talked.

## With an article

A Markdown (.md) file can be used as an answer instead of plain text, so the experience
will be more appealing whenever the channel allow the text to be present that way. The
answer column specifies the .md file to be presented whenever the question is elected
as matching the user intent.

## With a video

To display a video on the projector, just provide the Video URL to the desired question,
instead of specifing an text answer in the column **answer**.
The list of answers is a series of tabular files (.tsv, .csv, etc.) inside the **tabular** directory of the .gbkb.

## With a Script (PREVIEW)

To call a VBA script stored on a .gbdialog, just specify the script file name in a form of `script:<FILENAME>` instead of specifing an text answer in the column **answer**. When someone asks that match the **question**, the script will be invoked and the answer dialog will be started.

## Subject Menu 

### Associating a [Subject Menu Item](glossary.md#subject-menu-item) to a Dialog

To call a dialog just when an answer would provide the desired question, just
use dialog:*dialogName* instead of specifing an text answer.

## How To

### Updating the Bot Knowledge Base (.gbkb folder)

The subjects.json file contains all information related to the subject tree and can be used to build the menu carrousel as well give a set of words to be used as subject catcher in the conversation. A hierarchy can be specified.

### Use Excel for (Hierarchical) Knowledge Base Editing

![General Bots Inside Excel can enable bot production the masses](https://github.com/pragmatismo-io/BotServer/blob/master/docs/images/general-bots-composing-subjects-json-and-excel.gif)
