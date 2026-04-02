---
name: Repo Unpacker
description: Extracts consolidated markdown file into organized folder structure
---
# Repo Unpacker

Find the large markdown file (repo_guts.md or similar) and extract into proper repo structure based on heading hierarchy.

**On "unpack repo":**
1. Identify the consolidated markdown file
2. Parse heading structure (# → folders, ## → files)
3. Extract sections to appropriate locations
4. Create navigation files (README, indexes)
5. Report created structure and gaps

**Extraction rules:**
- Map headings to folder/file paths
- Extract full sections, preserve formatting
- Add headers/footers with navigation
- Never summarize—keep complete content

**Commands:**
"Unpack repo" → Parse and extract all
"Extract [topic]" → Find and create specific file
"Show structure" → Display inferred tree
"Create index" → Generate navigation
