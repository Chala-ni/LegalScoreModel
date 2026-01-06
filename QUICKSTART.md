# 🎯 Quick Start Guide

## ✅ What Has Been Created

### 1️⃣ Project Structure
```
✓ app/                    - FastAPI backend (services, API, core)
✓ training_pipeline/      - ML pipeline scripts
✓ data/                   - Data storage (PDFs, processed text, metadata)
✓ models/                 - Model artifacts storage
✓ tests/                  - Unit & integration tests
✓ scripts/                - Utility scripts
✓ logs/                   - Application logs
```

### 2️⃣ Configuration Files
```
✓ requirements.txt        - Data engineering dependencies
✓ requirements-ml.txt     - ML training dependencies  
✓ requirements-api.txt    - API production dependencies
✓ .env.example           - Environment variables template
✓ .gitignore             - Git ignore patterns
```

### 3️⃣ Core Implementation
```
✓ training_pipeline/1_ocr_extraction.py   - OCR extraction script (READY TO RUN)
✓ app/services/llm_service.py             - Ollama integration service
✓ app/core/config.py                      - Settings management
✓ app/core/grading_schema.py              - 8-category rubric definition
```

### 4️⃣ Documentation
```
✓ README.md              - Comprehensive project documentation
✓ setup_env.ps1          - Automated environment setup script
✓ scripts/verify_setup.py - Environment verification script
```

---

## 🚀 Getting Started (3 Steps)

### Step 1: Set Up Virtual Environment

**Option A: Automated (Recommended)**
```powershell
# Run the setup script
.\setup_env.ps1
```

**Option B: Manual**
```powershell
# Create virtual environment
python -m venv .venv

# Activate it
.\.venv\Scripts\Activate.ps1

# Install dependencies (choose one)
pip install -r requirements.txt        # For OCR extraction
pip install -r requirements-api.txt    # For API development
```

---

### Step 2: Configure Environment

```powershell
# Copy environment template
cp .env.example .env

# Edit with your settings (optional, defaults work for most cases)
notepad .env
```

**Key settings:**
- `OLLAMA_BASE_URL`: Default is `http://localhost:11434`
- `OLLAMA_MODEL_NAME`: Default is `qwen2.5:7b`
- `TESSERACT_CMD`: Path to Tesseract executable

---

### Step 3: Verify Setup

```powershell
# Run verification script
python scripts/verify_setup.py
```

**This checks:**
- ✓ Python version (3.10+)
- ✓ Tesseract OCR installation
- ✓ Ollama server status
- ✓ PDF files availability
- ✓ Environment configuration

---

## 📝 Priority Task: Run OCR Extraction

**This is the first task to process the 80 Supreme Court PDFs:**

```powershell
# Ensure virtual environment is activated
.\.venv\Scripts\Activate.ps1

# Run OCR extraction
python training_pipeline/1_ocr_extraction.py
```

**Expected output:**
```
============================================================
OCR Extraction Pipeline Started
============================================================
Found 80 PDF files in data\raw_pdfs
Processing PDFs: 100%|████████████████████| 80/80 [45:30<00:00]

Summary: 78/80 files processed successfully
============================================================
```

**Output location:**
- Extracted text: `data/processed_text/*.txt`
- Metadata log: `data/metadata/ocr_extraction_*.json`

---

## 🔧 Troubleshooting

### Issue: Virtual environment activation fails

**Error:**
```
.\\.venv\Scripts\Activate.ps1 : cannot be loaded because running scripts is disabled
```

**Solution:**
```powershell
# Allow script execution (run as Administrator)
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

### Issue: Tesseract not found

**Error:**
```
pytesseract.pytesseract.TesseractNotFoundError
```

**Solution:**
1. Download Tesseract: https://github.com/UB-Mannheim/tesseract/wiki
2. During installation, select **Sinhala language pack**
3. Update `.env` file with correct path:
   ```ini
   TESSERACT_CMD=C:\Program Files\Tesseract-OCR\tesseract.exe
   ```

---

### Issue: Ollama connection refused

**Error:**
```
httpx.ConnectError: Connection refused
```

**Solution:**
```powershell
# Start Ollama server
ollama serve

# Pull Qwen model (if not already done)
ollama pull qwen2.5:7b

# Verify it's running
ollama list
```

---

## 📊 Project Roadmap

### Phase 1: Data Engineering ⏳ (Current)
- [x] Project scaffolding
- [x] OCR extraction script
- [ ] Run OCR on all 80 PDFs
- [ ] Verify extraction quality

### Phase 2: Dataset Preparation
- [ ] Implement `2_dataset_generation.py`
- [ ] Generate synthetic training data
- [ ] Create train/validation/test splits

### Phase 3: Model Fine-Tuning
- [ ] Implement `3_fine_tune_unsloth.py`
- [ ] Fine-tune Qwen2.5 on Google Colab
- [ ] Evaluate model performance

### Phase 4: API Development
- [ ] Implement FastAPI endpoints
- [ ] Integrate Ollama service
- [ ] Add request/response validation
- [ ] Create API documentation

### Phase 5: Testing & Deployment
- [ ] Unit tests
- [ ] Integration tests
- [ ] Docker containerization
- [ ] Production deployment

---

## 📚 Additional Resources

- **README.md**: Comprehensive documentation
- **app/core/grading_schema.py**: Rubric definition and scoring logic
- **app/services/llm_service.py**: Ollama integration examples
- **.env.example**: All configuration options

---

## 💡 Tips

1. **Start with OCR**: Process the PDFs first to build the training dataset
2. **Check logs**: All operations log to `logs/` directory
3. **Verify Ollama**: Always ensure Ollama is running before API calls
4. **Use virtual environment**: Always activate `.venv` before running scripts

---

## ❓ Need Help?

- Review [README.md](README.md) for detailed documentation
- Check logs in `logs/` directory
- Run verification: `python scripts/verify_setup.py`
- Open an issue on GitHub

---

**Ready to begin? Run the OCR extraction script! 🚀**

```powershell
python training_pipeline/1_ocr_extraction.py
```
