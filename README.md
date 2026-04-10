# daim

> Claude Code plugin that helps developers quickly understand new projects and generate token-efficient Context Documents.

## What does this plugin do?

When you take on a new project or unfamiliar codebase, run a single command to organize the project context. The generated **Context Document** lets you skip repeated explanations in future Claude conversations and jump straight into work.

## Supported Project Types

- **Frontend**: React, Next.js, Vue
- **Unity**: Unity (URP), REST API server integration
- **Backend**: Node.js (Express / NestJS)

## Installation

### From GitHub (team marketplace)

1. Add the marketplace:
```
/plugin marketplace add sochoi-daim/daim-context
```

2. Install the plugin:
```
/plugin install daim@daim-context
```

### From local directory (development)

```bash
git clone https://github.com/sochoi-daim/daim-context.git
claude --plugin-dir ./daim-context
```

### Verify installation

```
/daim:context help
```

## Commands

The main entry point is `/daim:context`. After the skill is loaded, sub-commands work without prefix in the conversation.

| Command | Description |
|---------|-------------|
| `/daim:context` | Start interview-based project analysis |
| `/daim:context frontend` | Start with frontend-specific interview |
| `/daim:context unity` | Start with Unity-specific interview |
| `/daim:context fast` | Generate document immediately from files (no questions) |

**In-conversation commands** (after skill is loaded):

| Command | Description |
|---------|-------------|
| `/update` | Update an existing Context Document |
| `/save [path]` | Save document to a file |
| `/show` | Print current document |
| `/help` | Print command list |

## Usage

### Thorough Analysis (Interview Mode)

Best for complex projects where you need high accuracy.

```
/daim:context
```

1. Claude asks your project type (Frontend / Unity / Backend / Other)
2. Walks through targeted questions one by one:
   - Project name and description
   - Current task and goals
   - Key areas of complexity
   - Framework-specific questions (routes, state management, scene structure, etc.)
   - Don't know the answer? Type **skip** or **s** to move on — skipped items are tagged `[needs confirmation]`
3. If files are available, Claude scans the codebase automatically
4. Generates a structured Context Document
5. Lists all `[needs confirmation]` items for your review

```
/save ./docs/
```

Save the document once you've verified everything.

### Quick Start (Fast Mode)

Best when you have the codebase and want results immediately.

```
/daim:context fast
```

1. Claude auto-detects project type and framework from files
2. Scans `package.json`, `tsconfig.json`, folder structure, etc.
3. Generates Context Document instantly — no questions asked
4. Unverified items are clearly tagged:
   - `[inferred]` — high confidence but not confirmed
   - `[needs confirmation]` — must be verified by you

```
/save ./docs/
```

### Updating an Existing Document

As work progresses, keep your Context Document current:

```
/update
```

Choose what to update:
1. Add new module or feature
2. Change current work context
3. Add notes or caveats
4. Free-form input

Only the relevant section is modified. Updated items have their tags removed.

### Saving the Document

Save the Context Document as a markdown file:

```
/save                          → ./context-myapp-20260410.md (default)
/save ./docs/                  → ./docs/context-myapp-20260410.md
/save ./docs/myapp-context.md  → ./docs/myapp-context.md
```

If `[needs confirmation]` items remain, a warning is shown before saving.

### Viewing the Current Document

Review the generated document before saving:

```
/show
```

If no document has been generated yet, a message will prompt you to run `/daim:context` first.

### Checking Available Commands

```
/help
```

### Using the Document in Future Sessions

Paste or attach the saved Context Document at the start of a new conversation. Claude will have full project context without any setup.

```
[paste context-myproject-20260410.md]
Fix the login redirect bug on the /auth page.
```

## Key Features

- **No-assumption principle** — never fills in project details from general knowledge
- **Confidence tags** — clearly distinguishes confirmed / `[inferred]` / `[needs confirmation]`
- **Token optimization** — structured format for minimum tokens, maximum context
- **Framework branching** — auto-selects React, Next.js, or Vue template
- **Unity REST API support** — covers REST API server integration patterns
