# Packaged Candy: Trade Promotion Effectiveness

**Question:** Which promotional discount depths earn their cost in packaged candy, and where should a brand shift promo spend?

**Data:** Dunnhumby *The Complete Journey* (Kaggle): `transaction_data.csv`, `product.csv` (not included; download from Kaggle). 2,500 households, 102 weeks. Category: CANDY - PACKAGED; 25 top SKUs with enough promo and non-promo weeks.

## Method
1. Built a SKU-week panel; regular price = (sales - retail discount) / units; promo week = 5%+ off.
2. Baseline = each SKU's mean units in non-promo weeks. Lift = promo units / baseline - 1.
3. Promo ROI = incremental profit / discount dollars given on all units sold, at a **40% gross margin assumption** (sensitivity 30-50% included).
4. Confidence bands: bootstrap resampling of SKUs (10th-90th percentile).
5. Validation: Poisson regression with SKU and week-of-year fixed effects, depth buckets, clustered standard errors.

## Findings
| Depth | Weeks | Lift | ROI |
|---|---|---|---|
| 5-15% | 77 | +185% | +82% |
| 15-25% | 80 | +220% | +32% |
| 25-35% | 562 | +708% | +15% |
| 35-50% | 147 | +451% | -16% |
| 50%+ | 9 | +263% | -50% |

- Overall promo ROI: +9%. 68% of spend sits at 25-35% off; 25% ran 35%+ off.
- Lift at 35-50% off is not statistically different from 25-35% (p = 0.62): the extra discount buys no extra volume.
- No post-promo dip (week +1 units run about 30% above baseline), so no pantry-loading adjustment was made.
- **Recommendation:** cap depth at ~30% (reprice 156 weeks, 25% of spend); test 15-25% on top multipacks. Sizing: +$234 profit in the sample (+$211 to +$256 for 20% to 0% volume loss), taking ROI from 9% to 17%.

## Limitations
- Household panel sample: dollar figures are sample-level, not market-level.
- Margin is assumed (not in the data); conclusions at depth >30% are sensitive to it.
- `causal_data` (display/mailer) not used; no cannibalization analysis; discounts are loyalty-card discounts, not manufacturer trade rates.
- Sparse weekly volumes per SKU; shallow-depth buckets have few observations.
- Next step: replicate on Circana/Nielsen data with trade-rate and cost data.
