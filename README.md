# 🩺 CareCompass AI

**AI-Assisted Healthcare Triage & Patient Tracking System**

A hackathon MVP built for rural and under-resourced healthcare settings. This system provides AI-powered triage support to help healthcare workers prioritize patient care.

> ⚠️ **Medical Disclaimer**: This system provides AI-assisted triage support only. It does NOT provide medical diagnosis or treatment. All clinical decisions remain the responsibility of qualified healthcare professionals.

---

## 📋 Features

- **🔐 Authentication**: Email/password login with role-based access (Doctor/Admin)
- **🤖 AI Triage**: Google Gemini-powered analysis with structured risk assessment
- **📊 Patient Records**: Timeline view of patient visits with trend analysis
- **📈 Dashboard**: Real-time statistics on case volumes and risk levels
- **📱 Responsive Design**: Mobile-friendly interface
- **📄 PDF Export**: Print/export case details for documentation

---

## 🏗️ Project Structure

```
carecompass-ai/
├── backend/
│   ├── server.js          # Express server with Gemini AI integration
│   └── package.json       # Backend dependencies
│
└── frontend/
    ├── index.html         # Main app structure
    ├── styles.css         # Professional medical theme
    └── app.js             # Firebase + application logic
```

---

## 🚀 Setup Instructions

### Prerequisites

