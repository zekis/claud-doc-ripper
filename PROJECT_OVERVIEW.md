# Wiki Article Creator - Project Overview

## 🎯 Purpose

This tool automatically extracts knowledge from Word documents and creates organized wiki articles using Augment's AI SDK. It's designed to:

1. **Generalize documentation** - Remove client-specific information and create reusable how-to guides
2. **Extract product knowledge** - Document information about products like Insight CM, SMS, QMS
3. **Capture client details** - Separately store client-specific information for reference

## 📁 Project Structure

```
claud-doc-ripper/
├── wiki_article_creator.py    # Main application
├── example_usage.py            # Usage examples
├── requirements.txt            # Python dependencies
├── README.md                   # Full documentation
├── QUICKSTART.md              # Quick start guide
├── PROJECT_OVERVIEW.md        # This file
└── .gitignore                 # Git ignore rules
```

## 🔧 Technology Stack

- **Python 3.10+** - Core language
- **auggie-sdk** - Augment's Python SDK for AI interactions
- **python-docx** - Word document processing
- **Dataclasses** - Type-safe data structures
- **Augment CLI** - Backend AI agent

## 🏗️ Architecture

### Data Models

```python
DocumentStructure    # Document organization and hierarchy
HowToGuide          # Generalized creation guide
ProductKnowledge    # Product-specific information
ClientInformation   # Client-specific details
```

### Processing Pipeline

```
Word Document
    ↓
Read & Parse (python-docx)
    ↓
Extract Structure (Auggie AI)
    ↓
Create How-To Guide (Auggie AI)
    ↓
Extract Products (Auggie AI)
    ↓
Extract Client Info (Auggie AI)
    ↓
Generate Markdown Articles
    ↓
Organized Wiki Output
```

### Output Organization

```
wiki_output/
├── document_structure/
│   └── [doc_name]/
│       ├── overview.md
│       ├── chapter_*.md
│       └── best_practices.md
├── product_knowledge/
│   ├── insight_cm/
│   ├── sms/
│   └── qms/
└── client_information/
    └── [client]_[doc].md
```

## 🎨 Key Features

### 1. Intelligent Structure Extraction
- Identifies document type (manual, guide, specification)
- Extracts heading hierarchy
- Recognizes key components
- Analyzes section organization

### 2. Generalization
- Removes client-specific examples
- Creates reusable templates
- Generates best practices
- Provides writing guidelines

### 3. Product Knowledge Extraction
- Identifies product mentions
- Extracts features and capabilities
- Documents use cases
- Captures technical details

### 4. Client Information Capture
- Extracts names and addresses
- Documents hardware specifications
- Captures configuration details
- Stores contact information

### 5. Flexible AI Models
- Sonnet 4.5 (default) - Best quality
- Haiku 4.5 - Faster processing
- Opus 4.5 - Maximum capability

## 🚀 Usage Patterns

### Command Line

```bash
# Single document
python wiki_article_creator.py document.docx

# Multiple documents
python wiki_article_creator.py *.docx

# Custom options
python wiki_article_creator.py doc.docx --output wiki --model haiku4.5
```

### Programmatic

```python
from wiki_article_creator import WikiArticleCreator

creator = WikiArticleCreator(output_dir="wiki", model="sonnet4.5")
creator.process_document("document.docx")
```

### Batch Processing

```python
from pathlib import Path

creator = WikiArticleCreator()
for doc in Path("documents").glob("*.docx"):
    creator.process_document(str(doc))
```

## 🔄 Workflow Integration

### Typical Use Cases

1. **Documentation Standardization**
   - Process existing client documents
   - Extract reusable patterns
   - Create standard templates

2. **Knowledge Base Creation**
   - Extract product information
   - Build searchable wiki
   - Maintain product documentation

3. **Client Database**
   - Centralize client information
   - Track hardware deployments
   - Document configurations

## 🛠️ Customization Points

### 1. Data Models
Modify dataclasses to capture different information:
```python
@dataclass
class ProductKnowledge:
    # Add custom fields
    pricing: Optional[str] = None
    certifications: List[str] = field(default_factory=list)
```

### 2. AI Prompts
Adjust extraction prompts for specific needs:
```python
def extract_product_knowledge(self, content: str):
    # Customize prompt
    products = session.run(
        f"""Focus on extracting: pricing, support, certifications...""",
        return_type=List[ProductKnowledge]
    )
```

### 3. Output Format
Change markdown generation:
```python
def write_markdown_file(self, filepath, title, content):
    # Add custom formatting, headers, footers
```

## 📊 Performance Considerations

- **Model Selection**: Haiku 4.5 is 3-5x faster than Sonnet 4.5
- **Document Size**: Large documents (>50 pages) may take several minutes
- **Batch Processing**: Process documents sequentially to avoid rate limits
- **Session Management**: Uses sessions for context continuity

## 🔐 Security & Privacy

- Client information is extracted separately
- No data is stored by Augment beyond session
- All processing happens locally via CLI
- Output is stored only in specified directory

## 🧪 Testing

Run examples to verify installation:
```bash
python example_usage.py
```

Test with sample document:
```bash
python wiki_article_creator.py sample.docx --output test_output
```

## 📈 Future Enhancements

Potential improvements:
- [ ] Support for PDF documents
- [ ] HTML output format
- [ ] Database integration
- [ ] Web interface
- [ ] Incremental updates
- [ ] Version control integration
- [ ] Multi-language support
- [ ] Custom extraction rules
- [ ] Template library

## 🤝 Contributing

To extend this tool:
1. Add new data models for different extraction types
2. Create custom extraction methods
3. Add new output formats
4. Improve error handling
5. Add unit tests

## 📚 Resources

- [Augment SDK Documentation](https://docs.augmentcode.com)
- [python-docx Documentation](https://python-docx.readthedocs.io)
- [Augment CLI](https://github.com/augmentcode/auggie)

## 💡 Tips

1. Start with small documents to test
2. Review AI output for accuracy
3. Adjust prompts based on your documents
4. Use faster models for iteration
5. Process related documents together
6. Keep original documents as backup

---

**Built with ❤️ using Augment SDK**

