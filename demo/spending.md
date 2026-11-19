# Spending chat demos

Load [Spending](../agents/spending.md) and the [ledger rules](../shared/transaction-ledger.md). Paste only the inputs and Walker's messages. All data are fictional.

~~~text
Demo run: 2026-11-15 19:00 America/Los_Angeles. Threshold: USD 500.
Chase and Amex reads succeeded for November 14 through the run time.
source_key,account,transaction_date,merchant,amount,currency,type,status
c01,Chase,2026-11-14,Sample Hotel,350,USD,purchase,pending
c01,Chase,2026-11-14,Sample Hotel,350,USD,purchase,pending
a01,Amex,2026-11-14,Sample Airline,250,USD,purchase,pending
c02,Chase,2026-11-15,Sample Grocer,350,USD,purchase,pending
a02,Amex,2026-11-15,Sample Rail,250,USD,purchase,pending
~~~

**Walker:** What did I spend yesterday?

**Agent:** I observed $600 on November 14 across Chase and Amex. It came from two pending purchases, $350 for Sample Hotel and $250 for Sample Airline. That's $100 over your daily threshold.

**Walker:** Am I over $500 today? Can you notify me if I do this again?

**Agent:** Today's observed purchases total $600 through 7 p.m., so you're $100 over. I can flag crossings when a digest runs. This demo has no push schedule configured.

**Variation.** Start a fresh run. Remove Amex rows and change its read status to failed. Ask for yesterday again. The reply should give $350, say Chase only, and avoid implying that combined spend stayed below $500. With both sources successful and zero rows, expect “no purchases observed” instead.
