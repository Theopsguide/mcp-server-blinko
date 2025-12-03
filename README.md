# mcp-server-blinko-extended

An extended MCP (Model Context Protocol) server for Blinko note service with update, delete, and archive capabilities.

Forked from [BryceWG/mcp-server-blinko](https://github.com/BryceWG/mcp-server-blinko) to add missing functionality for tracking task completion.

## Features

All original features plus:

- **update_blinko_note** - Update existing notes by ID (content, type, status flags)
- **delete_blinko_note** - Permanently delete notes by ID
- **archive_blinko_note** - Archive notes (move to archive without deleting)
- **complete_blinko_todo** - Mark todos as complete (archives them for metrics tracking)

## Installation

```bash
npx -y mcp-server-blinko-extended
```

## Claude Code Setup

```bash
claude mcp add -s user blinko \
  -e BLINKO_DOMAIN=<your-blinko-url> \
  -e BLINKO_API_KEY=<your-api-key> \
  -- npx -y mcp-server-blinko-extended@latest
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `BLINKO_DOMAIN` | Your Blinko instance URL (e.g., `https://blinko.example.com`) |
| `BLINKO_API_KEY` | Your Blinko API key |

## Available Tools

### Note Creation
- `upsert_blinko_flash_note` - Create quick flash notes (type 0)
- `upsert_blinko_note` - Create normal notes (type 1)
- `upsert_blinko_todo` - Create todo notes (type 2)

### Note Management (NEW)
- `update_blinko_note` - Update existing note by ID
- `delete_blinko_note` - Permanently delete note by ID
- `archive_blinko_note` - Archive note (move to archive)
- `complete_blinko_todo` - Mark todo as complete (archives it)

### Search & Discovery
- `search_blinko_notes` - Search notes with filters
- `review_blinko_daily_notes` - Get today's notes for review

### Other
- `share_blinko_note` - Share note publicly with optional password
- `clear_blinko_recycle_bin` - Empty the recycle bin

## Usage Example: Task Tracking

```
# Create a todo
upsert_blinko_todo(content="#claude #project:my-project\n\nImplement feature X")
# Returns: Note ID: 123

# When task is done, complete it
complete_blinko_todo(noteId=123)
# Todo moves to archive, preserving history for metrics
```

## License

MIT
