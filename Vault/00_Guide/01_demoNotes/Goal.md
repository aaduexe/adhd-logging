---
RecordDate: 2025-04-13
Deadline: 
tags: 
Parent: 
Object: Goal
---
%% Delete this comment and setup a tracker if you need to. %%

>[!rsrc]  Related Notes
>```dataview
>TABLE Object
>WHERE !(contains(Object, "Project") OR contains(Object, "DailyNote"))
>AND contains(file.outlinks, this.file.link)

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
> WHERE contains(Object, "Project") AND (contains(Status, "active") and contains(file.outlinks, this.file.link))

> [!warning] Inactive
> ```dataview
> TABLE Deadline, Status
> WHERE !(contains(Status, "active")
> OR contains(Status, "completed"))
> AND contains(file.outlinks, this.file.link)
> AND contains(Object, "Project")

> [!done] Completed
> ```dataview
> TABLE Deadline
> WHERE (contains(Status, "completed") and contains(file.outlinks, this.file.link))
> AND contains(Object, "Project")

