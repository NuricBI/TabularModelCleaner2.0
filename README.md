# Tabular Model Cleaner 2.0

A **free tool for Power BI and Microsoft Fabric** that finds the measures, columns and tables
your semantic model no longer needs — and tells you which ones are safe to remove.

As models grow they accumulate unused objects: refreshes get slower, the model gets harder to
read, and cleaning it by hand is risky because one wrong delete breaks a downstream report.
This tool maps every dependency first, so you decide with the full picture.

📖 **[Full instructions and screenshots →](https://nudatabi.com/blog/tabular-model-cleaner-2-0-for-microsoft-power-bi-and-fabric/)**
⬇️ **[Download the .pbix →](https://github.com/NuricBI/TabularModelCleaner2.0/blob/NuricBI/Tabular%20Model%20Cleaner%20tool%202.0.pbix)**

## What it does

- **Finds unused objects precisely.** Detects which measures, columns, calculated columns and
  tables are actually used by your connected reports — and which are not.
- **Traces nested dependencies.** Follows measure-to-measure chains down to the deepest level,
  so a column used indirectly is never reported as unused.
- **Detects filter usage.** Fields used in report, page and visual filters count as used.
- **Handles partitioned tables correctly.** Partitions are no longer double-counted.
- **Shows usage per report.** Which report, which page, which visual type uses each object.

## How it works

- **Object dependencies** — reads the model's Dynamic Management Views (notably
  `DISCOVER_CALC_DEPENDENCY`) and builds a hierarchical dependency tree with a custom Power
  Query function.
- **Report usage** — parses the metadata of your connected reports (visuals, report-level
  measures, filters and bookmarks) and cross-references it with the dependency map.

## Requirements

- Power BI Desktop
- [DAX Studio](https://daxstudio.org/) — to get the local server, port and database GUID
- [Report Analyzer](https://github.com/m-kovalsky/ReportAnalyzer) — to export the metadata of
  the connected reports
- Access to the semantic model: a local Power BI file, or the XMLA endpoint of a workspace on a
  Fabric capacity (F SKU), Premium Per User, or Power BI Premium

## Quick start

1. **Connect to the model.** Local: open the file, connect DAX Studio (*PBI / SSDT Model*) and
   copy the `localhost:port` plus the database GUID from
   `SELECT * FROM $SYSTEM.DBSCHEMA_CATALOGS`. Fabric/Premium: copy the workspace connection
   string from the workspace settings and use the semantic model name as the database.
2. **Export report metadata.** Put every report connected to the model in one folder and run
   Report Analyzer → *Export Report Metadata*.
3. **Set the parameters.** Open the `.pbix`, set the dataset server and database, point
   `LocalSourcePBITemplates` at the metadata folder, and refresh.

Full walkthrough with screenshots in the [blog post](https://nudatabi.com/blog/tabular-model-cleaner-2-0-for-microsoft-power-bi-and-fabric/).

## Before you delete anything

- Back up the model first.
- Include **every** report connected to it — a missing report means missing dependencies.
- When in doubt, hide before deleting.

## License

MIT — free to use, modify and distribute.

---

Built by [Nuric Ugarte](https://www.linkedin.com/in/nuricugarte/) — MCT, editor of the official
DP-600 certification book. More on Fabric and Power BI at **[nudatabi.com](https://nudatabi.com)**.
