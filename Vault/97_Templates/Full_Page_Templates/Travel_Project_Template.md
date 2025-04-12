---
RecordDate: <% tp.file.creation_date("YYYY-MM-DD") %>
Deadline: 
IntendedResult:
  - Trip & Tour
Status: active
Collaborator: 
Parent:
  - "[[Travel]]"
Object: Project
---
>[!abstract] Trip Members.
>[[Your Name|Me]]: 

---
>[!rsrc]  Related Notes
>```dataview
>TABLE Object
>FROM !"01_DailyNotes"
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