- **Node.js** (v14 or higher)
- **Google Gemini API Key** ([Get one here](https://makersuite.google.com/app/apikey))
- **Firebase Project** ([Create one here](https://console.firebase.google.com))

### Step 1: Backend Setup

1. **Navigate to backend folder**:
   ```bash
   cd backend
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Configure Gemini API Key**:
   - Open `server.js`
   - Find line 23: `const GEMINI_API_KEY = 'YOUR_GEMINI_API_KEY_HERE';`
   - Replace with your actual API key

4. **Start the server**:
   ```bash
   node server.js
   ```
   
   Server will run on `http://localhost:3000`

### Step 2: Firebase Setup

1. **Create a Firebase project**:
   - Go to [Firebase Console](https://console.firebase.google.com)
   - Click "Add project"
   - Follow the setup wizard

2. **Enable Authentication**:
   - In Firebase Console, go to **Authentication** → **Sign-in method**
   - Enable **Email/Password**

3. **Create Firestore Database**:
   - Go to **Firestore Database** → **Create database**
   - Start in **test mode** (for development)
   - Choose a location

4. **Get Firebase Configuration**:
   - Go to **Project Settings** → **Your apps**
   - Click **Web** (</> icon)
   - Copy the `firebaseConfig` object

5. **Configure Frontend**:
   - Open `frontend/app.js`
   - Find lines 20-26 (the `firebaseConfig` object)
   - Replace with your Firebase configuration

### Step 3: Run the Frontend

1. **Open the app**:
   - Simply open `frontend/index.html` in your web browser
   - Or use a local server:
     ```bash
     cd frontend
     python -m http.server 8000
     ```
   - Then visit `http://localhost:8000`

2. **Create an account**:
   - Click "Register"
   - Enter your details
   - Leave admin code blank for doctor role
   - Or use `ADMIN2024` for admin access

---

## 🎯 Usage Guide

### Creating a New Case

1. Click **"New Case"** tab
2. Choose **"New Patient"** or **"Existing Patient"**
3. Fill in patient details and symptoms
4. Add vitals (optional but recommended)
5. Click **"Analyze & Save Case"**
6. View AI triage results

### Viewing Patient Records

1. Click **"Patient Records"** tab
2. Click on a patient to expand their timeline
3. Click on any case to view full details
4. Export to PDF if needed

### Understanding Trends

- **↓ Improving**: Risk score decreased by >10 points
- **→ Stable**: Risk score changed by ≤10 points
- **↑ Worsening**: Risk score increased by >10 points

### Dashboard

- View total cases and breakdown by risk level
- **Admin**: See all cases across all doctors
- **Doctor**: See only your own cases

---

## 🎨 Risk Levels

| Level | Score Range | Color | Meaning |
|-------|-------------|-------|---------|
| **Low** | 0-25 | 🟢 Green | Routine care |
| **Moderate** | 26-50 | 🟡 Yellow | Monitor closely |
| **High** | 51-75 | 🟠 Orange | Urgent attention |
| **Critical** | 76-100 | 🔴 Red | Immediate action |

---

## 🔧 Troubleshooting

### Backend Issues

**Problem**: Server won't start
- Check if Node.js is installed: `node --version`
- Make sure you ran `npm install`
- Check if port 3000 is available

**Problem**: AI analysis fails
- Verify your Gemini API key is correct
- Check your internet connection
- Look at server console for error messages

### Frontend Issues

**Problem**: Can't login/register
- Check browser console for errors
- Verify Firebase configuration is correct
- Make sure Firestore is created and in test mode

**Problem**: Cases not saving
- Check if backend server is running
- Verify Firebase connection
- Check browser console for errors

### CORS Issues

If you see CORS errors:
- Make sure backend server is running
- Try using a local server for frontend (not just opening HTML file)
- Check that backend has CORS enabled (it should by default)

---

## 🛡️ Security Notes

**For Production Deployment**:

1. **Firestore Rules**: Update to proper security rules
   ```javascript
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{userId} {
         allow read, write: if request.auth != null && request.auth.uid == userId;
       }
       match /patients/{patientId} {
         allow read, write: if request.auth != null;
       }
       match /cases/{caseId} {
         allow read, write: if request.auth != null;
       }
     }
   }
   ```

2. **API Keys**: Use environment variables, not hardcoded values

3. **Backend**: Deploy to a secure server with HTTPS

4. **Admin Code**: Change the default admin code in `app.js`

---

## 📝 API Reference

### Backend Endpoint

**POST** `/analyze`

**Request Body**:
```json
{
  "patientName": "string",
  "age": "string",
  "symptoms": "string",
  "vitals": "string"
}
```

**Response**:
```json
{
  "risk_level": "Low|Moderate|High|Critical",
  "risk_score": 0-100,
  "key_concerns": ["array of concerns"],
  "triage_recommendation": "string",
  "clinical_summary": "string",
  "tests_advised": ["array of tests"],
  "first_aid_steps": ["array of steps"],
  "when_to_refer": "string"
}
```

---

## 🎓 For Beginners

This project is designed to be beginner-friendly:

- **No frameworks**: Just vanilla HTML, CSS, and JavaScript
- **Well-commented code**: Every section is explained
- **Copy-paste safe**: You can copy entire files
- **Clear structure**: Each file has a single purpose

### Learning Resources

- [Firebase Documentation](https://firebase.google.com/docs)
- [Express.js Guide](https://expressjs.com/en/starter/installing.html)
- [Google Gemini API](https://ai.google.dev/docs)

---

## 🏆 Hackathon Tips

### For Demo

1. **Prepare test cases**: Have 2-3 sample patients ready
2. **Show the flow**: Register → Create case → View records → Dashboard
3. **Highlight AI**: Show the triage results and explain risk levels
4. **Show trends**: Create multiple visits for one patient
5. **Explain safety**: Emphasize the disclaimers and responsible AI use

### Talking Points

- **Problem**: Rural healthcare workers need triage support
- **Solution**: AI-powered risk assessment with patient tracking
- **Impact**: Helps prioritize care in resource-limited settings
- **Safety**: Clear disclaimers, not a diagnostic tool
- **Scalability**: Offline-first design (future enhancement)

---

## 📄 License

MIT License - Feel free to use for your hackathon!

---

## 🙏 Acknowledgments

Built with:
- Google Gemini AI
- Firebase (Auth + Firestore)
- Express.js
- Vanilla JavaScript

---

## 📞 Support

For issues or questions during the hackathon:
1. Check the troubleshooting section above
2. Review the code comments
3. Check browser console for errors
4. Verify all API keys are configured

**Good luck with your hackathon! 🚀**
