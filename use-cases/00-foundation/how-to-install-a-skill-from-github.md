# How to install a Claude Code skill from GitHub

A step-by-step guide for beginners. It works for any public skill on GitHub. You need about 15 minutes, a Mac or Linux computer (on Windows, use WSL), Git, and Claude Code.

**What a skill is:** a folder with a file called `SKILL.md` inside. The file tells Claude how to do one job, like auditing a website or writing a case study. Some skills also include guides (`references/`), examples (`examples/`) or programs (`scripts/`).

**How to use this guide:** replace everything in `CAPITALS` with your own values. Type the commands in a terminal, one block at a time.

---

## Step 1. Find the skill folder

Open the repository on GitHub and click through the folders until you see `SKILL.md`. That folder is the skill.

Note three things from the web address. For example, in
`https://github.com/elmohq/elmo/tree/main/skills/aeo`:

| Placeholder | Meaning | Example |
|---|---|---|
| `OWNER` | who published it | `elmohq` |
| `REPO` | the repository name | `elmo` |
| `PATH/TO/SKILL` | the folder path after `tree/main/` | `skills/aeo` |
| `SKILL-NAME` | the last part of that path | `aeo` |

## Step 2. Read before you install

A skill can run code on your computer, so read it first. On GitHub, open:

1. **`SKILL.md`**: what the skill does and when Claude uses it.
2. **Every file in `scripts/`**, if there is one. These are programs. Check:
   - Which websites does it contact?
   - Does it read, change or delete files on your computer?
   - Does it install anything else?
   - Does it ask for passwords, API keys or tokens?
3. **The license**: look for `LICENSE`, `LICENSE.md` or an access note at the top of the repository.
   - **MIT or Apache:** free to use, copy and change. Keep the license file with your copy.
   - **No license:** "all rights reserved." Use it for yourself, but don't republish it.

If you don't understand a script, paste it into Claude and ask: "What does this do, what does it contact, and is anything risky?"

**Stop here if** a script sends your data somewhere unexpected, deletes files, or asks for a key without explaining why.

## Step 3. Download only the skill folder

This downloads one folder, not the whole project, into a review folder where nothing runs yet:

```bash
git clone --depth 1 --filter=blob:none --sparse https://github.com/OWNER/REPO.git ~/skill-review/REPO && cd ~/skill-review/REPO && git sparse-checkout set PATH/TO/SKILL && ls -R PATH/TO/SKILL
```

**What each part does:**

| Part | Meaning |
|---|---|
| `--depth 1` | only the latest version, without the history |
| `--filter=blob:none --sparse` | the file list, not the files yet |
| `git sparse-checkout set PATH/TO/SKILL` | now fetch just this folder |
| `ls -R` | show what arrived, including subfolders |

**Check:** the list shows `SKILL.md` and the same files you saw on GitHub.

## Step 4. Install it

Claude Code looks for skills in `~/.claude/skills/`. A skill there works in every project.

```bash
mkdir -p ~/.claude/skills && cp -R ~/skill-review/REPO/PATH/TO/SKILL ~/.claude/skills/SKILL-NAME && ls ~/.claude/skills/SKILL-NAME
```

**Check:** you see `SKILL.md` directly inside, not inside another folder.

If the repository has its license at the top level, copy it in too:

```bash
cp ~/skill-review/REPO/LICENSE* ~/.claude/skills/SKILL-NAME/
```

**Want the skill in one project only?** Copy it into that project's `.claude/skills/` folder instead.

## Step 5. Use it

1. Open a new Claude Code session.
2. Type `/SKILL-NAME` followed by your request, for example:
   `/aeo Check whether AI crawlers can read https://example.com`
3. Or just describe the task. Claude loads the skill when the topic matches its description.

The first time a skill runs a script, Claude asks for permission. Approve it only if you read that script in Step 2.

## Step 6. Clean up (optional)

The review folder isn't needed any more:

```bash
rm -rf ~/skill-review/REPO
```

`rm -rf` deletes without using the Trash. Check the path before you press Enter.

---

## Common mistakes

| Problem | Cause | Fix |
|---|---|---|
| Claude doesn't find the skill | The file isn't named exactly `SKILL.md` | Rename it. Capital letters matter. |
| Claude doesn't find the skill | `SKILL.md` sits one folder too deep | Move it up so it's directly inside `~/.claude/skills/SKILL-NAME/` |
| The skill mentions files that don't exist | You copied only `SKILL.md`, not the whole folder | Repeat Steps 3 and 4 with the full folder |
| A folder appears inside itself | You ran `cp -R` twice | Delete the inner copy |
| `git sparse-checkout` is unknown | Git is too old | Update Git (version 2.25 or newer) |
| A command did nothing in Claude Code | You typed it without `!` | In Claude Code's prompt, start terminal commands with `!` |

## Safety checklist

- [ ] I read `SKILL.md`.
- [ ] I read every script, or had it explained.
- [ ] I know which websites it contacts.
- [ ] It doesn't ask for keys or passwords, or I know why it does.
- [ ] I checked the license.
- [ ] I installed the whole folder, with `SKILL.md` at the top.
