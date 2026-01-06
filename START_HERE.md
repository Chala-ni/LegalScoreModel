# 📚 Documentation Index

## 👋 Start Here!

Welcome to the Legal Argument Critic API. This project provides an AI-powered API to analyze and score legal arguments from Sri Lankan civil cases.

---

## 📖 Documentation Files

### For Setup (Read First!)

1. **[SETUP_GUIDE.md](SETUP_GUIDE.md)** ⭐ START HERE
   - Step-by-step setup instructions (10-15 min)
   - Troubleshooting common issues
   - Quick reference for running the server
   - **Read this first if you've never set up the project**

2. **[README.md](README.md)** 📘 Complete Reference
   - Full API documentation
   - All endpoints with examples
   - Backend configuration options
   - Advanced troubleshooting
   - **Read after setup for complete details**

### For Frontend Developers

3. **[FRONTEND_GUIDE.md](FRONTEND_GUIDE.md)** 🎨 Frontend Quick Reference
   - API response structure (TypeScript interfaces)
   - Copy-paste code snippets (React, JavaScript)
   - Chart integration examples
   - Error handling patterns
   - **Use this while building your frontend**

### Project Status

4. **[PROJECT_STATUS.md](PROJECT_STATUS.md)** ✅ Deliverables Checklist
   - What's included in this ZIP
   - Feature completion status
   - Testing results
   - **Read to understand what's ready**

---

## 🚀 Quick Start Path

```
Step 1: Read SETUP_GUIDE.md
   ↓
Step 2: Follow setup steps (10-15 min)
   ↓
Step 3: Verify server is running
   ↓
Step 4: Read FRONTEND_GUIDE.md
   ↓
Step 5: Build your frontend!
```

---

## ❓ Which Document Do I Need?

### "I just received the ZIP file"
→ **[SETUP_GUIDE.md](SETUP_GUIDE.md)**

### "Server won't start / I'm getting errors"
→ **[README.md](README.md)** → Troubleshooting section

### "How do I call the API from my frontend?"
→ **[FRONTEND_GUIDE.md](FRONTEND_GUIDE.md)** → Quick Code Snippets

### "What does the JSON response look like?"
→ **[FRONTEND_GUIDE.md](FRONTEND_GUIDE.md)** → JSON Response Structure

### "How do I display the score/categories/feedback?"
→ **[FRONTEND_GUIDE.md](FRONTEND_GUIDE.md)** → React/JavaScript examples

### "Where are the JSON files saved?"
→ **They aren't!** The API returns JSON via HTTP. See [README.md](README.md) → Key Concept

### "How do I switch from OpenRouter to Gemini?"
→ **[README.md](README.md)** → Backend Options

### "Can I use my own fine-tuned model?"
→ **[README.md](README.md)** → Option 3: Local Fine-Tuned Model

---

## 🔑 Key Concepts

### API-First Architecture

**No JSON files are saved to disk!**

- Frontend makes HTTP POST request
- Backend processes and returns JSON
- Frontend receives and displays results
- All communication via API

```
Frontend → API → JSON Response → Display
```

### JSON Response Contains:

✅ `overall_score` - 0-100 score  
✅ `strength_label` - "Very Weak" / "Weak" / "Moderate" / "Strong"  
✅ `breakdown` - 8 categories with scores and explanations  
✅ `feedback` - Array of improvement suggestions  

### Your Frontend Should:

1. Accept text input or PDF upload
2. Call API endpoint
3. Parse JSON response
4. Display:
   - Overall score with progress bar
   - Category breakdown with charts
   - Weaknesses (low-scoring categories)
   - Improvement suggestions

---

## 📦 What's in This ZIP?

```
LegalScoreModel/
├── 📄 SETUP_GUIDE.md          ← Start here!
├── 📄 README.md               ← Full documentation
├── 📄 FRONTEND_GUIDE.md       ← Frontend code examples
├── 📄 PROJECT_STATUS.md       ← Project summary
├── 📄 .env.example            ← Configuration template
├── 📄 requirements.txt        ← Python dependencies
├── 📄 test_full_pipeline.py   ← Test suite
├── 📄 api_examples.py         ← Additional examples
│
├── 📁 app/                    ← FastAPI server
│   ├── main.py
│   ├── api/v1/analyze.py
│   └── services/inference_service.py
│
├── 📁 models/fine_tuned/      ← Fine-tuned model
│   └── adapter_model/         (117 MB)
│
├── 📁 scripts/                ← Utility scripts
│   └── merge_and_convert_ollama.py
│
├── 📁 data/raw_pdfs/          ← Sample PDFs (80 files)
│
└── 📁 training_pipeline/      ← Training notebooks
```

---

## ✅ Checklist: Am I Ready?

### Setup Complete?

- [ ] Extracted ZIP to `D:\LegalScoreModel\`
- [ ] Created virtual environment (`.venv`)
- [ ] Installed dependencies (`pip install -r requirements.txt`)
- [ ] Created `.env` file with API key
- [ ] Server starts successfully (`python -m uvicorn app.main:app --reload`)
- [ ] Browser shows API at http://localhost:8000
- [ ] Tests pass (`python test_full_pipeline.py`)

### Understanding Complete?

- [ ] I know the API returns JSON (not files)
- [ ] I know how to call `/api/v1/analyze` endpoint
- [ ] I understand the JSON response structure
- [ ] I know how to extract score, categories, and feedback
- [ ] I know where to find code examples

### Ready to Build!

- [ ] Frontend project created (React/Vue/etc)
- [ ] Can fetch from `http://localhost:8000`
- [ ] Tested API call from browser console
- [ ] Know how to display results in UI

---

## 💡 Tips for Success

### 1. Keep Server Running
The FastAPI server must run continuously while developing your frontend.

### 2. Use Swagger Docs
http://localhost:8000/docs provides interactive API testing.

### 3. Copy-Paste from FRONTEND_GUIDE.md
Don't write from scratch - adapt the provided examples.

### 4. Test with Real PDFs
Use the PDFs in `data/raw_pdfs/` for testing file uploads.

### 5. Handle Errors Gracefully
API can fail - always check response status and show user-friendly errors.

---

## 🆘 Getting Help

### Step 1: Check Documentation
- Setup issue? → [SETUP_GUIDE.md](SETUP_GUIDE.md)
- API issue? → [README.md](README.md) Troubleshooting
- Frontend issue? → [FRONTEND_GUIDE.md](FRONTEND_GUIDE.md)

### Step 2: Verify Basics
```powershell
# Is server running?
curl http://localhost:8000

# Is API key configured?
cat .env

# Is virtual environment activated?
# Should see (.venv) in prompt
```

### Step 3: Run Tests
```powershell
python test_full_pipeline.py
```

If tests pass but frontend fails → Check CORS settings in README.md

---

## 🎯 Next Steps

1. ✅ Complete setup (SETUP_GUIDE.md)
2. ✅ Verify API works (test_full_pipeline.py)
3. ✅ Read FRONTEND_GUIDE.md
4. ✅ Test API from browser console
5. ✅ Build your frontend
6. ✅ Deploy and demo!

---

**Good luck with your project! 🚀**

---

## 📞 Quick Links

- Interactive Docs: http://localhost:8000/docs
- API Info: http://localhost:8000
- Health Check: http://localhost:8000/api/v1/health

**Documentation Version:** 1.0.0  
**Last Updated:** January 6, 2026  
**API Version:** 1.0.0
