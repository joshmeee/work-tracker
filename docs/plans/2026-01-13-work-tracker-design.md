# Work Tracker System Design

**Date:** 2026-01-13  
**Status:** Implemented  
**Goal:** Create a unified tracking system for all projects and work with Claude

## Problem Statement

Need to track work across multiple projects (buzzwordbingo, booklend, cle-engine, etc.) with these requirements:
- Single place to see everything
- Works on mobile for capturing ideas on the go
- Get notified when Claude makes updates
- Connect to markdown documentation
- Support both chat-driven work and planned sprints
- Maximum automation from conversations

Previous attempt with Obsidian inbox failed due to sync issues.

## Design Decisions

### Why GitHub Issues (not Jira, Notion, Linear)?

**Chosen:** GitHub Issues + Projects

**Reasons:**
1. All code already on GitHub (buzzwordbingo, booklend, etc.)
2. Native cross-referencing between issues and commits
3. GitHub MCP tools available (Claude can read/write directly)
4. Free for unlimited repos
5. Mobile app with push notifications
6. Markdown-native
7. Can clone repo into Obsidian vault for doc sync

**Rejected alternatives:**
- **Jira Cloud:** Overkill for solo + Claude, costs money after trial, less mobile-friendly
- **Notion:** Better UI but weaker git integration, API limits, not markdown files
- **Linear:** Great UX but another platform to manage, costs money, no direct git integration

### Central Repo vs. Per-Project Issues?

**Chosen:** Central tracking repo (`work-tracker`)

**Reasons:**
1. Single source of truth - one place to check
2. Mobile-friendly - only watch one repo for notifications
3. Cross-project planning easier
4. Labels provide project organization
5. Can still reference specific repos in descriptions

**Trade-off:** Issues are separate from code, but we mitigate with cross-references

### How Claude Tracks Work?

**Automation approach:**

1. **Session start:**
   - Check for new issues (especially `question` and `idea` labels)
   - Read memory-keeper context
   - Respond to questions in comments

2. **During work:**
   - Create issues for significant implementations
   - Update existing issues with progress
   - Add `from:claude` label
   - Prefix all comments with 🤖 **Claude:**

3. **Session end:**
   - Create session summary issue
   - Tag with `session-summary`
   - List what was accomplished

4. **When uncertain:**
   - Ask user: "Should I create an issue for this?" with options

### Labeling System

**Project labels:** `project:buzzwordbingo`, `project:booklend`, etc.
**Type labels:** `idea`, `task`, `question`, `bug`, `planning`
**Meta labels:** `from:claude`, `session-summary`

User doesn't need to add labels manually - Claude handles it based on context.

### Notification Strategy

**User gets notified via:**
- GitHub mobile push notifications
- Every issue create/update
- Prefix identifies Claude's updates: 🤖 **Claude:**

**Why this works:**
- Immediate feedback when Claude responds to questions
- Can check progress while away from computer
- Filter by `from:claude` label to see just Claude's updates

### Documentation Integration

**Markdown docs in repo:**
- Design docs: `docs/plans/YYYY-MM-DD-topic.md`
- Issue templates: `.github/ISSUE_TEMPLATE/`
- Setup guide: `docs/SETUP.md`

**Obsidian integration:**
- Clone repo into vault: `~/OneDrive/Apps/remotely-save/JoshMeeDev/work-tracker/`
- Use GitHub Desktop to sync (manual pull for visibility)
- Markdown files appear in Obsidian automatically

**Why not auto-sync?**
- User wants to see what Claude changed before pulling
- Obsidian Git plugin was unreliable before
- GitHub Desktop provides visual diff review

### Cross-Referencing

**Code to issues:**
```bash
git commit -m "feat: add dark mode (joshmeee/work-tracker#42)"
```

**Issues to code:**
```markdown
See: [buzzwordbingo/src/components/Board.tsx](link)
```

**Issues to issues:**
```markdown
Related to #38
Blocks #45
```

