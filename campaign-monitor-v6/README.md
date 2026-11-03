# Campaign Monitor v6

## Corrections

- Excel percentage cell styles now convert stored fractions into percentage points. The supplied GAM workbook contains Sponsorship values such as 0.5 with a percentage format: this is 50%, not 0.5%.
- Scientific-notation IDs and whole-number counts are normalized using exact decimal/BigInt arithmetic; unsafe integers and fractional counts are rejected before floating-point rounding can hide the error. Formatted CSV counts and percent signs are supported.
- CSV quoting is strict. Trimmed headers, ISO periods and English long month periods are accepted.
- Nonexistent/ambiguous local flight times at DST transitions block time-dependent calculations rather than silently choosing an offset.
- Lifetime coverage is independent of precise flight hours when lifetime delivery and the goal are comparable; required/day and projections still require valid times.
- Future starts no longer receive an incorrect 'incomplete history' label. Delivery outside the declared flight disables lifetime comparison.
- Reports without a valid export-generation timestamp conservatively exclude their final date. A historical partial export remains partial when reopened.
- Achieved goals receive a clear label without spurious pace alerts. Completed/paused/inactive items do not receive actionable future rates.
- CTR ratios and bounded viewability ratios are distinguished. Failed local settings persistence does not produce a false success message.
- v5 cached report snapshots require reimport because their discarded Excel cell formats cannot safely be reconstructed. Preferences are retained.

## Interface

Larger system typography (18px campaign names), clearer contrast, dark navigation, expandable orders, expand/collapse controls, filter reset, six overview priorities, a visible complete-day cutoff, and an explicit calculation breakdown. Layouts checked from 320 to 1536 pixels. The Save HTML button downloads the original source rather than a serialized DOM containing imported campaign data.

## Validation

32 deterministic core tests. 3,427 browser integration assertions, including independent Python comparisons for all 281 line items: source counts, daily counts, Sponsorship percentages, delivery cutoff, coverage, remaining goal, pacing deviation, required/day, recent rate, constant-rate projection, CTR and viewability. Another 3 assertions exercise settings-storage failures.

The workbook used for comparison was the supplied GAM export dated October 21, 2026: 109,780 rows. These checks do not establish the validity of any newer report that has not been supplied. Browser functional validation used Chromium over local HTTP. Direct file:// navigation was unavailable under this environment's browser policy; the delivered HTML embeds all runtime code and does not require external assets.

HTML validation passed recommended html-validate checks with style-policy rules no-inline-style and no-raw-characters disabled. No live GAM API or available inventory is queried. Projections are constant-rate scenarios, not guaranteed delivery or GAM forecasts.

The private source workbook, reference results, and screenshots are excluded from the published files. SAX 1.6.0 license is distributed alongside the online page.
