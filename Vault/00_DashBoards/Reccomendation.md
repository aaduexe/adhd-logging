---
aliases:
  - Choose next leisure
  - What to consume next
  - what to read
  - what to watch
Object: DashBoard
---
# Movie
```dataview
TASK
WHERE contains(tags, "#fleeting/muse/recommendation/movie")
AND !completed
```
# Series
```dataview
TASK
WHERE contains(tags, "#fleeting/muse/recommendation/series")
AND !completed
```
## Animated
```dataview
TASK
WHERE !completed AND (contains(tags, "#fleeting/muse/recommendation/series/cartoon") OR contains(tags, "#fleeting/muse/recommendation/series/anime"))
```
