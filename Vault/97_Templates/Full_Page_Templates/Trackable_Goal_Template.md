---
RecordDate: <% tp.file.creation_date("YYYY-MM-DD") %>
Deadline: 
tags: 
Parent: 
Child: 
Object:
  - Goal
---
%% Delete this comment and setup a tracker if you need to. %%

>[!rsrc]  Related Notes
>```dataview
>TABLE Object
>FROM !"03_Project" and !"01_DailyNotes"
>WHERE contains(file.outlinks, this.file.link)

> [!example] Logs
> ```dataview
> TASK
>WHERE contains(text, "#log/sprint" )
>AND contains(text, this.file.name)
>OR any(this.file.inlinks, (x) => contains(outlinks, x))
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

# Projects

> [!atom] Active
> ```dataview
> TABLE Deadline
> FROM "03_Projects"
> WHERE contains(Status, "active") and contains(file.outlinks, this.file.link)

> [!warning] Inactive
> ```dataview
> TABLE Deadline, Status
> FROM "03_Projects"
> WHERE !(contains(Status, "active")
> OR contains(Status, "completed"))
> AND contains(file.outlinks, this.file.link)

> [!done] Completed
> ```dataview
> TABLE Deadline
> FROM "03_Projects"
> WHERE contains(Status, "completed") and contains(file.outlinks, this.file.link)