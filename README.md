# 💊 MediMinder Pro – Smart Medication Adherence Tracker

> A complete web app for medication management. It plans dose schedules, tracks every dose, warns about refills and drug interactions, and uses a **machine-learning model trained in the browser** to predict which doses you are likely to miss.

🔗 **Live demo:** https://&lt;your-username&gt;.github.io/mediminder/
&nbsp;·&nbsp; Click **✨ Demo data** on first load to explore with 60 days of sample history.

![Dashboard](docs/screenshots/dashboard.png)

---

## 📌 Problem statement
Up to half of patients with long-term conditions such as diabetes and hypertension do not take their medicines as prescribed (WHO). Missed doses lead to poor disease control and avoidable hospital visits. Most reminder apps only send alarms. They do not learn *when* and *why* a patient misses doses.

**MediMinder Pro** combines scheduling and tracking with analytics and an ML model that spots each patient's personal risk patterns, such as night doses or weekends, and gives targeted advice.

## ✨ Features
| Module | What it does |
|---|---|
| **Dashboard** | Today's timeline with Take / Snooze / Skip, a next-dose countdown, KPIs (today's progress, 7-day adherence with week-over-week change, perfect-day streak, refills due) and smart alerts |
| **Medicines** | Name, strength, form, quantity, meal timing, several daily times, chosen weekdays, course start/end dates, stock count, colour tag and notes. Stock goes down automatically when a dose is taken, with days-left estimates and refill alerts |
| **History** | Calendar heat-map coloured by daily adherence. Click a day to see each dose or correct it |
| **Analytics** | 30-day adherence trend, adherence by time of day, by weekday and per medicine, a taken/skipped/missed donut and average delay |
| **AI Insights** | Logistic-regression **missed-dose predictor**: accuracy, precision, recall, F1, ROC-AUC, confusion matrix, feature weights, training-loss curve and personalised recommendations. Each upcoming dose gets a live risk badge |
| **Interaction checker** | Checks every pair of your medicines against a built-in list of 17 well-documented interactions (generic and Indian brand names) and flags duplicates |
| **Reminders** | In-app pop-up and sound at dose time, browser notifications (on GitHub Pages), snooze |
| **Export & backup** | Dose log as CSV, a doctor-ready text report, JSON backup and restore |
| **Extras** | Dark mode, responsive mobile layout, works offline, no login, data stays in the browser |

## 🤖 Machine-learning model
**Goal:** predict the probability that a scheduled dose will be missed.

Every past scheduled dose becomes one training row. The features use only information known *before* that day, so there is no data leakage:

| # | Feature | Why it matters |
|---|---|---|
| 1 | Hour of day | Adherence changes across the day |
| 2 | Night dose (after 9 pm) | Night doses are often forgotten |
| 3 | Weekend | Routines change at weekends |
| 4 | Before-food dose | Harder timing constraint |
| 5 | Doses scheduled that day | Pill burden |
| 6 | Past miss rate of this slot (last 14 days, smoothed) | Personal habit |
| 7 | Missed a dose yesterday | Misses tend to come in runs |

**Algorithm.** Logistic regression written from scratch in `js/ml.js`:
- z-score feature standardisation
- mini-batch gradient descent with L2 regularisation
- *balanced class weights*, because missed doses are the minority class
- stratified 80/20 train/test split and evaluation metrics (accuracy, precision, recall, F1, ROC-AUC by the Mann–Whitney method)
- per-prediction explanations (feature contribution = standardised value × weight)

The model retrains automatically whenever the history changes. It needs at least 30 past doses that include both taken and missed ones.

![AI insights](docs/screenshots/insights.png)

## 🛠️ Tech stack
| Layer | Technology |
|---|---|
| UI | HTML5, CSS3 (custom design system, dark mode, responsive) |
| Logic | Vanilla JavaScript (ES2020), no frameworks |
| ML | Custom logistic regression (`js/ml.js`) |
| Charts | Custom SVG chart library (`js/charts.js`) |
| Storage | Browser `localStorage` |
| Tests | Node.js built-in test runner |
| Hosting | GitHub Pages |

**No external libraries and no build step.** Open `index.html` and it runs.

## 📂 Project structure
```
mediminder/
├── index.html              # App shell and all views
├── css/base.css            # Design system (shared look & feel)
├── js/
│   ├── ui.js               # DOM helpers, router, modals, toasts, storage, export
│   ├── ml.js               # Logistic regression + metrics (from scratch)
│   ├── charts.js           # SVG line / bar / donut / diverging-bar charts
│   ├── interactions.js     # Drug-interaction knowledge base
│   └── app.js              # App logic: schedule, tracking, analytics, ML features
├── tests/core.test.js      # Unit tests (ML + interactions)
├── docs/screenshots/       # Images used in this README
├── package.json
└── README.md
```

## 🚀 Run locally
```bash
git clone https://github.com/<your-username>/mediminder.git
cd mediminder
# open index.html in your browser, or serve it:
python -m http.server 8000      # then visit http://localhost:8000
```

## ✅ Run the tests
```bash
npm test          # or: node --test
```

## 🌐 Deploy to GitHub Pages
1. Push this folder to a public repository.
2. Go to **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, then click **Save**.
3. Your app will be live at `https://<your-username>.github.io/mediminder/`.

## 📸 Screenshots
| Analytics | History |
|---|---|
| ![Analytics](docs/screenshots/analytics.png) | ![History](docs/screenshots/history.png) |
| **Interactions** | |
| ![Interactions](docs/screenshots/interactions.png) | |

## 🔮 Future scope
- Cloud sync and caregiver accounts (Firebase / Supabase)
- Push reminders through a service worker when the tab is closed
- Prescription OCR to add medicines from a photo
- Connect to a full drug database (e.g. RxNorm / DrugBank) for interaction checks
- Gradient-boosted model when more multi-user data is available

## ⚠️ Disclaimer
This is an educational project. It does not replace medical advice. The interaction list covers common examples only. Always follow your doctor's prescription and ask a pharmacist about interactions.

## 👤 Author
**&lt;Your Name&gt;**, B.Tech CSE (AI & ML), Dayananda Sagar University, Bengaluru
GitHub: [@&lt;your-username&gt;](https://github.com/<your-username>)

## 📄 License
MIT. See [LICENSE](LICENSE).
