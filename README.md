# AI Assistant Plugin for Super Productivity

An AI assistant plugin — powered by OpenAI, Anthropic Claude, or Google Gemini — that lets you manage tasks, projects, and tags via natural language chat.

## Features

- 🤖 Chat with AI to manage your tasks
- 🔀 Switch between OpenAI, Claude, and Gemini in Settings
- 📋 Create, update, delete, complete tasks — single or bulk
- 📁 Manage projects and tags
- ⏱️ Start/stop timers, set current task, plan for today
- 🏷️ Add/remove individual tags without replacing others
- 📊 Worklog reports: time per day/project/tag, estimate accuracy
- 🔄 Agentic tool calling — AI auto-executes operations (up to 5 rounds)
- 📝 Markdown rendering for AI responses (headers, tables, code blocks, lists)
- ⚙️ Configurable: API key, base URL, model, temperature

## Installation

1. Download the latest `ai-assistant-plugin.zip` from Releases
2. Open Super Productivity → Settings → Plugins → Load unpacked
3. Select the zip file
4. Click the ⚙️ button in the plugin panel to configure your API key

## Configuration

Click the ⚙️ button in the top-right corner of the plugin panel:

| Field | Default | Description |
|-------|---------|-------------|
| Provider | `OpenAI` | `OpenAI`, `Claude`, or `Gemini` — switches API format and fills the fields below |
| API Key | *(required)* | Key for the selected provider |
| Base URL | `https://api.openai.com/v1` | Provider API endpoint (auto-filled per provider) |
| Model | `gpt-4o` | Model name (auto-filled per provider) |
| Max Tokens | `4096` | Max response tokens |
| Temperature | `0.7` | Response creativity (0-2; Claude clamps to 0-1) |

Provider defaults:

| Provider | Base URL | Default Model |
|----------|----------|---------------|
| OpenAI | `https://api.openai.com/v1` | `gpt-4o` |
| Claude | `https://api.anthropic.com` | `claude-sonnet-5` |
| Gemini | `https://generativelanguage.googleapis.com/v1beta` | `gemini-2.5-flash` |

The OpenAI provider also accepts any OpenAI-compatible API (DeepSeek, local models, etc.) via a custom Base URL.

## Supported Operations

| Category | Tools | Description |
|----------|-------|-------------|
| **Tasks** | `create_task`, `get_tasks`, `update_task`, `complete_task`, `delete_task` | Full CRUD with advanced filters (search, overdue, planned, recurring) |
| **Bulk** | `bulk_complete_tasks`, `bulk_update_tasks` | Batch operations, up to 100 tasks |
| **Tags** | `add_tag_to_task`, `remove_tag_from_task` | Add/remove single tags without replacing others |
| **Subtasks** | `create_task_with_subtasks` | Create parent + subtasks in one call |
| **Planning** | `plan_tasks_for_today` | Add/remove tasks from Today view |
| **Timer** | `get_current_task`, `start_task`, `stop_task` | Time tracking control |
| **Reorder** | `reorder_tasks`, `move_task_to_project` | Reorder tasks, move between projects |
| **Worklog** | `get_worklog` | Time reports by day/project/tag with estimate accuracy |
| **Projects** | `get_projects`, `create_project`, `update_project` | Project management |
| **Tags** | `get_tags`, `create_tag`, `update_tag` | Tag management |
| **Context** | `set_active_work_context` | Switch active project/tag view |
| **UI** | `show_notification` | Show snackbar notifications |

### Task Filters (`get_tasks`)

| Filter | Description |
|--------|-------------|
| `project_id` | Filter by project |
| `tag_id` | Filter by tag |
| `search_query` | Case-insensitive title/notes search |
| `parents_only` | Exclude subtasks |
| `overdue` | Due date before today |
| `unscheduled` | No due date set |
| `planned_for_today` | Planned for today |
| `recurring_only` | Only recurring tasks |

## Development

```
├── manifest.json        # Plugin metadata
├── plugin.js            # Background: register buttons/shortcuts
├── index.html           # Chat UI + OpenAI/Claude/Gemini integration (all inline)
└── icon.svg             # Plugin icon
```

### Build / Package

```bash
cd ~/server/ai-assistant-plugin && python3 -c "
import zipfile
with zipfile.ZipFile('ai-assistant-plugin.zip', 'w', zipfile.ZIP_DEFLATED) as zf:
    for f in ['manifest.json', 'plugin.js', 'index.html', 'icon.svg']:
        zf.write(f, f)
        print(f'  added: {f}')
"
```

Output: `ai-assistant-plugin.zip` in the project root.

## Requirements

- Super Productivity v13.0.0+
- API key for OpenAI, Anthropic Claude, or Google Gemini

## License

MIT
