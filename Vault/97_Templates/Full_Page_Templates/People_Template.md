---
tags: 
aliases: 
Object: Noun
---

%%Replace this comment with an Image%%

---
```dataviewjs
// Define the link you want to filter by
const targetLink = `[[${dv.current().file.name}`;

// Initialize a variable to store the latest entry
let latestEntry = null;

// Iterate through all daily notes
dv.pages('"01_DailyNotes"')
    .sort(p => p.file.name, 'asc') // Sort by date (assuming daily notes are named YYYY-MM-DD)
    .forEach(page => {
        let dailies = page.Dailies || [];
        if (!Array.isArray(dailies)) dailies = [dailies]; // Normalize to array

        if (dailies.some(entry => entry.includes(targetLink))) {
            latestEntry = page.file.link; // Store the latest matching daily note
            return; // Exit loop once the latest occurrence is found
        }
    });

// Display the result
if (latestEntry) {
    dv.paragraph(`**Last appearance on:** ${latestEntry}`);
} else {
    dv.paragraph("No matching dailies found.");
}

```

---
>[!danger] Collaborating On
>```dataview
>TABLE Status, EndDate, tags as Tags
>WHERE contains(Collaborator, this.file.link)

>[!bug] Client Of
>```dataview
>TABLE Status, EndDate, tags as Tags
>WHERE contains(Client, this.file.link)

---

>[!example] Logs
>```dataview
>TASK
>WHERE contains(text, this.file.name)
>GROUP by file.name as Reference
>SORT Reference DESC

---
# Dailies
```dataviewjs
// Define the link you want to filter by
const targetLink = `[[${dv.current().file.name}]]`;

// Initialize an empty array to store matching dailies
let matchingEntries = [];

// Iterate through all pages in the vault or a specific folder
dv.pages('"01_DailyNotes"').forEach(page => {
    // Get the "Dailies" property as an array (supports multiple entries)
    let dailies = page.Dailies || [];
    if (!Array.isArray(dailies)) dailies = [dailies]; // Normalize to array

    // Filter for dailies containing the target link
    let filtered = dailies.filter(entry => entry.includes(targetLink));

    // Add matching entries along with the page name
    if (filtered.length > 0) {
        matchingEntries.push({
            page: page.file.link,
            entries: filtered,
            date: page.file.name // Extract the file name (assumed to be YYYY-MM-DD)
        });
    }
});

// Sort the entries by date in descending order (latest first)
matchingEntries.sort((a, b) => b.date.localeCompare(a.date));

// Display results as a table
if (matchingEntries.length > 0) {
    dv.table(["On", "Dailies"], 
        matchingEntries.map(row => [row.page, row.entries.join(", ")]));
} else {
    dv.paragraph("No matching dailies found.");
}
```