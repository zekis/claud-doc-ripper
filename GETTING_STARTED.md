# Getting Started with Wiki Article Creator

Welcome! This guide will help you get up and running quickly.

## 📋 What You'll Need

- **Python 3.10+** installed on your system
- **Node.js and npm** (for Augment CLI)
- **Word documents** (.docx format) to process
- **Augment account** (free to create)

## 🚀 Installation (5 minutes)

### Step 1: Install Augment CLI

```bash
npm install -g @augmentcode/auggie@prerelease
```

### Step 2: Login to Augment

```bash
auggie login
```

This will open your browser to authenticate. Follow the prompts.

### Step 3: Install Python Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Verify Installation

```bash
python example_usage.py
```

If you see a list of AI models, you're ready to go! ✅

## 🎯 Your First Extraction

### Quick Test

```bash
python wiki_article_creator.py your_document.docx
```

Replace `your_document.docx` with your actual Word document.

### What Happens?

The tool will:
1. 📖 Read your Word document
2. 🤖 Analyze it with AI
3. 📝 Extract three types of information:
   - **Document Structure** - How to create similar documents
   - **Product Knowledge** - Info about products (Insight CM, SMS, QMS)
   - **Client Information** - Client-specific details
4. 📄 Generate organized markdown articles

### Check Your Output

Look in the `wiki_output` directory:

```
wiki_output/
├── document_structure/     ← How-to guides
├── product_knowledge/      ← Product documentation
└── client_information/     ← Client details
```

## 📚 What Gets Extracted?

### 1. Document Structure Articles

**Purpose**: Create reusable templates and guides

**Output**:
- `overview.md` - Document type, structure, key components
- `chapter_*.md` - How to write each section
- `best_practices.md` - Guidelines and tips

**Example**: If you process a user manual, you'll get a guide on how to write user manuals.

### 2. Product Knowledge Articles

**Purpose**: Build a product knowledge base

**Output**: Separate folders for each product with:
- Product description
- Features and capabilities
- Use cases
- Technical details

**Example**: Information about "Insight CM" extracted from multiple documents, all in one place.

### 3. Client Information Articles

**Purpose**: Centralize client-specific data

**Output**: One file per client with:
- Client name and addresses
- Hardware specifications
- Configuration details
- Contact information

**Example**: All hardware and config details for "Acme Corp" in one document.

## 🎨 Common Workflows

### Workflow 1: Process Multiple Documents

```bash
python wiki_article_creator.py doc1.docx doc2.docx doc3.docx
```

Or use wildcards:
```bash
python wiki_article_creator.py *.docx
```

### Workflow 2: Build Product Knowledge Base

```bash
# Process all product manuals
python wiki_article_creator.py manuals/*.docx --output product_wiki

# Check product_knowledge/ folder for consolidated info
```

### Workflow 3: Extract Client Database

```bash
# Process all client documents
python wiki_article_creator.py clients/*.docx --output client_db

# Check client_information/ folder for all client details
```

### Workflow 4: Create Documentation Templates

```bash
# Process your best documents
python wiki_article_creator.py best_manual.docx --output templates

# Check document_structure/ for how-to guides
```

## ⚙️ Customization

### Use Different AI Models

```bash
# Faster processing (good for testing)
python wiki_article_creator.py doc.docx --model haiku4.5

# Best quality (default)
python wiki_article_creator.py doc.docx --model sonnet4.5
```

### Custom Output Directory

```bash
python wiki_article_creator.py doc.docx --output my_wiki
```

### Programmatic Usage

```python
from wiki_article_creator import WikiArticleCreator

# Create instance
creator = WikiArticleCreator(
    output_dir="my_wiki",
    model="sonnet4.5"
)

# Process document
creator.process_document("document.docx")

# Or extract specific information
content = creator.read_word_document("document.docx")
products = creator.extract_product_knowledge(content)
```

## 💡 Tips for Best Results

1. **Start Small**: Test with 1-2 documents first
2. **Clean Documents**: Remove unnecessary formatting
3. **Clear Structure**: Documents with clear headings work best
4. **Review Output**: Always review AI-generated content
5. **Iterate**: Adjust and reprocess as needed

## 🔍 Understanding the Output

### Document Structure Articles

These help you create similar documents in the future:
- What type of document it is
- How to structure it
- What to include in each section
- Best practices

### Product Knowledge Articles

These build your product documentation:
- Consolidated from multiple sources
- Generalized (client info removed)
- Organized by product
- Easy to search and update

### Client Information Articles

These centralize client data:
- All client details in one place
- Hardware and configuration
- Contact information
- Easy reference

## 🛠️ Troubleshooting

### "Command not found: auggie"

Install Augment CLI:
```bash
npm install -g @augmentcode/auggie@prerelease
```

### "Not authenticated"

Login to Augment:
```bash
auggie login
```

### "No module named 'docx'"

Install dependencies:
```bash
pip install -r requirements.txt
```

### Processing is slow

Use faster model:
```bash
python wiki_article_creator.py doc.docx --model haiku4.5
```

### Output is not accurate

- Try the more capable model: `--model sonnet4.5`
- Ensure document has clear structure
- Check that document is in .docx format

## 📖 Next Steps

1. ✅ Process your first document
2. 📚 Read the [README.md](README.md) for detailed documentation
3. 🔧 Check [config_example.py](config_example.py) for customization options
4. 💻 Review [example_usage.py](example_usage.py) for code examples
5. 🏗️ Read [PROJECT_OVERVIEW.md](PROJECT_OVERVIEW.md) for architecture details

## 🤝 Need Help?

- **Augment SDK**: https://docs.augmentcode.com
- **python-docx**: https://python-docx.readthedocs.io
- **This tool**: Check the README.md and examples

---

**Ready to extract knowledge from your documents? Let's go! 🚀**

