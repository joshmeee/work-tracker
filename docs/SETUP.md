# Setup Guide

Complete setup instructions for the work-tracker system.

## 1. Repository Labels

You need to create these labels in the GitHub repository. Go to:
**Issues → Labels → New label**

### Project Labels (Color: #0E8A16 - Green)

- `project:buzzwordbingo`
- `project:booklend`
- `project:cle-engine`
- `project:art-stream-auction`
- `project:term-dashboard`

### Type Labels (Color: #0075CA - Blue)

- `idea` - Things to explore
- `task` - Concrete work to do
- `question` - Questions for Claude
- `bug` - Issues to fix
- `planning` - Sprint/milestone planning

### Meta Labels

- `from:claude` (Color: #7057FF - Purple) - Updated by Claude
- `session-summary` (Color: #D4C5F9 - Light Purple) - End of session recaps

## 2. Mobile Setup

### GitHub App

1. **Install GitHub mobile app**
   - iOS: App Store
   - Android: Google Play

2. **Enable notifications**
   - Open app → Settings → Notifications
   - Enable "Push notifications"
   - Set preferences for Issues

3. **Watch this repository**
   - Go to joshmeee/work-tracker
   - Tap the Watch button
   - Select "All Activity"

### Quick Issue Creation

On mobile, you can create issues in 3 taps:
1. Open repo → Issues tab
2. Tap "+"
3. Select template (Idea, Question, or blank)

## 3. Desktop Integration

### Option A: Obsidian Vault (Recommended)

Clone this repo into your Obsidian vault:

```bash
cd ~/OneDrive/Apps/remotely-save/JoshMeeDev/
git clone git@github.com:joshmeee/work-tracker.git
```

Now markdown docs in `docs/` will appear in Obsidian.

**Sync workflow:**
- Pull regularly to get Claude's updates: `cd work-tracker && git pull`
- Push your local changes: `git add . && git commit -m "..." && git push`

### Option B: GitHub Desktop

1. Download GitHub Desktop: https://desktop.github.com/
2. Clone joshmeee/work-tracker
3. Pull regularly to see Claude's updates
4. Review diffs before pulling

## 4. Mac Setup (Always-On Machine)

If you want automated syncing on your Mac:

1. Clone the repo to your Mac
2. Set up a cron job or launchd task to auto-pull every 15 minutes
3. Or use GitHub Desktop and pull manually

## 5. Verify Setup

Create a test issue:
- Title: "Test: Setup verification"
- Body: "Testing the work-tracker system"
- Label: `question`

In the next Claude session, Claude should:
- See the issue
- Comment with 🤖 **Claude:** prefix
- You should get a mobile notification

## 6. First Use

**Try these workflows:**

1. **Ask a question:**
   - Create issue: "Question: What's the best way to structure my database?"
   - Claude responds in comments

2. **Capture an idea:**
   - Create issue: "buzzwordbingo: Add chat feature"
   - Claude labels it and can help plan it later

3. **Work with Claude:**
   - Start a session: "Let's add dark mode to buzzwordbingo"
   - Claude creates/updates issues automatically
   - Check notifications to see progress

## Troubleshooting

### Not getting notifications?

- Check GitHub mobile app notification settings
- Verify you're watching the repo (All Activity)
- Check your phone's notification settings for GitHub app

### Can't see Claude's updates in Obsidian?

- Run `git pull` in the work-tracker directory
- Check if repo is in the right location in your vault
- Verify git credentials are set up

### Labels not appearing?

- Create them manually (see section 1 above)
- Or let Claude know and he can guide you through it

---

**Setup complete!** You're ready to start tracking your work with Claude.
