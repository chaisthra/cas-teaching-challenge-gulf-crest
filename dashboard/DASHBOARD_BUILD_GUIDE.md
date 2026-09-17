# Dashboard Build Guide

This is the visual-by-visual specification for the six report pages, mirroring the structure of the
Python/Plotly companion dashboard (`local/dashboard_preview/GulfCrest_Interactive_Dashboard.html`). The data
model already has every field and measure needed; this guide only covers what to place on the canvas, which
Power BI visual type to use, and which fields go into it.

Several pages call for a visual type beyond the basic bar, line, and donut. Power BI ships gauge, funnel,
treemap, and waterfall charts as native visuals; a box-and-whisker chart requires enabling a Microsoft-certified
custom visual (Box and Whisker Chart, free, from AppSource) since Power BI has no built-in box plot.

## Page 1: Executive Summary

**KPI cards (top row):**
- Total Claims
- Total Reported Severity
- Catastrophe Claims (with Routine Claims as a comparison card)
- Open Claims (with Closed Claims as a comparison card)
- Total Insured Value
- Fraud Rate

**Claims by zone (bar chart):**
- Axis: `Policies[zone_id]`
- Values: `[Total Claims]`

**Claims by coverage type (donut chart):**
- Legend: `Policies[coverage_type]`
- Values: `[Total Claims]`

**Claims over time, routine vs. catastrophe (line chart):**
- Axis: `Claims[date_of_loss]` (Month granularity)
- Values: `[Total Claims]`
- Legend: `Claims[is_catastrophe_flag]`, so the routine baseline stays visible next to the Hurricane Marisol
  spike rather than being flattened by a single combined series
- Add a text box or the built-in "analytics: line" annotation naming the Marisol quarter on the spike

**Average severity, catastrophe vs. routine (clustered column):**
- Axis: `Claims[is_catastrophe_flag]`
- Values: `[Average Claim Severity]`

**Fraud rate gauge (Gauge visual):**
- Value: `[Fraud Rate]`
- Target/threshold: set a constant line at 15% (Format pane > Gauge axis > Target) to mirror the
  monitoring-threshold gauge in the Python dashboard

## Page 2: Claims Dashboard

**Severity by cause of loss (bar chart):**
- Axis: `Claims[cause_of_loss]`
- Values: `[Average Claim Severity]`
- Sort descending by value

**Claims by status (donut chart):**
- Legend: `Claims[claim_status]`
- Values: `[Total Claims]`

**Catastrophe vs. routine claim counts (clustered column):**
- `[Catastrophe Claims]` and `[Routine Claims]` as two columns

**Claims by construction type (bar chart):**
- Axis: `Policies[construction_type]`
- Values: `[Total Claims]`

**Severity by zone (bar chart):**
- Axis: `Policies[zone_id]`
- Values: `[Average Claim Severity]`

**Severity distribution by zone (Box and Whisker Chart, custom visual):**
- Category: `Policies[zone_id]`
- Value: `Claims[reported_severity]`
- Shows the spread and outliers behind each zone's average, not just the mean

**Claim volume by zone and cause of loss (Treemap):**
- Group: `Policies[zone_id]`, then `Claims[cause_of_loss]`
- Values: `[Total Claims]`

## Page 3: Fraud Dashboard

**KPI cards:**
- Investigated Claims
- Confirmed Fraud Claims
- Fraud Rate

**Investigated vs. not investigated (donut chart):**
Needs a measure comparing `FraudLabels[is_fraud]` being blank versus not; a simple version is a card showing
`[Investigated Claims]` next to a card showing `[Total Claims] - [Investigated Claims]` labeled "Not Yet
Investigated," or a donut fed by those two values.

**Fraud rate by catastrophe flag (clustered column):**
- Axis: `Claims[is_catastrophe_flag]`
- Values: `[Fraud Rate]`

**Fraud rate by cause of loss (bar chart):**
- Axis: `Claims[cause_of_loss]`
- Values: `[Fraud Rate]`
- Sort descending; add data labels showing the investigated count per cause for context

**Fraud detection model comparison (clustered column chart):**
This compares approaches from Notebook 4 rather than live data. Add a small disconnected table (Enter Data)
with columns Model, Precision, Recall, F1, and the six rows from the notebook (Naive, Baseline, Class
weighting, SMOTE, SMOTE + recall-targeted threshold, Gradient boosting + tuned threshold), then chart it as a
clustered column with Model on the axis and the three metrics as values.

**Recall-target sensitivity (line chart):**
Another disconnected table (Enter Data): Target Recall [50, 60, 70, 80, 90] against Resulting F1, from
Notebook 7.

