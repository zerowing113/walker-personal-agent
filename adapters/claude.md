# Claude adapter · primary platform

**Status:** the primary target for v1. Run the [test checklist](#5-test-checklist) once after setup.

| Capability the skill needs | What provides it in Claude |
|---|---|
| Skill support | Custom skills (open SKILL.md standard) |
| Email reader | Gmail connector |
| Spreadsheet read/write | Google Drive connector, reaching your `Walker Finance Ledger` Google Sheet |
| Scheduler | Claude Duet's background monitoring, or scheduled tasks where your plan offers them |
| Bank link (optional) | Personal Finance in Claude (US beta, read-only, via Plaid) |

## 1. Install the skill (2 min)

1. In **Settings → Capabilities**, make sure code execution and file creation is on. The skill feature needs it.
2. Download [`dist/walker-finance.zip`](../dist/walker-finance.zip). Don't unzip it. The zip already has the `walker-finance/` folder at its top level, which is what Claude expects.
3. Go to **Customize → Skills**, click **+**, and upload the zip. Keep the skill toggled on.

Custom skills you upload are private to your account.

## 2. Connect your data (3 min)

1. In Claude's connector settings, connect **Gmail** and **Google Drive**.
2. In Google Sheets, create a sheet named **`Walker Finance Ledger`** with three tabs: **Ledger**, **Review**, **Config**.
   - Paste the header row from [`ledger-template.csv`](../walker-finance/assets/ledger-template.csv) into **Ledger** and **Review**.
   - Paste [`config-template.csv`](../walker-finance/assets/config-template.csv) into **Config** and fill it in using [SETUP.md](../SETUP.md).
3. *(Optional)* Open **Personal Finance** in Claude's sidebar and link your bank and card accounts. Then set `bank_link_available = yes` in Config. This gives you the monthly cash-flow view, so the skill doesn't have to rebuild it.

> [!NOTE]
> If your Drive connector can read the sheet but not edit it, the skill falls back to manual mode. It returns the rows, and you paste them into the sheet yourself.

## 3. Turn on pings

**Without Duet.** The skill works on demand, so you just ask. If your Claude has scheduled tasks, create one that runs every 4 hours with this prompt:

```text
Run the walker-finance scheduled check. Only message me if a ping rule fires.
```

**With Claude Duet** (US Pro/Max waitlist). Duet carries over your memory, skills, and connected apps from your Claude account, so nothing needs reinstalling. Tell Duet once:

```text
When you check my accounts, use walker-finance's scheduled check rules. Put one spending line in my morning brief and only message me separately when a ping rule fires.
```

> [!IMPORTANT]
> Personal Finance isn't available inside Duet, so Duet's checks run from the card-alert emails. That's exactly what the Spending monitor is designed for.

## 4. Try it

```text
What did I spend yesterday?
Anything in my Review tab I should look at?
Run a scheduled check now and tell me what would have pinged.
```

## 5. Test checklist

- [ ] "What did I spend yesterday?" returns a total **and** names which cards were checked.
- [ ] Asking twice in a row doesn't add duplicate rows to the Ledger tab.
- [ ] Turning off one card's alerts (or using a card with no alerts) produces a coverage warning, not a lower total.
- [ ] A scheduled run with nothing to report sends nothing.
- [ ] The skill refuses to pay, book, or move money, and says that you do those yourself.
