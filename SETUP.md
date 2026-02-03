# Setup Guide - Knowledge Base Builder (Kimi 2.5)

## Quick Start

### 1. Create Virtual Environment (Already Done ✅)
```bash
python -m venv venv
```

### 2. Activate Virtual Environment

**Windows (Command Prompt):**
```bash
venv\Scripts\activate
```

**Windows (PowerShell):**
```powershell
venv\Scripts\Activate.ps1
```

**Linux/Mac:**
```bash
source venv/bin/activate
```

You should see `(venv)` prefix in your terminal when activated.

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

This will install:
- `openai>=1.0.0` - For Moonshot API access
- `python-docx>=1.1.0` - For Word document processing
- `python-dotenv>=1.0.0` - For loading `.env` configuration

### 4. Configure API Key

**Copy the example file:**
```bash
cp .env.example .env
```

**Windows (if cp doesn't work):**
```bash
copy .env.example .env
```

**Edit `.env` and add your Moonshot API key:**
```
MOONSHOT_API_KEY=your_actual_api_key_here
MOONSHOT_BASE_URL=https://api.moonshot.cn/v1
```

Get your API key from: https://platform.moonshot.cn/console/api-keys

### 5. Test Installation

**Run unit tests (no API key needed):**
```bash
python test_kimi_json_parsing.py
```

Expected output:
```
JSON PARSING HELPER FUNCTION TESTS
[PASS] Plain JSON
[PASS] JSON with markdown code fences
...
SUMMARY: Passed: 10, Failed: 0, Total: 10
```

**Test API connection (requires API key):**
```bash
python test_kimi_simple_function.py
```

### 6. Start Using

**Process a single document:**
```bash
python knowledge_base_builder_kimi.py "your_document.docx" -o output_folder
```

**Process a directory:**
```bash
python knowledge_base_builder_kimi.py -d ./documents -o output_folder
```

**Process recursively:**
```bash
python knowledge_base_builder_kimi.py -d ./documents -r -o output_folder
```

---

## Troubleshooting

### Virtual Environment Not Activating (PowerShell)

If you get an execution policy error on Windows PowerShell:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Missing API Key Error

```
[ERROR] MOONSHOT_API_KEY environment variable is not set
```

**Solution:** Make sure you created `.env` file with your API key:
```bash
# Check if .env exists
ls .env

# If not, create it
copy .env.example .env
# Then edit .env and add your API key
```

### Module Not Found Errors

```
ModuleNotFoundError: No module named 'openai'
```

**Solution:** Make sure virtual environment is activated and dependencies installed:
```bash
# Activate venv first
venv\Scripts\activate

# Then install dependencies
pip install -r requirements.txt
```

### Document Not Found

```
[ERROR] Document not found: document.docx
```

**Solution:** Use absolute or relative path:
```bash
python knowledge_base_builder_kimi.py "C:\path\to\document.docx" -o output
```

---

## Complete Setup Checklist

- [ ] Virtual environment created (`python -m venv venv`)
- [ ] Virtual environment activated (see `(venv)` prefix)
- [ ] Dependencies installed (`pip install -r requirements.txt`)
- [ ] `.env` file created from `.env.example`
- [ ] Moonshot API key added to `.env`
- [ ] Tests passing (`python test_kimi_json_parsing.py`)
- [ ] Ready to process documents!

---

## Directory Structure

```
claud-doc-ripper/
├── venv/                          # Virtual environment (git-ignored)
├── .env                           # Your API key (git-ignored)
├── .env.example                   # Template for .env
├── knowledge_base_builder_kimi.py # Main application
├── requirements.txt               # Python dependencies
├── test_kimi_json_parsing.py     # Unit tests
├── test_kimi_simple_function.py  # Integration tests
├── test_kimi_tool_performance.py # Performance tests
├── SETUP.md                       # This file
├── CODE_REVIEW_FIXES.md          # Change log
└── COMPLETION_SUMMARY.md         # Summary of improvements
```

---

## Next Steps

After setup is complete:

1. **Test with a sample document** to verify everything works
2. **Check output quality** - compare with your expectations
3. **Monitor API costs** - Kimi is much cheaper than Auggie SDK
4. **Process your document collection** - build your knowledge base!

---

## Deactivating Virtual Environment

When you're done working:
```bash
deactivate
```

## Reactivating Later

Next time you work on the project:
```bash
cd e:\AIResearch\claud-doc-ripper
venv\Scripts\activate
```

That's it! You're ready to go. 🚀
