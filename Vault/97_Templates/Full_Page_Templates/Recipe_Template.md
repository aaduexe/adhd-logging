---
RecordDate: <% tp.file.creation_date("YYYY-MM-DD") %>
Object:
  - Recipe
Rating: 
Version: 0.0
---
%% Space For Image %%
# Ingredients
- 
# Method
1. 
# Crumbs
> [!cite]- Logs
> ```dataview
> TASK
> WHERE contains(text, this.file.name) AND contains(text, "#log/cooked")
> GROUP BY file.name
> SORT file.name DESC

> [!info]- Change Log
> ```dataview
> TASK
> WHERE contains(text, this.file.name) AND contains(text, "changeLog:")
> GROUP BY file.name
> SORT file.name DESC

# Additional Meta-Data
[reference:: ]
[cuisine:: ]
[author:: ]
[servings:: ]