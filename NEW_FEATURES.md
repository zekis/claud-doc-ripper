# New Features Added

## 1. Enhanced Tool Call Visibility

All AI tool calls now show timestamped progress in the console:

```
[12:34:56] [TOOL CALL] get_section_by_index(1)
[12:34:56] [RETRIEVED] Section 1: Introduction

[12:35:08] [TOOL CALL] get_section_by_heading('Git')
[12:35:08] [RETRIEVED] Section 3: Standard Operations

[12:35:20] [TOOL CALL] get_multiple_sections([5, 6, 7])
[12:35:20] [RETRIEVED] 3/3 sections
```

This lets you see:
- **When** each tool call happens (timestamp)
- **What** section is being retrieved
- **Progress** - you can see it's working, not stuck

## 2. Select Single Document by Number

When using `--dir` mode, you can now select a specific document by entering its number:

### Example:

```bash
python knowledge_base_builder.py -d . -r -o test
```

**Output:**
```
======================================================================
KNOWLEDGE BASE BUILDER - BATCH MODE
======================================================================
Scan Directory: .
Recursive: Yes
======================================================================

[Scanning] Recursively for .docx files...
[OK] Found 5 document(s) to process:

   1. BMX-MAN-0.09-Using Git.docx
   2. Project Specification.docx
   3. User Guide.docx
   4. Technical Manual.docx
   5. Installation Guide.docx

======================================================================
Process all 5 document(s)? (y=yes all, n=no, e=each, or enter number): 
```

**Options:**
- `y` - Process all 5 documents
- `n` - Cancel
- `e` - Ask for each document individually
- `1` - Process ONLY document #1 (BMX-MAN-0.09-Using Git.docx)
- `3` - Process ONLY document #3 (User Guide.docx)

### Use Cases:

**Test a single document:**
```bash
python knowledge_base_builder.py -d /path/to/docs -r
# When prompted, enter: 1
```

**Process specific document from a large set:**
```bash
python knowledge_base_builder.py -d /large/folder -r
# Scan shows 100 documents
# Enter: 42  (to process only document #42)
```

## Benefits

✅ **Better visibility** - See exactly what the AI is doing in real-time  
✅ **Faster testing** - Test single documents without processing entire folders  
✅ **More control** - Pick specific documents from scan results  
✅ **Progress tracking** - Timestamps show it's working, not stuck  

## Performance Note

Each tool call takes ~12 seconds due to Auggie SDK overhead. This is expected behavior.
For a document where the AI retrieves 5-10 sections, expect 1-2 minutes of processing time.
The timestamped output lets you see progress and confirm it's not stuck in a loop.

