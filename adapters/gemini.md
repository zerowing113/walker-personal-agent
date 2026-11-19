# Gemini adapter · untested

> [!WARNING]
> **Untested.** These steps follow the capability contract but haven't been run end to end. Check what your Gemini plan offers today.

| Capability the skill needs | What to look for in Gemini |
|---|---|
| Skill support | Skills support, if available. Otherwise a **Gem** with custom instructions and knowledge files. |
| Email reader | Gmail access through Google Workspace apps |
| Spreadsheet read/write | Google Sheets access through Google Workspace apps |
| Scheduler | Scheduled actions |
| Bank link (optional) | A read-only finance feature, if offered |

## Setup with a Gem

1. Create a Gem named *Walker finance*.
2. Paste [paste-ready.md](paste-ready.md) into its instructions.
3. Add these files as knowledge:
   - `walker-finance/references/ledger-rules.md`
   - `walker-finance/references/spending.md`
   - `walker-finance/references/scheduled-check.md`
   - `walker-finance/references/config.md`
4. Make sure Gmail and Google Sheets access are on, and create the `Walker Finance Ledger` sheet as described in the [Claude adapter](claude.md#2-connect-your-data-3-min).
5. If you have scheduled actions, schedule one every 4 hours with:

```text
Run the walker-finance scheduled check. Only message me if a ping rule fires.
```

Then run the [test checklist](claude.md#5-test-checklist).
