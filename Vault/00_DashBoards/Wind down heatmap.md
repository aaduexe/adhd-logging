---
Object: DashBoard
---
```dataviewjs

const trackerData = {
	separateMonths: true,
    entries: [],
    colorScheme: {
        customColors: [
            "#d63230",
            "#f39237",
            "#40bcd8",
            "#39a9db",
            "#1c77c3",
            ]
    },
    heatmapTitle: "🌙 At bed by 10:00 🌙",
    heatmapSubtitle: "blue for timely bedtimes and orange for late nights. Build better habits and wake up refreshed! 🌌💤",
    intensityScaleStart: 0,
    intensityScaleEnd: 1
}

// Constants for configuration
const MAX_DIFF = 120; // Maximum time difference (in minutes) after which intensity is 0
const TARGET_TIME = "22:00"; // Target wake-up time (HH:MM format)
function calculateIntensity(wakeTime, targetTime = TARGET_TIME) {
  // Parse the wake-up time from ISO string to a Date object
  //const wakeDate = new Date(wakeTimeISO);
  const [wakeHour, wakeMinute] = wakeTime.split(":").map(Number);

  // Parse target time into hours and minutes
  const [targetHour, targetMinute] = targetTime.split(":").map(Number);

  // Convert target time to minutes since midnight
  const targetMinutes = targetHour * 60 + targetMinute;

  // Get wake-up time in minutes since midnight
  const wakeMinutes = wakeHour * 60 + wakeMinute;

  // Calculate the time difference (only if wake time is after the target time)
  const diffMinutes = Math.max(0, wakeMinutes - targetMinutes);

  // Normalize the intensity value: 1 (best) -> 0 (worst)
  return Math.max(0, 1 - diffMinutes / MAX_DIFF);
}

 
for(let page of dv.pages('"01_DailyNotes"').where(p=>p.onBed)){
    trackerData.entries.push({
        date: page.file.name,
        intensity: calculateIntensity(page.onBed),
        content: await dv.span(`[](${page.file.name})`)
    })  
}

renderHeatmapTracker(this.container, trackerData)

```
