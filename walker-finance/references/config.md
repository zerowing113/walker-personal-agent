# Config

Walker's settings live in the **Config** tab of his private ledger spreadsheet, never in this skill and never in a public repo. Each row is `key, value`. A blank template is in [../assets/config-template.csv](../assets/config-template.csv), and Walker fills it in using [SETUP.md](https://github.com/zerowing113/walker-personal-agent/blob/main/SETUP.md).

## Fields

| Key | Example | Required | Used by |
|---|---|---|---|
| `time_zone` | `America/Los_Angeles` | Yes | Every date |
| `currency` | `USD` | Yes | Totals and threshold |
| `card.<alias>.alert_sender` | `card.chase.alert_sender = alerts@example-bank.com` | One per card | Spending import |
| `card.<alias>.silence_days` | `3` | No (default 3) | Card gone quiet |
| `daily_threshold` | `500` | No | Threshold crossed |
| `large_purchase_amount` | `400` | No | Large purchase |
| `quiet_hours` | `22:00-07:00` | No | Scheduled check |
| `pings_enabled` | `yes` | No (default no) | Scheduled check |
| `bank_link_available` | `yes` | No | Cash Flow fallback |
| `travel_reserve` | `650` | No | Preview: Finance Planning, Rewards & Travel |
| `loyalty_programs` | `Sample Miles` | No | Preview: Rewards & Travel |
| `preview_modules` | `rewards-and-travel` | No | Turns preview modules on for scheduled runs |
| `last_check_at` | written by the agent | No | Scheduled check |

## Rules

- Read Config at the start of every run. Never cache it across runs.
- If a required field is missing, ask one focused question in chat. In a scheduled run, skip the dependent rule and note it.
- Only Walker edits Config. The agent may write `last_check_at` only.
