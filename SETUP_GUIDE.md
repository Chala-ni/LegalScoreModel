# 🚀 Setup Guide for Students

## ⏱️ Time Required: 10-15 minutes

---

## Step-by-Step Checklist

### ✅ Step 1: Extract Files (1 min)

1. Extract the ZIP file to `D:\` drive
2. Final path: `D:\LegalScoreModel\`
3. Verify you see these folders:
   - ✓ `app/`
   - ✓ `data/`
   - ✓ `models/`
   - ✓ `scripts/`
   - ✓ Files: `README.md`, `.env.example`, `requirements.txt`

---

### ✅ Step 2: Create Virtual Environment (2 min)

Open PowerShell and run:

```powershell
cd D:\LegalScoreModel
python --version  # Must be 3.10 or higher
python -m venv .venv
& .\.venv\Scripts\Activate.ps1
```

**✓ Check:** Your prompt should show `(.venv)` at the start

**If error:** "Execution policy" → Run this first:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

### ✅ Step 3: Install Packages (3 min)

```powershell
pip install -r requirements.txt
```

**✓ Check:** No red error messages. Should install ~20 packages.

---

### ✅ Step 4: Get Free API Key (3 min)

1. Go to: https://openrouter.ai/
2. Click "Sign In" → Sign up with Google/GitHub
3. Go to "Keys" → Click "Create Key"
4. Copy the key (starts with `sk-or-v1-...`)

---

### ✅ Step 5: Create .env File (1 min)

```powershell
Copy-Item .env.example .env
notepad .env
```

In Notepad, paste your API key:
```env
INFERENCE_BACKEND=openrouter
OPENROUTER_API_KEY=sk-or-v1-YOUR_KEY_HERE  ← PASTE HERE
OPENROUTER_MODEL=deepseek/deepseek-chat
```

Save and close.

---

### ✅ Step 6: Start Server (1 min)

```powershell
python -m uvicorn app.main:app --reload --port 8000
```

**✓ Check:** Should see:
```
INFO:     Uvicorn running on http://127.0.0.1:8000
INFO:     Application startup complete.
```

**Keep this window open!**

---

### ✅ Step 7: Test API (2 min)

Open browser: http://localhost:8000

Should see:
```json
{
  "message": "Legal Argument Critic API",
  "version": "1.0.0"
}
```

Then open: http://localhost:8000/docs

Should see interactive API documentation.

---

### ✅ Step 8: Run Tests (2 min)

**Open NEW PowerShell window** (keep server running):

```powershell
cd D:\LegalScoreModel
& .\.venv\Scripts\Activate.ps1
python test_full_pipeline.py
```

**✓ Expected:**
```
TEST 1: Health Check ✅
TEST 2: Text Analysis ✅
TEST 3: PDF Upload ✅
TEST 4: JSON Format ✅

All tests passed!
```

---

## ✅ You're Done! 🎉

Your API is now running and ready for frontend development.

---

## 🎨 Next Steps: Build Frontend

### Quick Test from Browser Console

Open http://localhost:8000/docs and try the `/api/v1/analyze` endpoint, or:

Open browser console (F12) and run:

```javascript
fetch('http://localhost:8000/api/v1/analyze', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    text: 'The appellant challenges the lower court decision on grounds of procedural irregularity. The court failed to consider Section 91 of the Civil Procedure Code which mandates proper notice to all parties.'
  })
})
.then(r => r.json())
.then(data => console.log(data));
```

You should see JSON response with score, breakdown, and feedback!

---

## 📊 Understanding the JSON Response

### What You Get:

```json
{
  "overall_score": 75,           // 0-100 score
  "strength_label": "Moderate",  // Very Weak/Weak/Moderate/Strong
  "breakdown": [                 // 8 categories
    {
      "category": "Issue & Claim Clarity",
      "rubric_score": 4,         // 0-5 score
      "points": 8.0,             // Weighted points
      "rationale": "..."         // Explanation
    }
    // ... 7 more
  ],
  "feedback": [                  // Improvement tips
    "Add more case citations",
    "Address counterarguments"
  ]
}
```

### How to Use in Frontend:

**Display Overall Score:**
```javascript
<h1>Score: {data.overall_score}/100</h1>
<p>Strength: {data.strength_label}</p>
```

**Show Category Chart:**
```javascript
data.breakdown.forEach(category => {
  const percentage = (category.rubric_score / 5) * 100;
  // Create progress bar with percentage
});
```

**List Weaknesses:**
```javascript
const weak = data.breakdown.filter(cat => cat.rubric_score < 3);
// Show these as "Areas to Improve"
```

**Show Suggestions:**
```javascript
data.feedback.forEach(tip => {
  // Display as bullet points
});
```

---

## 🔧 Common Issues

### Issue: Port 8000 already in use

```powershell
netstat -ano | findstr 8000
# Find the PID, then:
Stop-Process -Id <PID> -Force
```

### Issue: Module not found

```powershell
& .\.venv\Scripts\Activate.ps1  # Activate venv first!
pip install -r requirements.txt
```

### Issue: API returns error

Check `.env` file has correct API key:
```powershell
cat .env  # Should show your sk-or-v1-... key
```

### Issue: Tests fail

Make sure:
1. Server is running (in another window)
2. Virtual environment is activated
3. API key is configured in `.env`

---

## 📚 Full Documentation

See [README.md](README.md) for complete API reference and frontend examples.

---

## ❓ Quick Reference

**Start Server:**
```powershell
cd D:\LegalScoreModel
& .\.venv\Scripts\Activate.ps1
python -m uvicorn app.main:app --reload --port 8000
```

**Run Tests:**
```powershell
cd D:\LegalScoreModel
& .\.venv\Scripts\Activate.ps1
python test_full_pipeline.py
```

**API Docs:**
- Interactive: http://localhost:8000/docs
- JSON: http://localhost:8000/openapi.json

**Endpoints:**
- Analyze text: `POST /api/v1/analyze`
- Upload PDF: `POST /api/v1/upload`
- Health check: `GET /api/v1/health`

---

**Status:** ✅ Ready for frontend development!
