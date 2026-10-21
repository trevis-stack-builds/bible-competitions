# 🚀 Web App - Bible QuizCraft

An interactive, multi-user Bible quiz platform where hosts and participants can collaboratively prepare question repositories, schedule timed challenges, and test their Bible knowledge with instant automated grading and live leaderboards.

[👉 **View Live App](https://trevis-stack-builds.github.io/bible-competitions/)**

---

## 🌟 Features

* **Multi-Format Question Creation:** Supports Multiple Choice (MCQ), True/False/Not Given (TFNGQ), Fill in the Blanks, Matching Pairs, and Chronological Ordering questions with optional solution explanations.


* **Collaborative Question Banking:** Confidential creation phase allowing users to upload questions privately before hosts publish them live to the shared quiz bank.


* **Batch Import & Export:** Bulk question management using Excel/CSV spreadsheets (`.xlsx`, `.xls`, `.csv`, `.numbers`) with downloadable pre-formatted templates and unified repository export.


* **Timed Live Quizzes & Guest Mode:** Host-controlled live quiz sessions with automatic scheduling, submission deadlines, countdown timers, and an instant zero-login Guest Challenge mode.


* **Analytics, Leaderboard & Vault:** Real-time scoring breakdowns, confetti celebration, composite participant leaderboards, past session archives (Past Paper Vault), and multi-platform achievement sharing (WhatsApp, Signal, Instagram, Email).


* **Real-Time Community & Host Controls:** Built-in community chatroom with pinned announcement support, user role management (Host, Co-host, Participant), user ordering, and feedback collection.


* **Bilingual Interface:** Instant full UI translation toggling between English (EN) and Traditional Chinese (繁體中文).


* **Responsive Design:** Optimized for seamless navigation across desktop, tablet, and mobile devices.



---

## 🛠️ Tech Stack

* **Frontend:** Vanilla JavaScript (ES6+), HTML5, CSS3


* **Styling:** [Tailwind CSS](https://tailwindcss.com/) (via CDN)


* **Icons:** [Lucide Icons](https://lucide.dev/)

* **Backend & Database:** [Supabase](https://supabase.com/) (`@supabase/supabase-js`) with built-in in-memory / local storage fallback client for offline/demo mode


* **Utilities & Effects:**
* [SheetJS (xlsx)](https://sheetjs.com/) for spreadsheet batch processing


* [canvas-confetti](https://www.npmjs.com/package/canvas-confetti) for celebratory quiz submission animations




* **Hosting:** GitHub Pages

---

## 💻 Local Development

To run this project locally on your machine:

1. **Clone the repository:**
```bash
git clone https://github.com/trevis-stack-builds/bible-competitions.git
cd bible-competitions

```


2. **Open the application:**
* Because Bible QuizCraft is built as a lightweight client-side application, you can open `index.html` (or the application HTML file) directly in any modern browser.


* Alternatively, serve it via a local static server:
```bash
# Using Python 3
python3 -m http.server 8000

```


Then navigate to `http://localhost:8000` in your web browser.


3. **Configure Database (Optional):**
* The application runs out of the box in **Local Demo Mode** using browser storage.


* To connect to a live Supabase backend, update `SUPABASE_URL` and `SUPABASE_ANON_KEY` in the script tag with your project credentials.
