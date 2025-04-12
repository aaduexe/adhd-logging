---
Object: DashBoard
---
```dataviewjs
const basedata = Object.entries(dv.app.metadataCache.unresolvedLinks)
      .filter(([origin, unresolved]) =>
              Object.keys(unresolved).length)

// Build dictionary (or set) with key on the new file
let unresolvedDict = {}
for (let [origin, unresolvedList] of basedata) {
   for (let newFile in unresolvedList) {
      // If first time we see this, create an array...
      if (!unresolvedDict[newFile]) 
        unresolvedDict[newFile] =  []

      // Push another origin into the array
      unresolvedDict[newFile].push(dv.fileLink(origin))
   }
}

dv.table(["Unresolved", "Origin(s)"],
   Object.entries(unresolvedDict)
   .sort((a, b) => (a[0].toLowerCase() < b[0].toLowerCase() ? -1 : 1))
   .map(item => [dv.fileLink(item[0]), item[1]])
  )
```
