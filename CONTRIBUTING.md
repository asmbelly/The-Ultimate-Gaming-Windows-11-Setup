# Contributing

Thanks for wanting to improve this. Here's how to do it without wasting anyone's time.

---

## What Good Contributions Look Like

- **Accurate.** Every tweak must be verifiable. If you can't reproduce it, don't submit it.
- **Explained.** Every addition needs a "why." A setting change with no explanation is useless to someone learning.
- **Manual-first.** This guide is for humans, not scripts. If it can't be done by hand, it doesn't belong in the main guide.
- **Tested on Windows 11.** Don't submit Windows 10 tweaks and assume they carry over.

---

## What Will Be Rejected

- Tweaks with no measurable or documented impact
- Third-party tools that aren't widely trusted or are abandonware
- Registry edits you can't explain or source
- Bloated rewrites — if you're changing more than you're adding, open a discussion first
- Anything that requires running a mystery script from the internet

---

## How to Submit

1. Fork the repo
2. Create a branch: `git checkout -b your-tweak-name`
3. Make your changes
4. Open a pull request with a clear description of what you changed and why
5. Link a source if the tweak comes from external research

---

## Formatting Rules

- Follow the existing Markdown structure — headers, tables, and code blocks are already consistent, keep them that way
- Code goes in fenced code blocks with the correct language tag (` ```powershell `, ` ```cmd `, ` ```reg `)
- Registry paths go in code blocks, not inline
- Keep tables aligned
- No emojis

---

## Suggestions Without a PR

Open an issue. Describe the tweak, what it does, and why it should be included. If it's solid, it'll get added.

---

## Scope

This repo covers:

- Windows 11 only
- Gaming performance — latency, frame rate, frame time consistency
- App recommendations that are free, trusted, and actively maintained

Out of scope: Linux, Windows 10, overcloking guides, hardware recommendations, game-specific settings.
