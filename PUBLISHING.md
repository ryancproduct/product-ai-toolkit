# Publishing Guide

How to test, review, and publish AI PM Kit as a Claude Code plugin.

This guide assumes you're working from GitHub's web interface and the Terminal app on your Mac. Every command is copy-pasteable — nothing needs to be modified unless noted.

---

## Overview

There are two things to publish:

1. **This repo** (`product-ai-toolkit`) — the plugin itself, containing all the commands, skills, and agents.
2. **A new repo** (`ai-pm-kit-marketplace`) — a tiny "directory listing" that tells Claude Code where to find the plugin.

Users will run two commands to install:

```bash
claude plugin marketplace add ryancproduct/ai-pm-kit-marketplace
claude plugin install ai-pm-kit
```

---

## Step 1: Test the plugin before merging the PR

You can test the plugin directly from the PR branch without merging anything into `main`. This lets you verify everything works before making it public.

### 1a. Check out the PR branch locally

Open Terminal and run:

```bash
cd ~/dev/product-ai-toolkit
git fetch origin
git checkout feat/plugin-conversion   # replace with the actual PR branch name
```

> **How to find the branch name:** On the GitHub PR page, look near the top — it shows something like `username wants to merge 3 commits into main from feat/plugin-conversion`. The branch name is the part after "from".

### 1b. Create a temporary test marketplace

You need a temporary marketplace file that points to your PR branch (not `main`). Run this in Terminal:

```bash
mkdir -p /tmp/test-marketplace/.claude-plugin
```

Then create the marketplace file. Copy and paste this entire block:

```bash
cat > /tmp/test-marketplace/.claude-plugin/marketplace.json << 'EOF'
{
  "name": "ai-pm-kit-test",
  "owner": {
    "name": "Ryan Clement"
  },
  "metadata": {
    "description": "TEST marketplace for AI PM Kit",
    "version": "0.0.1"
  },
  "plugins": [
    {
      "name": "ai-pm-kit",
      "source": {
        "source": "url",
        "url": "https://github.com/ryancproduct/product-ai-toolkit.git",
        "ref": "feat/plugin-conversion"
      },
      "description": "AI PM Kit (testing from PR branch)",
      "version": "1.0.0"
    }
  ]
}
EOF
```

> **Important:** Replace `feat/plugin-conversion` on the `"ref"` line with the actual PR branch name if different.

### 1c. Install from the test marketplace

```bash
claude plugin marketplace add --local /tmp/test-marketplace
claude plugin install ai-pm-kit
```

### 1d. Verify it works

Open Claude Code and try a command:

```
/jtbd "Users keep asking for dark mode"
```

Try a few more to make sure things are wired up:

```
/competitive-analysis "project management software market"
/stakeholder-update
```

Check that the agents show up too — start a Claude Code session and ask:

```
Use the market-research-analyst agent to summarise the AI agent market
```

### 1e. Clean up after testing

Once you're happy, remove the test plugin so it doesn't interfere with the real one:

```bash
claude plugin uninstall ai-pm-kit
claude plugin marketplace remove ai-pm-kit-test
rm -rf /tmp/test-marketplace
```

---

## Step 2: Merge the PR

Once testing passes, merge the PR on GitHub:

1. Go to the PR page on GitHub (e.g. `https://github.com/ryancproduct/product-ai-toolkit/pulls`)
2. Open the PR
3. Click the green **"Merge pull request"** button
4. Click **"Confirm merge"**
5. Optionally click **"Delete branch"** to clean up the PR branch

Your `main` branch now has the plugin structure.

---

## Step 3: Create the marketplace repo on GitHub

The marketplace is a separate, tiny repo that acts as a directory listing for your plugin.

### 3a. Create the repo on GitHub

1. Go to [github.com/new](https://github.com/new)
2. Fill in:
   - **Repository name:** `ai-pm-kit-marketplace`
   - **Description:** `Claude Code marketplace for AI PM Kit`
   - **Visibility:** Public
   - Leave everything else as default (no README, no .gitignore, no licence — we'll push our own files)
3. Click **"Create repository"**
4. Leave the page open — you'll need the URL in the next step

### 3b. Push the marketplace files

Back in Terminal:

```bash
cd ~/dev/product-ai-toolkit/marketplace
git init
git add .
git commit -m "Initial marketplace for AI PM Kit"
git branch -M main
git remote add origin https://github.com/ryancproduct/ai-pm-kit-marketplace.git
git push -u origin main
```

> **If you get an authentication error:** GitHub may ask you to sign in. If you haven't used `git push` from Terminal before, follow [GitHub's guide to setting up authentication](https://docs.github.com/en/get-started/getting-started-with-git/set-up-git).

---

## Step 4: Test the real installation

Now test the full installation flow that your users will follow:

```bash
claude plugin marketplace add ryancproduct/ai-pm-kit-marketplace
claude plugin install ai-pm-kit
```

Open Claude Code and run:

```
/jtbd "Users keep asking for dark mode"
```

If it works, you're live. Anyone can now install with those same two commands.

---

## Step 5: Update the README (optional but recommended)

The README already has the new install instructions. Give it a final read on GitHub to make sure it looks right:

`https://github.com/ryancproduct/product-ai-toolkit`

---

## Releasing updates

When you make changes to commands, skills, or agents in the future:

### For small updates (bug fixes, tweaks)

Just merge to `main`. Users will pick up changes next time they update:

```bash
claude plugin update ai-pm-kit
```

### For version bumps (new features, new commands)

1. Update the version in `.claude-plugin/plugin.json` (e.g. `"1.0.0"` → `"1.1.0"`)
2. Merge to `main`
3. Update the marketplace repo to match:

```bash
cd ~/dev/ai-pm-kit-marketplace
# Edit .claude-plugin/marketplace.json — update the version to match plugin.json
git add .
git commit -m "Bump ai-pm-kit to 1.1.0"
git push
```

---

## Troubleshooting

**"Plugin not found" when installing:**
The marketplace repo might not be public. Go to `https://github.com/ryancproduct/ai-pm-kit-marketplace` → Settings → Danger Zone → Change visibility → Public.

**Commands don't show up after installing:**
Restart Claude Code. Some installations need a fresh session to pick up new commands and skills.

**"Permission denied" when pushing to GitHub:**
You need to authenticate with GitHub from Terminal. The simplest way is [GitHub CLI](https://cli.github.com/):

```bash
brew install gh
gh auth login
```

Then retry the `git push` command.

**Want to remove everything and start fresh:**

```bash
claude plugin uninstall ai-pm-kit
claude plugin marketplace remove ai-pm-kit-marketplace
```
