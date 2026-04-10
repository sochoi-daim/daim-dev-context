# daim

> Claude Code plugin that helps developers quickly understand new projects and generate token-efficient Context Documents.

## What does this plugin do?

When you take on a new project or unfamiliar codebase, run a single command to organize the project context. The generated **Context Document** lets you skip repeated explanations in future Claude conversations and jump straight into work.

## Supported Project Types

- **Web**: React, Next.js, Vue
- **Unity**: Unity (URP), REST API server integration
- **Backend**: Node.js (Express / NestJS)

## Installation

```bash
npx claude-plugins install @daim-research/daim
```

Reload plugins in Claude Code:
```
/reload-plugins
```

## Commands

| Command | Description |
|---------|-------------|
| `/daim:context` | Start interview-based project analysis |
| `/daim:context web` | Start with web-specific interview |
| `/daim:context unity` | Start with Unity-specific interview |
| `/daim:context fast` | Generate document immediately from files (no questions) |
| `/daim:update` | Update an existing Context Document |
| `/daim:save [path]` | Save document to a file |
| `/daim:show` | Print current document |

## Usage

### Thorough Analysis (Interview Mode)

Best for complex projects where you need high accuracy.

```
/daim:context
```

1. Claude asks your project type (Web / Unity / Other)
2. Walks through targeted questions one by one:
   - Project name and description
   - Current task and goals
   - Key areas of complexity
   - Framework-specific questions (routes, state management, scene structure, etc.)
3. If files are available, Claude scans the codebase automatically
4. Generates a structured Context Document
5. Lists all `[needs confirmation]` items for your review

```
/daim:save ./docs/
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
/daim:save ./docs/
```

### Updating an Existing Document

As work progresses, keep your Context Document current:

```
/daim:update
```

Choose what to update:
1. Add new module or feature
2. Change current work context
3. Add notes or caveats
4. Free-form input

Only the relevant section is modified. Updated items have their tags removed.

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
- **Framework branching** — auto-selects React or Vue template
- **Unity REST API support** — covers REST API server integration patterns
