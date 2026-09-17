# Power BI Dashboard: Setup Guide

This folder contains a Power BI Project (PBIP) for the Gulf Crest teaching module. It was built as text
files (TMDL for the data model, PBIR for the report) rather than a single opaque `.pbix` file, which is
Microsoft's newer, source-control-friendly format and the reason it can be generated outside Power BI
Desktop at all.

## Why This Needs Windows, at Least Once

Power BI Desktop, the tool that actually loads this project, connects it to the CSV data, and renders the
visuals, only runs on Windows. There is no Mac version. The data model in this folder (every table, every
relationship, every measure) was built and can be fully reviewed as plain text without Windows, but opening
it, loading the data, and publishing it needs a Windows machine at least once. After that, viewing and
sharing the finished dashboard works from any browser, Mac included, through Power BI Service.

## Setup Steps

1. **Copy this whole `06_PowerBI` folder** onto the Windows machine, keeping `GulfCrest_Dashboard.pbip`,
   `GulfCrest_Dashboard.SemanticModel`, and `GulfCrest_Dashboard.Report` together in the same parent folder.
   Also copy the `04_Datasets` folder onto that machine (or make sure it is reachable, for example through a
   synced cloud folder).

2. **Install Power BI Desktop** (free) from the Microsoft Store or https://powerbi.microsoft.com/desktop/.

3. **Open `GulfCrest_Dashboard.pbip`** by double-clicking it. Power BI Desktop will load the semantic model.

4. **Point the `DatasetsFolder` parameter at your local `04_Datasets` folder.** Go to
   **Transform Data > Manage Parameters**, find `DatasetsFolder`, and set its value to the full path of the
   `04_Datasets` folder on that machine, ending in a backslash, for example:
   `C:\Users\yourname\Documents\cas\04_Datasets\`

5. **Refresh the model** (Home > Refresh). All 8 tables should load, and the relationships and measures are
   already wired up.

6. **Add the visuals.** The report currently has six empty pages (Executive Summary, Claims Dashboard, Fraud
   Dashboard, Reserve Dashboard, Financial Dashboard, Scenario Dashboard) with no visuals placed yet, matching
   the structure of the Python/Plotly companion dashboard. Hand-authoring every visual's layout as raw JSON
   without a way to open and check it first is too easy to get subtly wrong, since the visual file format is
   intricate, so this one step is left as a manual pass in the Desktop GUI. `DASHBOARD_BUILD_GUIDE.md` in this
   folder lists exactly which visual to add to each page and which fields go into it, including a few chart
   types beyond the basics (gauge, funnel, treemap, waterfall, and a box-and-whisker chart, the last of which
   needs a free custom visual imported from AppSource since Power BI has no built-in box plot). Budget closer
   to 45 to 60 minutes for this pass given the added variety of visual types across six pages.

7. **Publish.** File > Publish > Publish to Power BI (sign in with a free Microsoft account if needed).

8. **Make it viewable from any browser without a Power BI account.** In Power BI Service (app.powerbi.com),
   open the report, go to File > Publish to Web, and use the generated public link. Since this dataset was
   built for a teaching exercise and contains no real policyholder or claimant information, there is no
   data-privacy concern with making it public this way, and it means anyone reviewing the submission can open
   it directly in a browser, Mac or otherwise, without installing anything.

## If Something Doesn't Open Cleanly

The semantic model (tables, relationships, measures) is the part most worth trusting, since TMDL is a
simpler, better-documented format. If Power BI Desktop reports a problem with a specific file, that file is
still plain text and can be opened in any editor to see exactly what it contains and fix it directly; nothing
here is a binary blob that has to be regenerated blind.
