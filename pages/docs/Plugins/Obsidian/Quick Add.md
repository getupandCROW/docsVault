---
type: plugin
---
# Quick Add
## Getting started

The first thing you'll want to do is add a new choice. A choice can be one of four types.

-   [Template Choice](https://github.com/chhoumann/quickadd/blob/master/docs/Choices/TemplateChoice.md) - A powerful way to insert templates into your vault.
-   [Capture Choice](https://github.com/chhoumann/quickadd/blob/master/docs/Choices/CaptureChoice.md) - Quick capture anything, anywhere.
-   [Macro Choice](https://github.com/chhoumann/quickadd/blob/master/docs/Choices/MacroChoice.md) - Macros to augment your workflow. Do more, faster.
-   [Multi Choice](https://github.com/chhoumann/quickadd/blob/master/docs/Choices/MultiChoice.md) - Organize your choices in folders.

In your choices, you can use [format syntax](https://github.com/chhoumann/quickadd/blob/master/docs/FormatSyntax.md), which is similar to the Obsidian template syntax.

- You could, for example, use `{{DATE}}` to get the current date.

### Take a look at some examples...

-   [Capture: Add Journal Entry](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Capture_AddJournalEntry.md)
-   [Macro: Log book to daily journal](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Macro_LogBookToDailyJournal.md)
-   [Template: Add an Inbox Item](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Template_AddAnInboxItem.md)
-   [Macro: Move all notes with a tag to a certain folder](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Macro_MoveNotesWithATagToAFolder.md)
-   [Template: Automatically create a new book note with notes & highlights from Readwise](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Template_AutomaticBookNotesFromReadwise.md)
-   [Capture: Add a task to a Kanban board](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Capture_AddTaskToKanbanBoard.md)
-   [Macro: Easily change properties in your daily note (requires MetaEdit)](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Macro_ChangePropertyInDailyNotes.md)
-   [Capture: Fetch tasks from Todoist and capture to a file](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Capture_FetchTasksFromTodoist.md)
-   [Macro: Zettelizer - easily create new notes from headings while keeping the contents in the file](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Macro_Zettelizer.md)
-   [Macro: Obsidian Map View plugin helper - insert location from address](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Macro_AddLocationLongLatFromAddress.md)
-   [Macro: Toggl Manager - set preset Toggl Track time entries and start them from Obsidian](https://github.com/chhoumann/quickadd/blob/master/docs/Examples/Macro_TogglManager.md)
-   [How I Read Research Papers with Obsidian and Zotero](https://bagerbach.com/blog/how-i-read-research-papers-with-obsidian-and-zotero/)
-   [How I Import Literature Notes into Obsidian](https://bagerbach.com/blog/how-i-import-literature-notes-into-obsidian/)

## Format Syntax

Template | Description
------- | -------
`{{DATE}}` | Outputs the current date in `YYYY-MM-DD` format. You could write `{{DATE+3}}` to offset the date with 3 days. You can use `+-3` to offset with `-3` days.
`{{DATE:<DATEFORMAT>}}` | Replace `<DATEFORMAT>` with a [Moment.js date format](https://momentjs.com/docs/#/displaying/format/). You could write `{{DATE<DATEFORMAT>+3}}` to offset the date with 3 days.
`{{VDATE:<variable name>, <date format>}}` | You'll get prompted to enter a date and it'll be parsed to the given date format. You could write 'today' or 'in two weeks' and it'll give you the date for that. Works like variables, so you can use the date in multiple places. **REQUIRES THE NATURAL LANGUAGE DATES PLUGIN!**
`{{VALUE}}` or `{{NAME}}` | Interchangeable. Represents the value given in an input prompt. If text is selected in the current editor, it will be used as the value.
`{{VALUE:<variable name>` | You can now use variable names in values. They'll get saved and inserted just like values, but the difference is that you can have as many of them as you want. Use comma separation to get a suggester rather than a prompt.
`{{LINKCURRENT}}` | A link to the file from which the template is activated from. `[[link]]` format.
`{{MACRO:<MACRONAME>}}` | Execute a macro and get the write the return value here.
`{{TEMPLATE:<TEMPLATEPATH>}}` | Include templates in your `format`. Supports Templater syntax.
`{{MVALUE}}` | Math modal for writing LaTeX. Use CTRL + Enter to submit.

***

## [QuickAdd API](https://github.com/chhoumann/quickadd/blob/master/docs/QuickAddAPI.md)

### `inputPrompt(header: string, placeholder?: string, value?: string): string`

- **Opens** a prompt that asks for an input. 
- **Returns** a string with the input.
- *This function is asynchronous*. You should `await` it.

### `yesNoPrompt(header: string, text?: string): boolean`

- **Opens** a prompt asking for confirmation. 
- **Returns** `true` or `false` based on answer.
- *This function is asynchronous*. You should `await` it.

### `suggester(displayItems: string[] | ((value: string, index?: number, arr?: string[]) => string[]), actualItems: string[])`

- **Opens** a suggester. Displays the `displayItems`, but you map these to other values with `actualItems`.
- The `displayItems` can either be an array of strings, or a map function that will be executed on the actual items.

This means that the following syntax is possible:

```js quickadd
const pickedFile = await params.quickAddApi.suggester(
    (file) => file.basename,
    params.app.vault.getMarkdownFiles()
);
```

- **Returns** the selected value.
- *This function is asynchronous*. You should `await` it.

### `checkboxPrompt(items: string[], selectedItems: string[])`

- **Opens** a checkbox prompt with the items given. Items in the `selectedItems` array will be selected by default.
- **Returns** an array of the selected items.
- *This function is asynchronous*. You should `await` it.

### `executeChoice(choiceName: string, variables?: {[key: string]: any})`

- **Executes** choice with the given name.
- You can also pass an optional parameter, `variables`.
- The object will be read as variables for the choice to be executed. These variables do _not_ affect the currently set variables. You should view the execution as a new branch, separate from the one executing the macro.
- *This function is asynchronous*. You should `await` it.

### [Utility Module](https://github.com/chhoumann/quickadd/blob/master/docs/QuickAddAPI.md#utility-module)

#### `getClipboard()`

- **Returns** the contents of your clipboard.
- *This function is asynchronous*. You should `await` it.
- Syntax: `await quickAddApi.utility.getClipboard();`

#### `setClipboard(text: string)`

- **Sets** the contents of your clipboard to the given input.
- *This function is asynchronous*. You should `await` it.
- Syntax: `await quickAddApi.utility.setClipboard();`

### [Date Module](https://github.com/chhoumann/quickadd/blob/master/docs/QuickAddAPI.md#date-module)

> Output format always defaults to `YYYY-MM-DD`.

#### `now(format?: string, offset?: number)`

- Gets the current time and formats according to the given format.
- Providing an offset will offset the date by number of days. Giving -1 would mean yesterday, and giving 1 would mean tomorrow.

##### `tomorrow(format?: string)`

- Same as `now` but with offset set to 1.

##### `yesterday(format?: string)`

- Again, same as `now` but with offset set to -1.

***

## [Inline scripts](https://github.com/chhoumann/quickadd/blob/master/docs/InlineScripts.md)

QuickAdd supports the usage of inline scripts in [Template choices] and [Capture choices].
- Inline scripts allow you to execute any JavaScript code you want.

You are given the QuickAdd API, just as with user scripts. In inline scripts, it is passed in as `this`, as can be seen in the example below.

```js quickadd
const input = await this.quickAddApi.inputPrompt("✍");
return `Input given: ${input}`;
```

- When you are making an inline script, remember to write `js quickadd` and not just `js` when denoting the language - otherwise you're just inserting a code snippet.
- If you want to insert something, simply `return` it. The return type **must** be a string

***

## [Capture](https://github.com/chhoumann/quickadd/blob/master/docs/Choices/CaptureChoice.md)

- _Capture To_ is the name of the file you are capturing to. You can choose to either enable _Capture to active file_, or you can enter a file name in the _File Name_ input field.

This field also supports the format syntax, which allows you to use dynamic file names. I have one for my daily journal with the name `bins/daily/{{DATE:gggg-MM-DD - ddd MMM D}}.md`. This automatically finds the file for the day, and whatever I enter will be captured to it.

-   _Create file if it doesn't exist_ will do as the name implies - you can also create the file from a template, if you specify the template (the input box will appear below the setting).
-   _Prepend_ will put whatever you enter at the bottom of the file.
-   _Task_ will format it as a task.
-   _Append link_ will append a link to the file you have open in the file you're capturing to.
-   _Insert after_ will allow you to insert the text after some line with the specified text. I use this in my journal capture, where I insert after the line `## What did I do today?`.
- _Capture format_ lets you specify the exact format that you want what you're capturing to be inserted as. You can do practically anything here. Think of it as a mini template. See the [format syntax] above on this page for inspiration. In my journal capture, I have it set to `- {{DATE:HH:mm}} {{VALUE}}`. This inserts a bullet point with the time in hour:minute format, followed by whatever I entered in the prompt.

![Quickadd Capture Image 1](https://user-images.githubusercontent.com/29108628/123451366-e025e280-d5dd-11eb-81b6-c21f3ad1823d.png) 

***

## [Macro](https://github.com/chhoumann/quickadd/blob/master/docs/Choices/CaptureChoice.md)

Macros are powerful tools that allow you to execute any sequence of Obsidian commands and user scripts. User scripts are Javascript scripts that you can write to do something in Obsidian. All you need is a Javascript file in your vault, and you can activate it.

- Each _macro choice_ has an associated _macro_. A macro choice allows you to activate a macro from the QuickAdd suggester.

This is what the settings for a _macro choice_ looks like.

![Quickadd Macro Choice Image|800](https://user-images.githubusercontent.com/29108628/121774145-22ccd100-cb81-11eb-8873-7533755bdf32.png)

- Now, you can have any amount of _macros_. You can use the macro manager to... manage them. If you have any macros that you want to run on plugin load - which is often just when you start Obsidian - you can specify that here, too.

This allows you to, for example, create a daily note automatically when you open Obsidian.

![Quickadd Macro Choice Image|800](https://user-images.githubusercontent.com/29108628/121774198-81924a80-cb81-11eb-9f80-9816263e4b6f.png)

This is what my `logBook` macro looks like. It's pretty plain - it just executes one of my user scripts.

![Quickadd Macro Choice Image|800](https://user-images.githubusercontent.com/29108628/121774245-cfa74e00-cb81-11eb-9977-3ddac04dc8bd.png)

- The `logBook` user script simply updates the book in my daily page to something I specify in a prompt. 

Here it is - with some comments that explain the code. [How-to-install guide](https://github.com/chhoumann/quickadd/issues/15#issuecomment-864553251).

```js quickadd
// You have to export the function you wish to run.
// QuickAdd automatically passes a parameter, which is an object with the Obsidian app object
// and the QuickAdd API (see description further on this page).
module.exports = async (params) => {
// Object destructuring. We pull inputPrompt out of the QuickAdd API in params.
    const {quickAddApi: {inputPrompt}} = params;
// Here, I pull in the update function from the MetaEdit API.
    const {update} = app.plugins.plugins["metaedit"].api;
// This opens a prompt with the header "📖 Book Name". val will be whatever you enter.
    const val = await inputPrompt("📖 Book Name");
// This gets the current date in the specified format.
    const date = window.moment().format("gggg-MM-DD - ddd MMM D");
// Invoke the MetaEdit update function on the Book property in my daily journal note.
// It updates the value of Book to the value entered (val).
    await update('Book', val, `bins/daily/${date}.md`)
}
```

Any function executed by QuickAdd will be passed an object as the first (and only) parameter. The object contains

-   A reference to the Obsidian `app`.
-   A reference to the QuickAddApi - which allows you to use the functions below.
-   A reference to `variables`, an object which, if you assign values to it, you can use in your format syntax.

Let's talk a bit more about `variables`. If you assign a value to a key in `variables`, you can access that variable by its key name. This can be accessed both in subsequent macros, and the format syntax `{{VALUE:<variable name>}}`.

For example, say you assign `myVar` to `variables`. Then you can access the value of `myVar` in subsequent macros, as well as through the format syntax`{{VALUE:myVar}}`. You can also access it through `<parametername>.variables["myVar"]`.

```js quickadd
// MACRO 1
module.exports = (params) => {
    params.variables["myVar"] = "test";
}
```
```js quickadd
// MACRO 2
module.exports = (params) => {
    console.log(params.variables["myVar"]);
}
```

- You can use variables to pass parameters between user scripts.

- In your user scripts for your macros, you can have use `module.exports` to export a function, which will be executed as expected.

- You can, however, export much more than functions. You can also export variables - and more functions!

```js quickadd
// Macro called 'MyMacro'
module.exports = {
    myVar: "test",
    plus: (params) => params.variables["a"] + params.variables["b"],
    start
}

async function start(params) {
    params.app.vault.doSomething();
    const input = await params.quickAddApi.suggester(["DisplayValue1", "DisplayValue2", "DisplayValue3"], ["ActualValue1", "ActualValue2", "ActualValue3"]);
    return input;
}
```

- If you select the macro that contains a user script with the above code, you'll be prompted to choose between one of the three exported items.

- However, if you want to skip that, you can access nested members using this syntax: `{{MACRO:MyMacro::Start}}`. This will just instantly execute `start`.

***

## [Multi](https://github.com/chhoumann/quickadd/blob/master/docs/Choices/CaptureChoice.md)

Multi-choices are pretty simple. They're like folders for other choices. Here are mine. They're the ones which you can 'open' and 'close'.

![Quickadd Multi Choice Image|800](https://user-images.githubusercontent.com/29108628/121774481-e39f7f80-cb82-11eb-92bf-6d265529ba06.png)

***

## [Template](https://github.com/chhoumann/quickadd/blob/master/docs/Choices/CaptureChoice.md)

The template choice type is not meant to be a replacement for Templater or core Templates. It's meant to augment them. You can use both QuickAdd format syntax in a Templater template - and both will work. That's one thing. But there's also all the other options: dynamic template names, adding to folders, appending links, incrementing file names, opening the file when it's created (or not), etc.

- You first need to specify a _template path_. This is a path to the template you wish to insert.

###### The remaining settings are useful, but optional. 

You can specify a format for the file name, which is based on the format syntax - which you can see further down this page. Basically, this allows you to have dynamic file names. If you wrote `{ {{DATE}} {{NAME}}`, it would translate to a file name like `{ 2021-06-12 FileName`, where `FileName` is a value you enter.

You can specify as many folders as you want. If you don't, it'll just create the file in the root directory. If you specify one folder, it'll create the file in there. If you specify multiple folders, you'll be asked which folder you wish to create the file in when you are creating it.

- _Append link_ appends a link to the created file in the file you're currently in.
- _Increment file name_ will, if a file with that name already exists, increment the file name. So if a file called `untitled` already exists, the new file will be called `untitled1`.
- _Open_ will open the file you've created. By default, it opens in the active pane. If you enable _New tab_, it'll open in a new tab in the direction you specified. 

![Quickadd Template Choice Image|800](https://user-images.githubusercontent.com/29108628/121773888-3f680980-cb7f-11eb-919b-97d56ef9268e.png)

***

## Example - [Open QuickAdd from your Desktop](https://github.com/chhoumann/quickadd/blob/master/docs/AHK_OpenQuickAddFromDesktop.md) 

This is an [[AutoHotkey]] script which unminimizes/focuses Obsidian and sends some keypresses to it.

I've bound this to my QuickAdd activation hotkey, so this script automatically brings Obsidian to the front of my screen with QuickAdd open.

```autohotkey
#SingleInstance, Force
SendMode Input
SetWorkingDir, %A_ScriptDir%
SetTitleMatchMode, RegEx

!^+g::
    WinActivate, i) Obsidian
    ControlSend,, {CtrlDown}{AltDown}{ShiftDown}G{CtrlUp}{CtrlUp}{ShiftUp}, i)Obsidian
Return
```

- I'm using `CTRL+SHIFT+ALT+G` as my shortcut, both in Obsidian and for the AHK script to activate. 
- I use a keyboard shortcut to send those keys *(lol, I know - but it's to avoid potential conflicts)*. Here's a guide to what the `!^+` mean, and how you can customize it: [AutoHotkey Docs](https://www.autohotkey.com/docs/Hotkeys.htm)

#### Update

If you are willing to install the [[Obsidian Advanced URI]] plugin, this script is much easier for you to use.

```autohotkey
SendMode Input
SetWorkingDir, %A_ScriptDir%
SetTitleMatchMode, RegEx

!^+g::
    WinActivate, i) Obsidian

    Run "obsidian://advanced-uri?vault=<YOUR_VAULT_NAME>&commandname=QuickAdd: Run QuickAdd"
Return
```

- Simply replace `<YOUR_VAULT_NAME>` with the name of your vault.
- **This version is more reliable**, as the other one can fail to activate occasionally.
- It uses the same hotkey to activate as above (`CTRL+SHIFT+ALT+G`). If you wish to change it:

>  `!` means `Alt`
> `^` means `Ctrl`
>  `+` means `Shift`

- You can replace the `!^+g` with any hotkey of your choosing.