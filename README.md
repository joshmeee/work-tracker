# Work Tracker

Central tracking for all projects and tasks across my development work with Claude.

## Overview

This repository serves as the single source of truth for:
- 📋 Task tracking across all projects
- 💡 Ideas and questions
- 📝 Planning documents and design specs
- 🔗 Cross-references to code in other repos
- 📊 Session summaries and progress tracking

## How It Works

### Mobile-First Workflow

1. **Capture ideas on the go** - Create issues from GitHub mobile app
2. **Get notified** - Push notifications when Claude responds or updates
3. **Review anywhere** - Phone, desktop, or synced to Obsidian vault
4. **No manual organization** - Claude handles labeling and structuring

### Issue Labels

**Projects:**
- `project:buzzwordbingo`
- `project:booklend`
- `project:cle-engine`
- `project:art-stream-auction`
- `project:term-dashboard`

**Types:**
- `idea` - Things to explore
- `task` - Concrete work to do
- `question` - Questions for Claude to answer/research
- `bug` - Issues to fix
- `planning` - Sprint/milestone planning

**Meta:**
- `from:claude` - Created or updated by Claude (watch for these notifications!)

### Documentation Structure

```
docs/
  plans/           # Design documents and implementation plans
    YYYY-MM-DD-topic-name.md
```

### Cross-Referencing

When code is committed in other repos, it references issues here:
```bash
git commit -m "feat: add dark mode (joshmeee/work-tracker#42)"
```

Issue descriptions link back to code:
```markdown
See implementation: [buzzwordbingo/src/components/Board.tsx](https://github.com/joshmeee/buzzwordbingo/blob/main/src/components/Board.tsx)
```

## Setup

### 1. Mobile Notifications

1. Install GitHub mobile app (iOS/Android)
2. Go to this repo → Watch → All Activity
3. Configure notification preferences

### 2. Desktop Integration

**Option A: Obsidian Vault Sync**
```bash
cd ~/OneDrive/Apps/remotely-save/JoshMeeDev/
git clone git@github.com:joshmeee/work-tracker.git
```

**Option B: GitHub Desktop**
- Clone this repo and pull regularly to see updates

### 3. Claude Integration

Claude automatically:
- Reads new issues at session start
- Responds to questions in comments (prefixed with 🤖 **Claude:**)
- Creates issues for completed work
- Updates issue status as work progresses
- Creates session summary issues

## Usage Examples

### Leaving a Question for Claude

Create an issue:
- **Title:** "Question: Should we use PostgreSQL or MongoDB for booklend?"
- **Body:** Context about what you're trying to decide
- Claude will respond in comments with analysis

### Capturing an Idea

Create an issue:
- **Title:** "buzzwordbingo: Add multiplayer spectator mode"
- **Body:** Brief description of the idea
- Claude will label it `idea`, `project:buzzwordbingo` and track it

### Planning a Sprint

Tell Claude in chat: "Let's plan the next sprint for buzzwordbingo"
- Claude creates structured issues with checklists
- Labels them appropriately
- Links related work

## Projects Tracked

- **buzzwordbingo** - https://github.com/joshmeee/buzzwordbingo
- **booklend** - Book lending management
- **cle-engine** - Custom game engine
- **art-stream-auction** - Live art auction platform
- **term-dashboard** - Terminal dashboard tool

## Session History

Session summaries are created as issues tagged `session-summary` with date in title.

---

**Last Updated:** 2026-01-13
