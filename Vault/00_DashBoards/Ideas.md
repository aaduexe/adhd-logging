---
Object: DashBoard
---
> [!error] Fleeting Ideas
> ```dataview
> TASK
> FROM !"97_Templates"
> WHERE contains(text, "#fleeting/idea") and !completed
> GROUP BY file.name
> SORT file.name DESC
