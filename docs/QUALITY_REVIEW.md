# Quality review

Status: findings verified from the current model and report metadata; proposed Desktop changes are not yet applied.

## Findings requiring Desktop changes

| Priority | Finding | Proposed action |
| --- | --- | --- |
| High | Total Orders and Total Transectionn both use COUNTROWS(Transection). No order ID exists in that fact table. | Label both as transaction rows; do not claim distinct orders. Reuse one canonical measure where practical. |
| Medium | Return Rate uses `/`. | Replace with `DIVIDE([Quantity Return], [Quantity Sold])`. |
| Medium | Monthly Revenue Target is used as a gauge maximum instead of a target marker. | Put the target on the target marker, and use an actual/target-based maximum. |
| Medium | Country/map visuals use customer geography, but the return fact has no customer relationship. | When comparing sales and returns by location, use a shared store/region dimension that filters both fact tables; otherwise clearly distinguish the filter context. |
| Low | Page is named Page 1 and transaction measures contain spelling errors. | Rename the page Retail Overview; rename measures through Desktop to update dependencies. |

## Documentation corrections applied

- The actual transaction dates are **1997-01-01 to 1998-12-30**, not 2017–2018.
- Revenue uses **Products[Discount_Price]**, not the unadjusted retail price.
- The brand table currently contains transaction-row count, profit, profit margin and return rate; it does not have a revenue column.
- The 269,720 fact rows are transaction rows; distinct order count is not inferable from a missing order identifier.

## Checks performed

- PBIX archive and JSON report definitions could be read.
- Product joins preserved the fact-row count; every fact product key matched.
- No fact rows had an unmatched customer key.
- Calendar dates were unique, nonblank and continuous, and covered every fact date.
- Recomputed monthly revenue reconciled to the all-row revenue total within 0.01.

These checks do not execute DAX, render report visuals, refresh source files or validate every filter interaction.
