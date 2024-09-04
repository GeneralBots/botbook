---
sidebar_position: 90
---

# General Bots Feature Matrix

| **Feature Code** | **Code**                                          | **Description**                                                                           | **Category**            | **Status** |
|------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------|-------------------------|------------|
| FEAT-01A         | `HEAR variable`                                   | Hears something from the person into a variable for later use.                            | Basic Interaction       | FUTURE     |
| FEAT-02B         | `TALK message`                                   | Talk the specified message to the person.                                                 | Basic Interaction       | FUTURE     |
| FEAT-03C         | `WAIT seconds`                                   | Wait a number of seconds before continuing the conversation.                              | Basic Interaction       | FUTURE     |
| FEAT-04D         | `confirm variable` (Comming soon)                 | Waits for confirmation and returns true or false.                                         | Basic Interaction       | FUTURE     |
| FEAT-05E         | `HEAR variable AS EMAIL`                         | Hears and validates an email address from the user.                                        | Data Validation         | FUTURE     |
| FEAT-06F         | `HEAR variable AS DATE`                          | Hears and validates a date from the user.                                                 | Data Validation         | FUTURE     |
| FEAT-07G         | `HEAR variable AS NAME`                          | Hears and validates a name from the user.                                                 | Data Validation         | FUTURE     |
| FEAT-08H         | `HEAR variable AS INTEGER`                       | Hears and validates an integer from the user.                                              | Data Validation         | FUTURE     |
| FEAT-09I         | `HEAR variable AS BOOLEAN`                       | Hears and validates a boolean (true/false) from the user.                                 | Data Validation         | FUTURE     |
| FEAT-10J         | `HEAR variable AS HOUR`                          | Hears and validates an hour from the user.                                                 | Data Validation         | FUTURE     |
| FEAT-11K         | `HEAR variable AS MONEY`                         | Hears and validates a monetary amount from the user.                                       | Data Validation         | FUTURE     |
| FEAT-12L         | `HEAR variable AS MOBILE`                        | Hears and validates a mobile number from the user.                                         | Data Validation         | FUTURE     |
| FEAT-13M         | `HEAR variable AS ZIPCODE`                       | Hears and validates a ZIP code from the user.                                              | Data Validation         | FUTURE     |
| FEAT-14N         | `HEAR variable AS "Abacate", "Maçã", "Morango"`  | Displays the specified menu and waits for user selection.                                 | Data Validation         | FUTURE     |
| FEAT-15O         | `HEAR variable AS LANGUAGE`                      | Hears and validates a language code from the user.                                         | Data Validation         | FUTURE     |
| FEAT-16P         | `HEAR variable AS LOGIN (internal)`              | Waits for Active Directory login integration before proceeding.                           | Data Validation         | FUTURE     |
| FEAT-17Q         | `variable = GET "file.xlsx", "A1:A1"`            | Gets the value of the cell specified in range address.                                    | Data Handling           | FUTURE     |
| FEAT-18R         | `SET "file.xlsx", "A1:A1", 42`                   | Sets the value of the cell specified in range address.                                    | Data Handling           | FUTURE     |
| FEAT-19S         | `variable = GET "https://server/query"`          | Gets the value from the specified web service.                                             | Data Handling           | FUTURE     |
| FEAT-20T         | `POST "https://", data`                          | Sends data to the specified URL.                                                           | Data Handling           | FUTURE     |
| FEAT-21U         | `data = FIND "sales_data.xlsx", "A1:B10"`        | Finds data in a specified range or file.                                                   | Data Handling           | FUTURE     |
| FEAT-22V         | `result = SELECT product, SUM(amount) AS total FROM data GROUP BY product` | Use SQL to manipulate a data variable returned from FIND or an array. | Data Handling           | FUTURE     |
| FEAT-23W         | `file = data AS IMAGE`                           | Converts a two-dimensional array into an image file.                                       | Data Handling           | FUTURE     |
| FEAT-24X         | `file = data AS PDF`                             | Converts a two-dimensional array into a PDF file.                                          | Data Handling           | FUTURE     |
| FEAT-25Y         | `data = NEW OBJECT`                              | Creates a new object to be used with REST calls.                                          | Data Handling           | FUTURE     |
| FEAT-26Z         | `data = NEW ARRAY`                               | Creates a new array.                                                                        | Data Handling           | FUTURE     |
| FEAT-27A         | `file = QRCODE "https://example.com"`            | Creates a QR code from specified text.                                                      | Data Handling

