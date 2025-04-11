---
RecordDate: <% tp.file.creation_date("YYYY-MM-DD") %>
Deadline: 
IntendedResult:
  - Trip & Tour
Status: active
Collaborator: 
Parent:
  - "[[Travel]]"
Child: 
Object:
  - Project
---
>[!abstract] Trip Members.
>[[Aadu|Me]]: As I'm the host. Otherwise why would I need this?

---
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

