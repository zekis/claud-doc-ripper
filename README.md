# Wiki Article Creator

A Python tool that uses the Augment SDK to extract knowledge from Word documents and create organized wiki articles.

## Features

This tool processes Word documents and automatically creates three types of wiki articles:

### 1. 📋 Document Structure Articles
- **Overview**: Document type, key components, and structure
- **Chapter Guides**: How to write each chapter/section
- **Best Practices**: Guidelines and templates for creating similar documents

### 2. 🔍 Product Knowledge Articles
Extracts and documents information about company products:
- Insight CM
- SMS (Safety Management System)
- QMS (Quality Management System)
- Any other products mentioned

For each product, captures:
- Description and purpose
- Features and capabilities
- Use cases
- Technical details

### 3. 👤 Client Information Articles
Extracts client-specific details:
- Client names
- Addresses and locations
- Hardware specifications
- Configuration details
- Contact information

## Installation

### Prerequisites

1. **Python 3.10 or higher**
   ```bash
   python --version
   ```

2. **Augment CLI (auggie)**
   ```bash
   npm install -g @augmentcode/auggie@prerelease
   auggie login
   ```

### Install Dependencies

```bash
pip install -r requirements.txt
```

This installs:
- `auggie-sdk` - Augment's Python SDK
- `python-docx` - For reading Word documents

## Usage

### Basic Usage

Process a single Word document:

```bash
python wiki_article_creator.py document.docx
```

### Advanced Options

```bash
# Custom output directory
python wiki_article_creator.py document.docx --output my_wiki

# Use a different AI model (faster but less capable)
python wiki_article_creator.py document.docx --model haiku4.5

# Process multiple documents at once
python wiki_article_creator.py doc1.docx doc2.docx doc3.docx

# Combine options
python wiki_article_creator.py *.docx --output company_wiki --model sonnet4.5
```

### Available Models

- `sonnet4.5` (default) - Most capable, best quality
- `haiku4.5` - Faster, more economical
- `opus4.5` - Most powerful (if available)

List all available models:
```python
from auggie_sdk import Auggie
models = Auggie.get_available_models()
for model in models:
    print(f"{model.id}: {model.name}")
```

## Output Structure

The tool creates the following directory structure:

```
wiki_output/
├── document_structure/
│   └── [document_name]/
│       ├── overview.md
│       ├── chapter_1_introduction.md
│       ├── chapter_2_methodology.md
│       └── best_practices.md
├── product_knowledge/
│   ├── insight_cm/
│   │   └── [document_name]_knowledge.md
│   ├── sms/
│   │   └── [document_name]_knowledge.md
│   └── qms/
│       └── [document_name]_knowledge.md
└── client_information/
    └── [client_name]_[document_name].md
```

## How It Works

1. **Read Document**: Extracts text, headings, and tables from Word document
2. **Analyze Structure**: Uses AI to identify document structure and hierarchy
3. **Create How-To Guide**: Generates generalized guide for creating similar documents
4. **Extract Products**: Identifies and documents product information
5. **Extract Client Info**: Captures all client-specific details
6. **Generate Articles**: Creates organized markdown files

## Example Output

### Document Structure Article
```markdown
# User Manual - Overview

## Document Type: Technical Manual

### Overview
This manual provides comprehensive guidance for system administrators...

### Key Components
- Installation procedures
- Configuration guidelines
- Troubleshooting steps
```

### Product Knowledge Article
```markdown
# Insight CM

## Description
Insight CM is a condition monitoring system that...

## Features
- Real-time vibration monitoring
- Predictive maintenance alerts
- Integration with SCADA systems
```

### Client Information Article
```markdown
# Client Information - Acme Corporation

## Hardware
- 24x Vibration Sensors (Model VS-2000)
- 2x Data Acquisition Units (DAU-500)
```

## Customization

### Modify Data Classes

Edit the dataclasses in `wiki_article_creator.py` to capture different information:

```python
@dataclass
class ProductKnowledge:
    product_name: str
    description: str
    # Add your custom fields here
    pricing: Optional[str] = None
    support_contact: Optional[str] = None
```

### Adjust AI Prompts

Modify the prompts in the extraction methods to focus on specific information:

```python
def extract_product_knowledge(self, content: str) -> List[ProductKnowledge]:
    # Customize this prompt to extract what you need
    products = session.run(
        f"""Extract product information focusing on:
        - Technical specifications
        - Pricing models
        - Support requirements
        ...
        """,
        return_type=List[ProductKnowledge]
    )
```

## Troubleshooting

### "auggie not found"
Make sure Augment CLI is installed and in your PATH:
```bash
npm install -g @augmentcode/auggie@prerelease
```

### "Not authenticated"
Login to Augment:
```bash
auggie login
```

### "Module not found: docx"
Install dependencies:
```bash
pip install -r requirements.txt
```

### Processing takes too long
Try using a faster model:
```bash
python wiki_article_creator.py document.docx --model haiku4.5
```

## Tips for Best Results

1. **Clean Documents**: Remove unnecessary formatting before processing
2. **Consistent Structure**: Documents with clear headings work best
3. **Batch Processing**: Process related documents together for consistency
4. **Review Output**: Always review AI-generated content for accuracy
5. **Iterative Refinement**: Adjust prompts based on your specific needs

## License

MIT License - Feel free to modify and use for your needs!

## Contributing

Contributions welcome! Feel free to:
- Add new extraction types
- Improve prompts
- Add output formats (HTML, PDF, etc.)
- Enhance error handling

## Support

For issues with:
- **Augment SDK**: https://github.com/augmentcode/auggie/issues
- **This tool**: Create an issue in your repository

