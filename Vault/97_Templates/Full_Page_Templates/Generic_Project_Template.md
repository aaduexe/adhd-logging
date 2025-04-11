---
RecordDate: <% tp.file.creation_date("YYYY-MM-DD") %>
Deadline: 
IntendedResult: 
Status: to_do
Collaborator: 
info: 
Parent: 
Child: 
Object:
  - Project
---
>[!rsrc]  Related Notes
>```dataview
>TABLE Object
>FROM !"03_Project" and !"01_DailyNotes"
>WHERE (contains(file.outlinks, this.file.link) 
>OR any(this.Parent, (x) => contains(Parent, x))) AND !contains(Object, "Project")

> [!example] Logs
> ```dataview
> TASK
>WHERE contains(text, "#log/sprint" )
>AND (contains(text, this.file.name)
>OR any(this.file.inlinks, (x) => contains(outlinks, x)))
>GROUP by file.name as fileName
>SORT fileName DESC

# Tasks

>[!question] Open
>```dataview
>TASK
>WHERE !completed
>AND (contains(text, "#task") or contains(text, "#question"))
>AND (contains(text, this.file.name) OR any(this.file.inlinks, (x) => contains(outlinks, x)))

>[!success] Closed
>```dataview
>TASK
>WHERE completed
>AND (contains(text, "#task") or contains(text, "#question"))
>AND (contains(text, this.file.name) OR any(this.file.inlinks, (x) => contains(outlinks, x)))

