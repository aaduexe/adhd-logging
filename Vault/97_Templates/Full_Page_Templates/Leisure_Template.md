---
RecordDate: <% tp.file.creation_date("YYYY-MM-DD") %>
tags:
  - genre
Status: to_do
info: 
Leisure: 
Rating: 
Object:
  - Leisure
Cover:
---
> [!example] Progress
> ```dataview
> TASK
> WHERE icontains(text, this.file.name)
> AND !contains(text, "#log/extract")
> GROUP by file.name as reference
> SORT reference DESC

---
# Misc.
<%tp.file.cursor()%>

---
>[!abstract] Ideas
>```dataview
>LIST aliases
>WHERE icontains(Parent, this.file.link)  AND icontains(Object, "Idea")

---
>[!notes]- Reflection & Notes
>```dataview
>TASK
>WHERE icontains(text, "#log/extract")
>AND (icontains(text, this.file.name) OR any(this.file.inlinks, (x) => contains(outlinks, x)))
>GROUP by file.name
>SORT file.name DESC

