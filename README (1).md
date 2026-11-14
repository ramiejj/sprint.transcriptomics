# Data

| File | Contents |
|---|---|
| `GSE126296_GEO2R_top_table.tsv` | Full GEO2R output for all 33,297 probes: probe ID, gene symbol, gene title, log2 fold change, unadjusted p, Benjamini–Hochberg adjusted p, moderated t, B-statistic. Groups ordered post vs pre, so positive logFC = induced by sprinting. |
| `genes_induced_strong_68.txt` | 68 named genes: adj. p < 0.05 and \|logFC\| > 1. |
| `genes_induced_all_248.txt` | 248 named genes: adj. p < 0.05, any magnitude. |
| `genes_repressed_75.txt` | 75 named genes: adj. p < 0.05, any magnitude. |
| `gprofiler_multiquery_input.txt` | Induced and repressed lists formatted for g:Profiler multiquery mode. |

Probes without a gene symbol were excluded from the derived lists, since enrichment tools cannot map them.

Raw CEL files are not redistributed here; they are available from GEO under accession GSE126296.
