# Campaign Monitor v5

Open `index.html` in a current browser, or use GitHub Pages. Reports are processed locally in a Web Worker and saved in IndexedDB on that browser; they are not uploaded. XLSX and CSV exports must include GAM report properties (time zone and date range) and the required dimensions and metrics. Legacy binary XLS files are not supported.

## Calculation policy

- Source totals include the entire imported period and reconcile exactly with the line-item and daily aggregates.
- Pacing uses only complete dates. Its cutoff is the earlier of the report end and the day preceding the export-generation date/current local date. If an export timestamp is unavailable, the initial import date is used. Reopening a partial historical export does not turn it into a complete day.
- Linear reference = delivered on complete dates / expected lifetime impressions at cutoff − 1. This is a reference model, not GAM Progress. Overrides can disable this model for special schedules.
- Required rate = max(0, booked goal − complete-date delivery) / remaining real 24-hour periods. DST is respected in the report time zone. Displayed required rates round upwards.
- Recent rate requires three consecutive complete dates inside both the report and the flight. Missing delivery on a covered date counts as zero. Normalize actual elapsed hours to 24-hour periods.
- Projected final delivery = complete-date delivery + recent rate × remaining real 24-hour periods. This is a constant-rate scenario, not an inventory forecast, confidence interval, or GAM guarantee.
- Sponsorship, incomplete lifetime history, inconsistent/missing times, conflicting goals and filtered inventory do not receive an impression-goal projection. Paused/inactive items do not receive an actionable required rate.
- CTR/viewability use count ratios, never averages of percentages. Row-level viewability inconsistencies retain raw counts but block the derived rating. Sample-size and tracking checks apply.

## Validation

21 deterministic core tests and 882 browser integration assertions passed in Chromium. These include an independent Python reconciliation of all 109,780 rows, 281 line items and every daily/metric total of the supplied report; Excel 1900/1904 date systems and shared strings; CSV delimiters; corrupt ZIP checksum rejection; preserved previous snapshots after failed imports; settings, persistence, filtering, detail dialogs, and 320/375/768/1440px layouts.

The private source report and browser data are not included in this deployment. No live GAM API, ad-serving behavior or available inventory is validated.

The bundled SAX XML parser is sax 1.6.0, distributed under its license in SAX-LICENSE.txt.
