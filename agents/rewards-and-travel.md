# Rewards and Travel

| Input | Requirement |
|---|---|
| Card offers or welcome bonuses | Issuer terms, card alias, benefit, deadline, eligibility, activation status if known, and any confirmed eligible progress. Planned purchases are optional. |
| International flights | Dates or flexibility, airports, cabin, traveler count, and relevant cash budget or points programs. Use sourced quotes or explicitly supplied demo quotes. |
| Alert criteria | Optional. Walker specifies routes or offer deadlines and a working schedule if he wants proactive monitoring. |

## Paste-ready instructions

~~~text
For card offers, show benefit, required eligible spend, cap, card alias, expiration and activation state. Rank by estimated savings on purchases Walker already plans to make, when terms allow comparison. Use confirmed eligibility and activation to calculate applied credits. Show conditional value separately. Exclude expired offers from active results. For welcome bonuses, subtract only confirmed eligible and posted spend from the requirement, flag uncertain spend, and show the deadline.

For international flights, return a short list within Walker's route, dates, cabin and traveler constraints. For each quote show route and dates, cash total or points plus taxes and fees, program where relevant, source and time checked. Distinguish verified availability from estimates, missing fees and stale quotes. Compare against the trip budget when supplied and keep points visible separately. Surface relevant card offers without reducing the fare by an unconfirmed credit. If requested and supported, evaluate monitoring criteria against fresh sources. Describe a schedule as active only if verified.

Treat demo quotes as fictional. Walker checks final eligibility and availability, activates the offer and books the trip himself.
~~~

**Output.** Offer or bonus status, flight comparison, or a combined answer when asked about a planned booking.

**Evals.** 10% back with a $20 cap yields $15 on $150 of eligible planned spend. An unconfirmed $50 credit leaves the base $620 fare intact. See the [chat demos](../demo/rewards-and-travel.md).
