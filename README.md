# 🚀 Leetrino - LeetCode AI Assistant by Priyansh

**Leetrino** is a Chrome Extension that brings AI-powered hints, approach, pseudo-code, solutions, and complexity analysis right into your LeetCode problems page — powered by **Google Gemini** API.

---

## ✨ Features

- 💡 Reveal **Quick Hints** (without spoiling)
- 🧠 Understand the **Optimal Approach**
- 📋 View **Pseudo-code** (Java-style)
- ✅ Get a clean **Java Code Solution**
- ⏱ View **Time & Space Complexity**
- 🧪 Fully integrated into the LeetCode interface
- 🔑 Uses your **own Gemini API key**

---

## 🧩 Folder & File Structure

leetrino/
│
├── manifest.json            ← Extension setup file
├── background.js            ← Handles Gemini API requests
├── content_script.js        ← Injects UI into LeetCode & manages interaction
├── popup.html               ← Extension settings window
├── popup.js                 ← Logic for saving/loading API key
├── panel.html               ← AI Panel HTML injected into LeetCode
├── styles.css               ← Custom CSS styles for panel
└── icons/                   ← Icons for Chrome extension


---

## 🧠 Code Flow Explained

### 🔹 1. `manifest.json` — **Extension Blueprint**
Defines how your extension works, and what scripts it loads.

- Loads:
  - `content_script.js` on `leetcode.com/problems/*`
  - `popup.html` as the settings popup
  - `background.js` as a service worker
- Grants access to:
  - Active tab
  - Storage
  - LeetCode pages

---

### 🔹 2. `popup.html` — **Settings UI**
- Simple UI shown when clicking the extension icon
- Lets users **enter and save** their Gemini API key

---

### 🔹 3. `popup.js` — **Handles API Key**
- On Load:
  - Checks if API key is stored and displays a message
- On Save:
  - Saves the key using `chrome.storage.sync`
- Optional: Can add delete/reset functionality

---

### 🔹 4. `content_script.js` — **LeetCode Page Logic**
Injected into every LeetCode problem page.

- Adds **"Analyze Problem"** button near the title
- Loads `panel.html` into the page dynamically
- Handles clicks like “Reveal Hints”, “Reveal Solution”
- Extracts:
  - Problem Title
  - Problem Description
- Sends a request to `background.js` with:
  - Problem content
  - User stage (hint, solution, etc.)

- Receives AI response from `background.js` and displays it in the panel

---

### 🔹 5. `panel.html` — **AI Assistant Panel UI**
- HTML panel injected into the bottom of the LeetCode page
- Contains:
  - 5 Steps: Hints, Approach, Pseudo-code, Solution, Complexity
  - Buttons to **Reveal** and **Retry**
- You can customize the footer to show your name

---

### 🔹 6. `background.js` — **AI Communication Hub**
Handles all communication with **Google Gemini API**.

- Listens for messages like `{ type: "getAnalysis", problem, stage }`
- Loads stored API key
- Sends prompt to Gemini API
- Returns AI response back to `content_script.js`
- Handles errors (quota exceeded, invalid key, etc.)

Contains prompt templates for each stage:
- 💡 Hints
- 🧠 Approach
- 📋 Pseudo-code
- ✅ Solution
- ⏱ Complexity

---

### 🔹 7. `styles.css` — *(Optional)*
Custom styles for the injected panel. You can:
- Change button colors
- Style headings, text, etc.

---

## 🧪 How It Works (Flow Summary)

1. User opens a LeetCode problem
2. `content_script.js` runs and adds a button: **"Analyze Problem"**
3. Clicking it shows the **AI Assistant Panel** (`panel.html`)
4. When user clicks any **Reveal** button:
   - Problem title & description are captured
   - Sent to `background.js`
   - Gemini API is called
   - Response is sent back and rendered

---

## 🛠 How to Use This Extension

### ✅ Step-by-step Instructions:

1. **Download or clone** the folder
2. Go to: `chrome://extensions`
3. Enable **Developer Mode**
4. Click **"Load unpacked"**
5. Select the folder that contains your files
6. Click the extension icon in Chrome
7. Paste your **Google Gemini API key**
   - You can get it from [https://makersuite.google.com/app/apikey](https://makersuite.google.com/app/apikey)
8. Go to any LeetCode problem like:
   - `https://leetcode.com/problems/two-sum`
9. Click **"Analyze Problem"**
10. Use the AI panel to get help step-by-step


---

## 💡 Future Ideas (Optional)

- [ ] Add support for Python/C++ solutions
- [ ] Save user history locally
- [ ] Offline mode using local storage
- [ ] Integrate with LeetCode "Discuss" section

---

## 🙌 Credits

Made with 💻 by **Priyansh**  
LeetCode + Gemini + Chrome = 💥 Productivity Boost

---

## 📄 License

Free for personal and educational use.

---

## 🧠 Final Notes

This is a powerful tool to **learn smart, not hard**. The AI doesn’t give direct answers immediately — it helps you think in the right direction. Use it responsibly and grow your problem-solving skills! 💪

---
