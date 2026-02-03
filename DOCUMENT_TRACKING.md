# Document Tracking & Smart Updates

## Overview

The knowledge base builder now tracks source document metadata and only updates wiki articles when the source document has been modified. This prevents redundant processing and maintains accurate version information.

---

## How It Works

### 1. **Document Metadata Extraction**

When processing a Word document, the system extracts:

```python
{
    "author": "Document author",
    "created": "2024-01-15T10:30:00",
    "modified": "2024-03-20T14:45:00",
    "last_modified_by": "Last editor",
    "revision": "5",
    "title": "Document title",
    "subject": "Document subject",
    "keywords": "comma, separated, keywords"
}
```

### 2. **YAML Front Matter**

All generated wiki articles include source document metadata:

```yaml
---
title: "Git"
type: "Product Overview"
product: "Git"
date_updated: "2026-02-03"
source_document_author: "Chris Garcia"
source_document_modified: "2020-07-15T14:30:00"
source_document_title: "Git Repository Workflow"
---
```

### 3. **Smart Update Logic**

When processing a document:

1. **Check if article exists**: Look for existing `overview.md`
2. **Compare dates**: Read `source_document_modified` from existing article
3. **Decision**:
   - If source document is **newer** → Update the article
   - If source document is **same or older** → Skip (save time and API costs)
   - If article doesn't exist → Create new article

**Console Output**:
```
[SKIP] overview.md - existing article is up-to-date (source: 2020-07-15T14:30:00)
```
or
```
[OK] Saved: overview.md
```

---

## Benefits

### 1. **Cost Savings**
- Skips processing documents that haven't changed
- Saves API calls and costs
- Faster batch processing

### 2. **Version Tracking**
- Know which document version was used
- Track when knowledge was last updated
- Maintain audit trail

### 3. **Incremental Updates**
- Process only changed documents
- Re-run on entire directory without wasting resources
- Efficient continuous integration

### 4. **Quality Assurance**
- See who authored the source document
- Know when it was last modified
- Track document lifecycle

---

## Usage Examples

### Example 1: Initial Processing

```bash
python knowledge_base_builder_kimi.py -d ./documents -o wiki
```

**First Run**:
```
[Processing] Product: Git
   [Saving] Files for Git...
      [OK] Saved: wiki/Products/Git/overview.md
```

**Second Run (no changes)**:
```
[Processing] Product: Git
   [Saving] Files for Git...
      [SKIP] overview.md - existing article is up-to-date
```

**After Document Update**:
```
[Processing] Product: Git
   [Saving] Files for Git...
      [OK] Saved: wiki/Products/Git/overview.md  (updated)
```

### Example 2: Viewing Article Metadata

Check a wiki article's YAML front matter:

```bash
head -20 wiki/Products/Git/overview.md
```

Output:
```yaml
---
title: "Git"
type: "Product Overview"
product: "Git"
date_updated: "2026-02-03"
source_document_author: "Chris Garcia, Systems Engineer"
source_document_modified: "2020-07-15T14:30:00"
source_document_title: "Git Repository Administration"
---

# Git

*Source document last modified: 2020-07-15*

Git is a distributed version control system...
```

---

## Implementation Details

### Document Property Extraction

Uses `python-docx` core properties:

```python
doc_props = doc.core_properties
doc_metadata = {
    "author": doc_props.author,
    "modified": doc_props.modified.isoformat(),
    "created": doc_props.created.isoformat(),
    # ... more properties
}
```

### Update Check Logic

```python
# Check if file exists and compare dates
if knowledge_file.exists() and doc_metadata.get('modified'):
    # Read existing YAML front matter
    match = re.search(r'source_document_modified:\s*"?([^"\n]+)"?', content)
    if match:
        existing_date = match.group(1)
        new_date = doc_metadata['modified']
        if existing_date >= new_date:
            # Skip - existing is up-to-date
            should_update = False
```

### Metadata Fields in YAML

**Product Overview**:
- `title`: Product name
- `type`: "Product Overview"
- `product`: Product identifier
- `date_updated`: When wiki was generated
- `source_document_author`: Original document author
- `source_document_modified`: Source document last modified date
- `source_document_title`: Original document title

**Reference Materials**:
- `title`: Article title
- `type`: Knowledge type (HOW_TO, CONFIGURATION, etc.)
- `category`: Technical category
- `product`: Related product
- `source_document`: Document type
- `source_document_author`: Original author
- `source_document_modified`: Source modified date
- `date_extracted`: When extracted
- `tags`: Searchable tags

---

## Configuration

No additional configuration needed! Document tracking works automatically once you update to the latest version.

### Environment Variables

Uses existing configuration:
```env
COMPANY_NAME=SGC Australia
COMPANY_FORMER_NAME=SG Controls
# ... other settings
```

---

## Advanced Usage

### Force Update All Articles

To force update all articles regardless of dates:

**Option 1**: Delete existing output directory
```bash
rm -rf wiki
python knowledge_base_builder_kimi.py -d ./documents -o wiki
```

**Option 2**: Use a new output directory
```bash
python knowledge_base_builder_kimi.py -d ./documents -o wiki_v2
```

### Check Which Documents Need Updates

Before processing, check document dates:

```bash
# List document modification dates
stat -c '%y %n' documents/*.docx | sort
```

### Audit Trail Queries

Search for articles from specific authors:
```bash
grep -r "source_document_author: \"Chris Garcia\"" wiki/
```

Find recently updated source documents:
```bash
grep -r "source_document_modified: \"2024" wiki/
```

---

## Troubleshooting

### Issue: Articles Always Updating

**Possible Causes**:
1. Document modified date changes each time opened (Word auto-save)
2. Document properties not preserved
3. Existing YAML corrupted

**Solution**:
- Check document properties: Right-click document → Properties → Details
- Ensure "Save preview picture" and "Save thumbnail" are disabled in Word
- Manually check YAML front matter for corruption

### Issue: Articles Never Updating

**Possible Causes**:
1. Date comparison logic issue
2. YAML parsing error

**Debug**:
```python
# Add debug output
print(f"Existing date: {existing_date}")
print(f"New date: {new_date}")
print(f"Should update: {should_update}")
```

---

## Future Enhancements

Potential improvements:

1. **Version History**: Track multiple versions of same article
2. **Change Diff**: Show what changed between versions
3. **Selective Update**: Update only specific sections
4. **Batch Report**: Generate report of what was updated/skipped
5. **Date Override**: Command-line flag to force updates

---

## Summary

Document tracking provides:

✅ **Smart updates** - Only process changed documents
✅ **Version control** - Track source document versions
✅ **Cost savings** - Reduce unnecessary API calls
✅ **Audit trail** - Know who created what and when
✅ **Quality tracking** - Monitor document lifecycle
✅ **Automatic** - No configuration needed

The system intelligently manages your knowledge base, ensuring it stays current without wasting resources on unchanged documents.

---

**Status**: Active and working in production! 🚀
