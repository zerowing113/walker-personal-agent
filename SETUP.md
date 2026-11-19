# Setup questionnaire

> [!CAUTION]
> **Don't fill this in on GitHub.** This repo is public. Copy the questions, answer them privately, and put your answers in the **Config** tab of your own `Walker Finance Ledger` spreadsheet. The assistant reads them from there.

This takes about 10 minutes. Each answer maps to one row in the Config tab (the key is shown in code font). Blank is fine for anything optional.

## 1. Basics (required)

| Question | Config key | Your answer |
|---|---|---|
| Which time zone should "today" and "yesterday" use? | `time_zone` | |
| Which currency do you think in? | `currency` | |

## 2. Your cards (one row per card)

Turn on purchase alerts in each card's app first, ideally for every purchase. Then open one alert email and copy the sender address.

| Card nickname (e.g. Chase, Amex) | Alert email sender | Days of silence before I warn you (default 3) |
|---|---|---|
| | `card.<nickname>.alert_sender` | `card.<nickname>.silence_days` |
| | | |
| | | |

Use a nickname only. Never put a card or account number anywhere.

## 3. When should I ping you?

| Question | Config key | Your answer |
|---|---|---|
| Ping me when I've spent more than this in one day | `daily_threshold` | |
| Ping me about any single purchase at or above | `large_purchase_amount` | |
| Don't ping me between (for example 22:00-07:00) | `quiet_hours` | |
| Turn pings on? (yes / no) | `pings_enabled` | |

## 4. Optional

| Question | Config key | Your answer |
|---|---|---|
| Have you linked your bank accounts in your assistant's read-only finance feature? (yes / no) | `bank_link_available` | |
| How much have you set aside for travel? | `travel_reserve` | |
| Which points or miles programs do you use? | `loyalty_programs` | |
| Try preview modules in scheduled checks? (e.g. `rewards-and-travel`) | `preview_modules` | |

## 5. Check yourself

- [ ] My spreadsheet is named `Walker Finance Ledger` and has **Ledger**, **Review**, and **Config** tabs.
- [ ] The Ledger tab's first row matches [the template](walker-finance/assets/ledger-template.csv).
- [ ] Every card I care about sends alert emails.
- [ ] Nothing in this repo contains my real details.