| **Feature Code** | **Code**                                          | **Description**                                                                           | **Category**            | **Status** |
|------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------|-------------------------|------------|
| FEAT-27A         | `file = QRCODE "https://example.com"`            | Creates a QR code from specified text.                                                     | Data Handling           | FUTURE     |
| FEAT-28B         | `FORMAT value, format`                           | Formats a value according to the specified format.                                        | Data Handling           | FUTURE     |
| FEAT-29C         | `ADD NOTE`                                       | Adds a note to a file named Notes.xls of .gbdata.                                         | Data Handling           | FUTURE     |
| FEAT-30D         | `ALLOW ROLE`                                     | Check if a role specified in People sheet (.gbdata) will have access.                     | Data Handling           | FUTURE     |
| FEAT-31E         | `page = OPEN url [AS #namedSession]`             | Web automation retrieval of a web page, saving the session for reuse.                     | Web Automation          | FUTURE     |
| FEAT-32F         | `variable = GET page, cssSelector`                | Retrieves an element within an IFRAME specified by selector.                               | Web Automation          | FUTURE     |
| FEAT-33G         | `SET page, cssSelector, value`                    | Defines a field to a value on the webpage specified by selector.                           | Web Automation          | FUTURE     |
| FEAT-34H         | `CLICK page, cssSelector`                        | Clicks on an element inside the web page being automated.                                 | Web Automation          | FUTURE     |
| FEAT-35I         | `file = DOWNLOAD url`                            | Downloads a file from the specified URL.                                                  | Web Automation          | FUTURE     |
| FEAT-36J         | `HEAR variable AS FILE`                           | Returns a file uploaded by the user to be saved.                                          | File Management         | FUTURE     |
| FEAT-37K         | `HEAR variable AS AUDIO`                          | Returns an audio file uploaded by the user to be saved.                                   | File Management         | FUTURE     |
| FEAT-38L         | `INCLUDE file`                                   | Includes a file into .gbdialog.                                                            | File Management         | FUTURE     |
| FEAT-39M         | `UPLOAD file`                                    | Uploads a file to a storage blob, like Azure Storage.                                     | File Management         | FUTURE     |
| FEAT-40N         | `DIR path`                                       | Returns a list of files in the specified directory.                                        | File Management         | FUTURE     |
| FEAT-41O         | `FILL`                                           | Fills data into a Word document to be exported as images.                                 | File Management         | FUTURE     |
| FEAT-42P         | `SAVE variable AS "path/file"`                    | Saves the specified variable as a file at the given path.                                 | File Management         | FUTURE     |
| FEAT-43Q         | `TABLE name ON connection`                       | Defines a TABLE on the specified storage (database) connection.                          | Advanced Operations     | FUTURE     |
| FEAT-44R         | `field AS dataType`                              | Defines a field in TABLE. Eg.: name string(50).                                           | Advanced Operations     | FUTURE     |
| FEAT-45S         | `CONTINUATION TOKEN`                             | Returns the value of the continuation token associated with the current dialog.           | Advanced Operations     | FUTURE     |
| FEAT-46T         | `aadToken()`                                     | Auto-generated variable that contains Azure AD Token useful for calling Microsoft Web Services. | Internal Variables and Functions | FUTURE     |
| FEAT-47U         | `SET PARAM name AS value`                        | Defines a retrievable param in the storage in the scope of the user.                      | Options                 | FUTURE     |
| FEAT-48V         | `GET PARAM name`                                 | Returns a previously user scoped param via SET PARAM from the storage.                    | Options                 | FUTURE     |
| FEAT-49W         | `SET HTTP HEADER _key = value`                    | Defines an HTTP header to be used in the next GET call.                                    | HTTP Authentication     | FUTURE     |
| FEAT-50X         | `SET HTTP USERNAME = value`                       | Defines the HTTP username to be used in the next GET call.                                 | HTTP Authentication     | FUTURE     |
| FEAT-51Y         | `SET HTTP PASSWORD = value`                       | Defines the HTTP password to be used in the next GET call.                                 | HTTP Authentication     | FUTURE     |
| FEAT-52Z         | `SET HEAR ON "mobile"`                            | Sets HEAR options for mobile numbers.                                                      | Options                 | FUTURE     |
| FEAT-53A         | `SET MAX LINES value`                            | Defines the maximum number of lines for output.                                            | Options                 | FUTURE     |
| FEAT-54B         | `SET SCHEDULE "2 * * * * *"`                      | Defines a schedule for periodic tasks.                                                     | Options                 | FUTURE     |
| FEAT-55C         | `SET LANGUAGE value`                             | Sets the language for the dialog.                                                          | Options                 | FUTURE     |
| FEAT-56D         | `SET TRANSLATOR [ON or OFF]`                     | Turns the translator feature on or off.                                                   | Options                 | FUTURE     |
| FEAT-57E         | `SET WHOLE WORD [TRUE or FALSE]`                 | Defines if whole word matching is used.                                                    | Options                 | FUTURE     |
| FEAT-58F         | `SET THEME "dark" or "white" or "blue"`           | Defines the theme for the next content generation (PDF, images, videos, etc.).            | Options                 | FUTURE     |
| FEAT-59G         | `SET OPERATOR [OR]`                              | Defines OR operations on multiple FIND filters separated by comma.                        | Options                 | FUTURE     |
| FEAT-60H         | `SET FILTER TYPE [comma separated list of types]` | Uses the specified type in next FIND calls, disabling auto-detection of filter type.       | Options                 | FUTURE     |
| FEAT-61I         | `SET PAGED "auto" or "none"`                      | Defines auto paging for HTTP REST GET calls.                                               | Options                 | FUTURE     |
| FEAT-A7B         | |  Any files inside public folder of bot .gbdrive will be accessible in /[botId].gbai/[botId].gbdrive/public  ||| Sharing                 | FUTURE     |


AUTO SAVE
.gbdrive public