---
type: plugin
---

# Templater
[Docs - Introduction - Templater](moz-extension://b81adc6a-b791-4a8a-8eee-e4e78e7fe7fe/_generated_background_page.html)
[Templater Showcase - GitHub](https://github.com/SilentVoid13/Templater/discussions/categories/templates-showcase)

## File Commands 

- File content: <% tp.file.content %>

- File creation date: <% tp.file.creation_date() %>
- File creation date with format: <% tp.file.creation_date("dddd Do MMMM YYYY HH:mm") %>

- File creation: [[<% (await tp.file.create_new("MyFileContent", "MyFilename")).basename %>]]

- File cursor: <% tp.file.cursor(1) %>

- File cursor append: <% tp.file.cursor_append("Some text") %>
    
- File existence: <% tp.file.exists("MyFile") %>

- File find TFile: <% tp.file.find_tfile("MyFile").basename %>
    
- File Folder: <% tp.file.folder() %>
- File Folder with relative path: <% tp.file.folder(true) %>

- File Include: <% tp.file.include("[[Template1]]") %>

- File Last Modif Date: <% tp.file.last_modified_date() %>
- File Last Modif Date with format: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm") %>

- File Move: <% await tp.file.move("/A/B/" + tp.file.title) %>
- File Move + Rename: <% await tp.file.move("/A/B/NewTitle") %>

- File Path: <% tp.file.path() %>
- File Path with relative path: <% tp.file.path(true) %>

- File Rename: <% await tp.file.rename("MyNewName") %>
- Append a "2": <% await tp.file.rename(tp.file.title + "2") %>

- File Selection: <% tp.file.selection() %>

- File tags: <% tp.file.tags %>

- File title: <% tp.file.title %>
- Strip the Zettelkasten ID of title (if space separated): <% tp.file.title.split(" ")[1] %>