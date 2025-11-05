# ChatGPT Thread Extractor

A Python tool to extract individual conversations from ChatGPT's exported conversation data into readable text files.

## Overview

This tool parses the large `conversations.json` file exported from ChatGPT and extracts each conversation into a separate text file. Each file is named with the conversation's creation date, update date, and title for easy organization and reference.

## Features

- Extracts all conversations from ChatGPT export data
- Creates individual text files for each conversation
- Intelligent filename generation: `YYYY-MM-DD__YYYY-MM-DD_Title.txt`
- Preserves conversation structure with clear role labels (USER/ASSISTANT)
- Handles large JSON files (200MB+)
- Sanitizes filenames for cross-platform compatibility
- Filters out empty system messages

## Prerequisites

- Python 3.6 or higher
- Your ChatGPT conversations export file (`conversations.json`)

## Getting Your Conversation Data

1. Log in to ChatGPT at https://chat.openai.com
2. Click on your profile icon (bottom left)
3. Go to Settings → Data controls
4. Click "Export data"
5. Wait for the email with your download link
6. Download and extract the ZIP file
7. Locate the `conversations.json` file

## Usage

1. Place your `conversations.json` file in the repository directory

2. Run the extraction script:
```bash
python extract_conversations.py
```

3. Find your extracted conversations in the `conversations_output/` directory

## Output Format

Each conversation is saved as a text file with the following structure:

```
Title: [Conversation Title]
Created: YYYY-MM-DD HH:MM:SS
Updated: YYYY-MM-DD HH:MM:SS
================================================================================

[USER]
User's message content here...

--------------------------------------------------------------------------------

[ASSISTANT]
Assistant's response here...

--------------------------------------------------------------------------------
```

### Filename Format

Files are named using the pattern: `CreateDate__UpdateDate_Title.txt`

Examples:
- `2025-02-14__2025-06-15_Furnace Install Issue ARS.txt`
- `2024-05-24__2025-06-15_Moonlit Werewolf Lyrics.txt`
- `2023-06-13__2025-06-15_Permanent Vacation Facilities.txt`

## Customization

You can customize the script by modifying `extract_conversations.py`:

**Change output directory:**
```python
extract_conversations('conversations.json', output_dir='my_custom_dir')
```

**Filter conversations by date:**
```python
for conversation in conversations:
    if conversation.get('create_time') > some_timestamp:
        # process conversation
```

**Modify filename format:**
Edit the filename construction in the `extract_conversations()` function.

## Technical Details

- The script loads the entire JSON file into memory (tested with files up to 250MB)
- Message trees are traversed depth-first starting from root nodes
- Invalid filename characters are automatically sanitized
- Files are encoded as UTF-8 to handle special characters
- Progress is displayed every 100 conversations

## Project Structure

```
ChatGPTThreadExtractor/
├── extract_conversations.py   # Main extraction script
├── CLAUDE.md                  # Documentation for Claude Code
├── README.md                  # This file
├── .gitignore                 # Excludes large data files
└── conversations.json         # Your export file (not in repo)
```

## Notes

- The `conversations.json` file and `conversations_output/` directory are excluded from version control
- Large conversation exports may take a minute or two to process
- System messages and empty content are automatically filtered out

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Feel free to open issues or submit pull requests.
