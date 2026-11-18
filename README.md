# 💊 MediMinder – Medicine Reminder & Dose Tracker

MediMinder is a simple web app for planning daily medicines. You tick off each dose as you take it, and the app shows how well you are keeping to your schedule.

🔗 **Live Demo:** https://<your-username>.github.io/mediminder/

---

## 📌 Problem Statement
Many patients, especially elderly people and those with long-term conditions, forget or skip doses. Missed doses make treatment work less well. MediMinder gives a clear daily schedule, reminds you when a dose is due, and tracks how often you follow the plan.

## ✨ Features
- **Add medicines** with name, dose, meal timing (before or after food) and several times per day
- **Today's schedule** sorted by time, with a **Taken ✓** button for each dose
- **Missed doses shown in red** once their time has passed
- **Reminder pop-up** when a dose time arrives (while the page is open)
- **Stats dashboard**
  - Doses taken today (e.g. 2/3)
  - 7-day adherence percentage with a progress bar
  - Streak of days with every dose taken
- **Data stays in your browser** (localStorage): no login, no server, private by default
- **Responsive design** for mobile and desktop

## 🛠️ Tech Stack
| Layer | Technology |
|-------|------------|
| Frontend | HTML5, CSS3 |
| Logic | Vanilla JavaScript (ES6) |
| Storage | Browser localStorage |
| Hosting | GitHub Pages |

No frameworks or libraries are needed. The whole app is one `index.html` file.

## 📂 Project Structure
```
mediminder/
├── index.html   # Complete app (HTML + CSS + JS)
└── README.md    # Project documentation
```

## 🚀 How to Run
**Option 1: Open locally**
1. Download or clone this repository
   ```bash
   git clone https://github.com/<your-username>/mediminder.git
   ```
2. Open `index.html` in any web browser.

**Option 2: Use the live demo**
Visit the GitHub Pages link above.

## 📖 How to Use
1. Enter the medicine name, dose and meal timing.
2. Enter times in 24-hour format, separated by commas (e.g. `08:00, 20:00`).
3. Click **Add to schedule**.
4. Click **Taken ✓** when you take each dose. Click **Undo** if you made a mistake.
5. Check the stats at the top to see your adherence and streak.

## ⚙️ How It Works
- Each medicine is stored as an object: `{ id, name, dose, meal, times[] }`
- Taken doses are logged by date: `log["YYYY-MM-DD"]["medId@HH:MM"] = true`
- **Adherence %** = doses taken ÷ doses scheduled over the last 7 days × 100
- **Streak** = number of days in a row with every scheduled dose taken
- A timer checks every 30 seconds and shows a reminder when a dose is due

## 🔮 Future Scope
- Browser push notifications that work when the tab is closed
- Cloud sync and login (Firebase)
- Refill alerts when stock runs low
- Caregiver mode to track a family member's doses
- Export adherence report as PDF to share with a doctor

## 📸 Screenshots

<!-- ![MediMinder Screenshot](screenshot.png) -->

## ⚠️ Disclaimer
This app is only for reminders and tracking. It does not give medical advice. Always follow your doctor's prescription.

## 👤 Author
**<Your Name>**
B.Tech CSE (AI & ML), Dayananda Sagar University, Bengaluru
GitHub: [@<your-username>](https://github.com/<your-username>)
