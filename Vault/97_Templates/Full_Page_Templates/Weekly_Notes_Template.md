---
Object: WeekNote
---
# Habit Summary
``` tracker
searchType: dvfield
searchTarget: exercise, diet, WeightUpdate
<%* const moment = window.moment, fileName = tp.file.title, match = fileName.match(/Week-(\d+)-(\d{4})/); if (match) { const weekNumber = parseInt(match[1]), year = parseInt(match[2]), monday = moment().year(year).week(weekNumber).startOf('week').format('YYYY-MM-DD'), sunday = moment().year(year).week(weekNumber).endOf('week').format('YYYY-MM-DD'); tR += `startDate: ${monday}\nendDate: ${sunday}\n`; } else { tR += "Error: File name should be in 'Week-XX-YYYY' format."; } %>
summary:
    template: "🏋🏻‍♀️ Exercise: {{numDaysHavingData(dataset(0))}} day/s. {{sum(dataset(0))}} minutes (approx).\n⚖ Average Weight: {{average(dataset(2))}} kg"
```
# Sprinted On
```dataviewjs
const thisWeek = dv.current().file.name.split("-");
let DailyPages = dv.pages('"01_DailyNotes"')

let relatedPages = DailyPages.where(p => dv.parse(p.file.name).weekNumber.toString() === thisWeek[1] && dv.parse(p.file.name).year.toString() === thisWeek[2])

let logs = relatedPages.file.tasks.where(t => t.tags.includes('#log/sprint'))
let outlinks = logs.outlinks
let projects = Array.from(new Set(outlinks.map(t => t.path)))
for (let link of projects){
	dv.paragraph(`🧶[[${link}]]`)
}
```
# Dailies
```dataview
TABLE WITHOUT ID file.link as "Date", Dailies as "Logs"
FROM "01_DailyNotes"
WHERE "Week" + dateformat(date(file.name),"-W-yyyy") = this.file.name
AND Dailies
```
>[!rsrc] MISC.
>```dataview
TASK
FROM "01_DailyNotes"
WHERE "Week" + dateformat(date(file.name),"-W-yyyy") = this.file.name
AND (
icontains(text, "#fleeting") OR
icontains(text, "#wishlist")
)