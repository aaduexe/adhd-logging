---
RecordDate: 2025-04-13
tags:
  - "#genre/action"
Status: read
info: 
Leisure: Book
Rating: ⭐
Object: Leisure
Cover: You can paste the image link here, and plugins like Dashboard visualize your library nicely
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