## User Workflows

### Capture Idea on Phone

1. Open GitHub mobile → work-tracker → Issues
2. Tap "+"
3. Choose "Idea" template or blank
4. Type title: "buzzwordbingo: Add multiplayer mode"
5. Add brief description
6. Submit (no labels needed)
7. Claude sees it next session, labels it, responds

### Ask a Question

1. Create issue with title: "Question: Should I use REST or GraphQL?"
2. Add context in body
3. Claude responds in comments with 🤖 **Claude:** prefix
4. Get push notification with answer

### Work on a Task

1. Tell Claude: "Let's add authentication to booklend"
2. Claude creates issue: "Implement authentication for booklend"
3. As work progresses, Claude updates issue
4. When done, Claude closes issue with summary
5. User gets notifications at each step

### Review Progress

1. Open GitHub mobile or web
2. Filter issues by `project:buzzwordbingo`
3. See open/closed ratio
4. Check session summaries
5. Review Claude's updates (filter by `from:claude`)

### Plan a Sprint

1. Tell Claude: "Let's plan the next two weeks for buzzwordbingo"
2. Claude creates issues with checklists
3. Labels as `planning`, `project:buzzwordbingo`
4. User reviews and adjusts
5. Work begins on prioritized issues

## Implementation

### Phase 1: Repository Setup ✅
- [x] Create work-tracker repo
- [x] Add README with workflow docs
- [x] Create docs structure
- [x] Add issue templates
- [x] Write setup guide

### Phase 2: User Setup (Next)
- [ ] User creates labels
- [ ] User clones repo to Obsidian vault
- [ ] User sets up mobile notifications
- [ ] Create test issue to verify

### Phase 3: First Use
- [ ] User creates a question issue
- [ ] Claude responds in next session
- [ ] User captures an idea
- [ ] Work on a task together and track it

## Success Metrics

**System is working if:**
1. User creates 3+ issues per week from mobile
2. User gets notifications within 1 hour of Claude's updates
3. Documentation syncs to Obsidian successfully
4. Claude successfully tracks 90%+ of significant work
5. User reviews issues at least 2x per week

## Risks & Mitigations

**Risk:** Notification overload  
**Mitigation:** User can adjust GitHub notification settings, filter by label

**Risk:** Claude creates too many issues (noise)  
**Mitigation:** Ask user when uncertain, learn patterns over time

**Risk:** User forgets to pull updates to Obsidian  
**Mitigation:** GitHub Desktop shows notification dot when updates available

**Risk:** Cross-references break if repos renamed  
**Mitigation:** Use full `owner/repo#number` format, document repo changes

## Future Enhancements

**Possible additions:**
- GitHub Actions to auto-label based on title patterns
- Weekly summary automation
- Link to deployed versions (e.g., buzzwordbingo live URL)
- Metrics dashboard (issues closed per week, etc.)
- Integration with time tracking
- Slack/Discord notifications as alternative to mobile

**YAGNI for now:**
- Automated project boards (use simple labels first)
- Complex workflows (keep it simple initially)
- Synchronization to other platforms (GitHub is enough)

## Technical Notes

**GitHub MCP Tools Used:**
- `create_issue` - Create tracking issues
- `issue_write` - Update status and labels
- `add_issue_comment` - Respond to questions
- `list_issues` - Check for new issues at session start
- `create_or_update_file` - Push markdown docs

**Memory Keeper Integration:**
- `context_save()` for short-term context within sessions
- GitHub issues for long-term memory across sessions

## Conclusion

This design provides a mobile-first, automated tracking system that:
- Lives where the code lives (GitHub)
- Works offline and online
- Requires minimal manual organization
- Provides notifications and visibility
- Integrates with existing tools (Obsidian, git)

The system scales from quick idea capture to structured sprint planning, supporting the evolution from chat-driven work to planned development cycles.

---

**Next Steps:** Follow `docs/SETUP.md` to complete user configuration.
