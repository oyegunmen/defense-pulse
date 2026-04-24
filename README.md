Static Website to Monitor the Situation.

## 🎯 Project Purpose
**Indian News Pulse (indipulse.in)** is a specialized, lightweight aggregator for Indian Defense and Geopolitical news, social media updates (X/Twitter), and YouTube content.
* **Target Audience:** Non-technical Indian users looking for a clean, ad-free monitoring tool.
* **Core Value:** Ad-free, Anonymous, Curated, and Centralized.
* **Guiding Principle:** Avoid LLM summaries, vector databases, or complex AI features to keep the project sustainable on free hosting resources.

---

## 🏗️ Technical Architecture
The project uses a **Static Site Generation (SSG)** approach where data is updated periodically by a script rather than a live server-side database.

### 1. Backend Engine (`Aggregator.py`)
* **Logic:** Uses `feedparser` to parse RSS/Atom feeds defined in `feeds.json`.
* **Window:** Strictly filters for content from the **last 48 hours** to keep the feed fresh.
* **Timezone:** Processes and labels all data in **Indian Standard Time (IST)**.
* **Output:** Overwrites a flat `data.json` file which acts as the database.

### 2. Data Layer (`data.json`)
* **Structure:**
    * `news`: Title, link, source, time, and 150-char truncated description.
    * `youtube`: Title, link, source, time, and auto-generated thumbnail URL.
    * `tweets`: Content/Title, link, source, and time.
    * `metadata`: Stores `last_updated` and `next_update` strings for the UI status bar.

### 3. Frontend (`index.html` + `app.js`)
* **Framework:** No frameworks (No React/Vue/Tailwind). Uses **Vanilla JavaScript** and minimalist CSS (`@knadh/oat`).
* **State Management:** Uses a `Set` for `activeSources` to allow real-time client-side filtering.
* **Rendering:** Uses a tabbed system (News/Tweets/YouTube) with a shared `render()` function generating HTML cards dynamically.
* **Cache Busting:** Fetches `data.json?v=[timestamp]` to bypass browser caching and show real-time updates.

---

## 🛠️ Known Issues & Specific Logic
* **YouTube RSS Bug:** Includes a hardcoded error state UI to handle the intermittent YouTube RSS 404 errors (typically 8 AM – 1 PM IST).
* **Source Filtering:** The UI dynamically builds the filter checklist based *only* on the sources available in the currently active tab.
* **Analytics:** Uses **GoatCounter** for privacy-first, lightweight tracking without cookies.

---

## 🚫 Development Constraints
1. **No Paid Services:** Never suggest features requiring AWS, Firebase, or paid APIs.
2. **No AI/LLM:** Do not suggest "AI-powered" summaries, sentiment analysis, or chatbots.
3. **Keep it Static:** All interactivity must remain client-side using the `data.json` file.
4. **Mobile First:** The `bottom-nav` and card layouts must remain highly responsive for mobile users.
5. **Vanilla Tech:** Stick to Vanilla JS and CSS. Do not introduce heavy dependencies or modern frameworks.
6. **Audience-Centric:** The UI is for end-users, not developers. Keep instructions and labels simple.