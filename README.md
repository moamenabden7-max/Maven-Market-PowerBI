# Maven Market | Power BI Analytics

Retail performance and product-brand analysis by **Moamen Taha Abuzied**.

[Power BI project](./maven%20market.pbip) · [Model & DAX](docs/MODEL.md) · [Quality review](docs/QUALITY_REVIEW.md)

![Static analysis summary, recomputed from the original imported data](assets/analysis-summary.svg)

## Business focus

Explore revenue, product costs, gross profit, return quantities and product-brand performance across time and locations. The report includes prior-month KPI comparisons, weekly revenue, a brand table, a map, and date/country filters.

## Open the project

1. Download the **whole repository** using **Code → Download ZIP**, or clone it.
2. Extract the ZIP and keep `maven market.pbip`, `maven market.Report` and `maven market.SemanticModel` together.
3. Open `maven market.pbip` in Power BI Desktop with support for PBIP/PBIR projects.
4. Configure the Power Query source paths to your original Maven Market source files, then refresh.

The PBIP file is an entry point; downloading it alone is insufficient. Local data cache and machine-specific settings are excluded. Original source files are not distributed here, so a fresh checkout requires those files to load the data. The former PBIX is no longer part of the current branch.

## Project structure

| Path | Purpose |
| --- | --- |
| `maven market.pbip` | Project entry point |
| `maven market.Report/` | Report pages, visuals and resources |
| `maven market.SemanticModel/` | Tables, Power Query, DAX and relationships |
| `assets/` | Portfolio analysis graphic |
| `docs/` | Model reference, review and historical audit evidence |
| `improvements/` | Optional measure replacements and theme |
| `tools/audit_model.py` | Aggregate audit of a locally supplied PBIX |
| `requirements.txt` | Dependencies for the optional audit |

## Historical data snapshot

These figures were independently recomputed from the original PBIX's imported data using Python. They are not DAX-engine results or a validation of the uploaded PBIP project.

| Metric | All original imported data |
| --- | ---: |
| Dates | 1997-01-01–1998-12-30 |
| Transaction rows | 269,720 |
| Units sold | 833,489 |
| Revenue | 1,588,091.80 |
| Product cost | 711,727.66 |
| Gross profit | 876,364.14 |
| Gross margin | 55.18% |
| Returned units / sold units | 0.99% |

A distinct order ID is not present in the fact table. Gross profit excludes operating expenses; amounts use the model's monetary units. [Audit evidence and original source hash](docs/audit-results.json).

## Model and validation

Revenue uses `Products[Discount_Price]`. Monthly Revenue Target is 105% of prior-month revenue. The [quality review](docs/QUALITY_REVIEW.md) documents outstanding issues; the files under `improvements/` are optional proposals, not applied fixes.

The uploaded project folder structure has been restored. Opening in Desktop, refreshing data, executing DAX and checking visual interactions still require verification.

To repeat the historical audit, supply your own PBIX exported from Desktop:

```bash
python -m pip install -r requirements.txt
python tools/audit_model.py "/path/to/your-report.pbix" --output audit-results.json
```

## More work

[AdventureWorks sales analysis](https://github.com/moamenabden7-max/AdventureWorks-Sales-PowerBI) · [LinkedIn](https://www.linkedin.com/in/moamen-taha-data-analyst/)