**Fraud investigation funnel (Funnel visual):**
- Category: a disconnected table with rows "Total Claims," "Investigated," "Confirmed Fraud"
- Values: `[Total Claims]`, `[Investigated Claims]`, `[Confirmed Fraud Claims]`

**Fraud rate heatmap: cause of loss x catastrophe flag (Matrix visual with conditional formatting, or the
Heatmap custom visual):**
- Rows: `Claims[cause_of_loss]`
- Columns: `Claims[is_catastrophe_flag]`
- Values: `[Fraud Rate]`, with background-color conditional formatting on a red scale

## Page 4: Reserve Dashboard

**KPI cards:**
- Total Paid to Date
- Total Reserve Estimate

**Reserve development over time (line chart):**
- Axis: `ReserveHistory[development_month]`
- Values: Average of `ReserveHistory[cumulative_paid]`

**Paid vs. reserved (clustered column or two cards):**
- `[Total Paid to Date]` and `[Total Reserve Estimate]`

**Chain Ladder vs. Bornhuetter-Ferguson for Hurricane Marisol (bar chart, log-scale value axis):**
Disconnected table with two rows (Naive Chain Ladder: $46,678.84; Bornhuetter-Ferguson: $159,637,651.24), from
Notebook 5. Set the value axis to a logarithmic scale (Format pane > Y axis > Type: Log) since the two
estimates differ by more than three orders of magnitude.

**BF ultimate sensitivity to percent-paid assumption (line chart):**
Disconnected table: Assumed Percent Paid [2, 3, 5, 8, 10, 15] against BF Ultimate ($M), from Notebook 7.

**Bornhuetter-Ferguson build-up (Waterfall visual):**
- Category: a disconnected table with rows "Paid So Far (5%)," "IBNR Load (Expected Prior)," "BF Ultimate"
  (the last marked as a Waterfall "total")
- Values: $7.98M, $151.66M, $159.64M respectively (from the same Notebook 5 base case)

**Cumulative paid growth (Area chart):**
Same source as the reserve development line chart, rendered as a stacked or basic area chart instead of a
line, to emphasize the cumulative build-up.

## Page 5: Financial Dashboard

**KPI cards:**
- Total Insured Value
- Total Written Premium

**Earned premium vs. incurred losses (line chart):**
- Axis: `CompanyFinancials[period]`
- Values: Sum of `CompanyFinancials[earned_premium]` and Sum of `CompanyFinancials[incurred_losses]`
  (two series on the same chart makes the Marisol quarter's spike visible immediately)

**Policyholder surplus over time (line chart):**
- Axis: `CompanyFinancials[period]`
- Values: Sum of `CompanyFinancials[policyholder_surplus]`

**Economic indicators (line chart):**
- Axis: `EconomicIndicators[date]`
- Values: `EconomicIndicators[construction_cost_index]` and `EconomicIndicators[wage_index]`

**Written premium vs. policyholder surplus (Combo chart — Line and Stacked Column):**
- Axis: `CompanyFinancials[period]`
- Column values: Sum of `CompanyFinancials[gross_written_premium]`
- Line values (secondary axis): Sum of `CompanyFinancials[policyholder_surplus]`

## Page 6: Scenario Dashboard

**BF ultimate vs. percent-paid assumption:**
Reuse the line chart built on Page 4, or rebuild it here from the same disconnected table.

**Triage capacity sensitivity (line chart, dual axis):**
Disconnected table: Capacity [50, 75, 100, 125, 150] against Days to Clear Backlog and $-Weighted Avg Days
(from Notebook 6/7). Put Days to Clear Backlog on the primary axis and $-Weighted Avg Days on the secondary
axis.

**Fraud recall-target sensitivity (F1):**
Reuse the line chart from Page 3, or rebuild it here from the same disconnected table.

## General Notes

- Use the **Format pane** to apply consistent number formatting (the measures already carry a default
  format string, so this mostly matters for axis labels and the disconnected-table visuals above, which
  need formatting set manually).
- A **slicer** for `Claims[is_catastrophe_flag]` placed on Page 2 lets a viewer toggle between catastrophe
  and routine claims across every visual on that page.
- The Box and Whisker Chart and (if used instead of a formatted matrix) Heatmap visuals must be imported once
  from AppSource before they appear in the visualizations pane; both are free and Microsoft-certified.
- Keep chart titles matching the section headers above; a reviewer should be able to tell what each panel
  shows without opening it.
- Disconnected tables used only to chart hardcoded notebook figures (model comparison, sensitivity curves,
  Chain Ladder vs. BF, the waterfall build-up) should each carry a text box citing the source notebook, matching
  the source notes already present in the Python dashboard.
