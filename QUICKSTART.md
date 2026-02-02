# Quick Start Guide

Get started with the Wiki Article Creator in 5 minutes!

## Step 1: Install Prerequisites

### Install Augment CLI

```bash
npm install -g @augmentcode/auggie@prerelease
```

### Login to Augment

```bash
auggie login
```

Follow the prompts to authenticate.

## Step 2: Install Python Dependencies

```bash
pip install -r requirements.txt
```

This installs:
- `auggie-sdk` - Augment's Python SDK
- `python-docx` - Word document reader

## Step 3: Run Your First Extraction

```bash
python wiki_article_creator.py your_document.docx
```

Replace `your_document.docx` with the path to your Word document.

## Step 4: Check the Output

The tool creates a `wiki_output` directory with three folders:

```
wiki_output/
├── document_structure/    # How-to guides for creating similar documents
├── product_knowledge/     # Information about products (Insight CM, SMS, QMS)
└── client_information/    # Client-specific details
```

## What Happens During Processing?

1. 📖 **Reads** your Word document (text, headings, tables)
2. 📋 **Analyzes** document structure and hierarchy
3. 📝 **Creates** generalized how-to guides
4. 🔍 **Extracts** product knowledge (removes client-specific info)
5. 👤 **Captures** client information separately
6. 📄 **Generates** organized markdown articles

## Common Use Cases

### Process Multiple Documents

```bash
python wiki_article_creator.py doc1.docx doc2.docx doc3.docx
```

### Use Custom Output Directory

```bash
python wiki_article_creator.py document.docx --output my_wiki
```

### Use Faster Model (for quick testing)

```bash
python wiki_article_creator.py document.docx --model haiku4.5
```

## Verify Installation

Run the example script to check everything is working:

```bash
python example_usage.py
```

This will list available AI models. If you see a list of models, you're all set! ✅

## Next Steps

- Read the full [README.md](README.md) for detailed documentation
- Customize the data classes for your specific needs
- Adjust AI prompts to extract different information
- Process your document library!

## Troubleshooting

### Error: "auggie not found"

Make sure Node.js and npm are installed, then:
```bash
npm install -g @augmentcode/auggie@prerelease
```

### Error: "Not authenticated"

Login to Augment:
```bash
auggie login
```

### Error: "No module named 'docx'"

Install dependencies:
```bash
pip install -r requirements.txt
```

### Processing is slow

Use the faster Haiku model:
```bash
python wiki_article_creator.py document.docx --model haiku4.5
```

## Need Help?

- Check the [README.md](README.md) for detailed documentation
- Review [example_usage.py](example_usage.py) for code examples
- Visit https://docs.augmentcode.com for Augment SDK documentation

---

**Ready to extract knowledge from your documents? Let's go! 🚀**

