# ChatGPT adapter · untested

> [!WARNING]
> **Untested.** These steps follow the capability contract but haven't been run end to end. Features vary by plan and change often, so check what your ChatGPT plan offers today.

| Capability the skill needs | What to look for in ChatGPT |
|---|---|
| Skill support | Skills support (SKILL.md folders), if your plan has it |
| Email reader | A Gmail (or other email) connector |
| Spreadsheet read/write | A Google Drive / Google Sheets connector |
| Scheduler | Scheduled tasks |
| Bank link (optional) | A read-only finance feature that links accounts |

## Option A: skills are available

Upload `dist/walker-finance.zip` (or the `walker-finance/` folder) as a skill, connect email and Drive, then follow steps 2–5 of the [Claude adapter](claude.md). The sheet setup is the same.

## Option B: no skills

1. Create a **Project** (or custom GPT) named *Walker finance*.
2. Paste [paste-ready.md](paste-ready.md) into its instructions.
3. Upload these files as Project files:
   - `walker-finance/references/ledger-rules.md`
   - `walker-finance/references/spending.md`
   - `walker-finance/references/scheduled-check.md`
   - `walker-finance/references/config.md`
4. Connect email and Drive if available. If they aren't, the assistant runs in manual mode: you paste alert emails in, and it returns rows to save.

## Scheduled pings

If scheduled tasks are available, create one that runs every 4 hours inside the project:

```text
Run the walker-finance scheduled check. Only message me if a ping rule fires.
```
