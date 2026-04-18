# stuff

Static site hosted on GitHub Pages. No build step, no framework.

## Structure

```
stuff/
├── index.html          # Landing page (fetches list.json, renders list with search)
├── list.json           # Project registry (source of truth for the landing page)
├── project-name/
│   └── index.html      # Each project lives in its own folder
└── ...
```

## Maintaining list.json

`list.json` is a JSON array of tool objects. The landing page fetches this file and renders the list. When adding or removing a tool, edit this file — not `index.html`.

### Fields

| Field  | Required | Description |
|--------|----------|-------------|
| `name`     | yes | Display name shown in the list |
| `path`     | no  | Folder name for tools hosted in this repo (e.g. `"my-tool"` links to `my-tool/`) |
| `url`      | no  | External URL for tools hosted elsewhere (opens in new tab) |
| `desc`     | no  | Short description shown below the name. Inline HTML allowed (`<br/>`, `<b>`, etc.) |
| `tag`      | no  | A string or array of strings. Any value works — colors are auto-generated from a hash so the same tag is always the same color |
| `category` | no  | Group heading (e.g. `"HTML/JS"`, `"CLI"`). Categories are derived from the data and sorted alphabetically. Tools without a category appear at the bottom ungrouped |

Entries can have `path`, `url`, or neither. If neither is present, the entry renders as plain (non-clickable) text — useful for projects that aren't publicly linkable yet.

### Adding a hosted tool

1. Create a folder with an `index.html` (e.g. `my-tool/index.html`)
2. Add an entry to `list.json`:
   ```json
   { "name": "My Tool", "path": "my-tool", "desc": "What it does", "tag": "llm", "category": "HTML/JS" }
   ```

### Adding an external link

Add an entry with `url` instead of `path`:
```json
{ "name": "My Repo", "url": "https://github.com/user/repo", "desc": "What it is", "tag": ["cli", "go"], "category": "CLI" }
```

### Adding a non-linkable entry

For projects that can't be linked yet (e.g. a private repo), omit both `path` and `url`:
```json
{ "name": "My Project", "desc": "What it does", "tag": "private repo", "category": "CLI" }
```

## Style

Keep tools simple — single-file HTML/JS/CSS where possible. No build tools, no package managers.
