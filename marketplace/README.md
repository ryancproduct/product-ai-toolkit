# AI PM Kit Marketplace

Claude Code marketplace for the [AI PM Kit](https://github.com/ryancproduct/product-ai-toolkit) plugin.

## Install

```bash
claude plugin marketplace add ryancproduct/ai-pm-kit-marketplace
claude plugin install ai-pm-kit
```

## What's included

- **ai-pm-kit** — 15 PM commands, 19 skills, and 5 specialist agents for product management

## Publishing

This directory is designed to be published as a separate GitHub repo at `ryancproduct/ai-pm-kit-marketplace`. To publish:

```bash
cd marketplace
git init
git add .
git commit -m "Initial marketplace"
git remote add origin https://github.com/ryancproduct/ai-pm-kit-marketplace.git
git push -u origin main
```
