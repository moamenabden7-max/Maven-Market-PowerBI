# Finish and verify in Power BI Desktop

The original PBIX has not been rewritten. Binary model edits and a guessed conversion to PBIP are deliberately avoided. The following is the remaining application workflow, not a completion claim.

1. Open the PBIX and **Save As** a working copy. Capture the current KPI totals and active filters.
2. Apply the formula replacements in [measure-fixes.dax](../improvements/measure-fixes.dax) one measure at a time. Use Transaction Rows as the business label for COUNTROWS; preserve existing measure references until visuals are updated.
3. Save as **Power BI Project (.pbip)** with the PBIR report format. Run the script against the exported **.Report** folder:

```bash
python tools/polish_pbir.py "path/to/Project.Report"
```

The script makes a sibling backup first. It renames known pages, orders the business pages, sets the overview as the active page, and replaces the AdventureWorks margin donut with clustered bars when present. It does not alter DAX or the semantic model. It was structurally tested against the Maven PBIR definition; the AdventureWorks legacy report must first be converted by Desktop.

4. Apply external changes/reopen in Desktop. Import [portfolio-theme.json](../improvements/portfolio-theme.json) from the Themes menu. Confirm contrast and alignment. Use Monthly Revenue Target as the gauge target and Revenue Gauge Maximum as its maximum. Prefer shared store/region geography for side-by-side sales and return comparisons.
5. Check every page at 100% zoom, filters, reset buttons, tooltip/drillthrough behavior, target gauges and empty selections. Confirm previous-month comparisons with one month selected, and verify that transaction-row and order labels cannot be confused.
6. Compare unfiltered totals against [audit-results.json](audit-results.json). Small numeric rounding differences can occur; investigate material differences rather than forcing a match. Test refresh separately using your source files.
7. Export actual report pages to PNG or PDF, add them under assets/, and label them as Desktop exports. Save the verified PBIX and replace the current repository file only after successful reopening.

## References

- [Microsoft: PBIR report folders and supported external editing](https://learn.microsoft.com/power-bi/developer/projects/projects-report)
- [Microsoft: PBIP and Desktop conversion](https://learn.microsoft.com/power-bi/developer/projects/projects-overview)
- [Microsoft: DIVIDE](https://learn.microsoft.com/dax/divide-function-dax)

The image in the repository README is an independent data-derived analysis graphic, not a Desktop export.
