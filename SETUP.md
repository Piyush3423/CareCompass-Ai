# 🚀 Quick Setup Guide

## ⏱️ 5-Minute Setup

### 1️⃣ Backend (2 minutes)

```bash
# Navigate to backend
cd backend

# Install dependencies
npm install

# Edit server.js - Add your Gemini API key on line 23
# Get key from: https://makersuite.google.com/app/apikey

# Start server
node server.js
```

✅ You should see: "Server running on http://localhost:3000"

---

### 2️⃣ Firebase (2 minutes)

1. Go to https://console.firebase.google.com
2. Create a new project
3. Enable **Authentication** → **Email/Password**
4. Create **Firestore Database** (test mode)
5. Go to **Project Settings** → Copy the config object
6. Paste into `frontend/app.js` (lines 20-26)

---

### 3️⃣ Frontend (1 minute)

```bash
# Just open in browser
cd frontend
# Double-click index.html

# OR use a local server
python -m http.server 8000
# Then visit: http://localhost:8000
```

---

## 🎯 First Use

1. **Register** an account (leave admin code blank)
2. Click **"New Case"**
3. Enter patient details and symptoms
4. Click **"Analyze & Save Case"**
5. View the AI triage results!

---

## ⚠️ Common Issues

| Problem | Solution |
|---------|----------|
| Backend won't start | Run `npm install` first |
| AI analysis fails | Check Gemini API key |
| Can't login | Verify Firebase config |
| CORS errors | Make sure backend is running |

---

## 📝 Configuration Checklist

- [ ] Node.js installed
- [ ] Backend dependencies installed (`npm install`)
- [ ] Gemini API key added to `server.js`
- [ ] Backend server running on port 3000
- [ ] Firebase project created
- [ ] Email/Password auth enabled
- [ ] Firestore database created
- [ ] Firebase config added to `app.js`
- [ ] Frontend opened in browser

---

## 🎓 File Locations

**Backend API Key**: `backend/server.js` → Line 23
```javascript
const GEMINI_API_KEY = 'YOUR_GEMINI_API_KEY_HERE';
```

**Firebase Config**: `frontend/app.js` → Lines 20-26
```javascript
const firebaseConfig = {
  apiKey: "YOUR_FIREBASE_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  // ... rest of config
};
```

---

## 🏆 Demo Tips

1. **Prepare 2-3 test cases** before the demo
2. **Show different risk levels** (Low, Moderate, High, Critical)
3. **Demonstrate trends** by creating multiple visits for one patient
4. **Highlight the disclaimers** to show responsible AI use
5. **Show both doctor and admin views** (use admin code: `ADMIN2024`)

---

**Need help?** Check the full [README.md](README.md) for detailed instructions.
