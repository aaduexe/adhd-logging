---
Object: Dashboard
---
```dataview
TASK
FROM !"97_Templates" and !"99_Archive"
WHERE !completed
AND icontains(text, "#task") AND !contains(text, "#tdsync")
SORT due DESC
```
