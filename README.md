# Transcriptomic response of human skeletal muscle to acute sprint exercise

A reanalysis of a public microarray dataset (GEO: **GSE126296**) asking whether a single bout of all-out sprinting activates genes associated with muscle growth, and how that squares with sprint training's inconsistent effect on muscle size.

*Independent project — James (Jamie) Joseph, BSc Biochemistry, University of Birmingham. November 2026.*

---

## Background and question

Sprint training reliably improves performance and mitochondrial capacity, but an increase in muscle cross-sectional area is **not** a consistent finding in longitudinal sprint studies. Resistance training, by contrast, reliably produces hypertrophy.

If sprinting does not reliably build muscle, does it activate the transcriptional programme associated with muscle growth at all?

This project reanalyses a published dataset to answer that, and to check whether the original paper's headline result reproduces.

## Dataset

| | |
|---|---|
| Accession | [GSE126296](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE126296) |
| Original study | Rundqvist et al. (2019), *PLoS ONE*, "Acute sprint exercise transcriptome in human skeletal muscle" ([10.1371/journal.pone.0223024](https://doi.org/10.1371/journal.pone.0223024)) |
| Participants | 14 healthy men and women |
| Protocol | Three all-out cycle sprints, 20 min recovery between each |
| Sampling | Muscle biopsy before the first sprint, and 2 h 20 min after the last |
| Platform | Affymetrix GeneChip Human Gene 1.0 ST Array (GPL6244), 33,297 probes |

This is a **reanalysis of published data**, not new experimental work. Reproducing a published result is part of the point.

## Methods

1. **Differential expression** — GEO2R (limma), pre vs post, Benjamini–Hochberg adjustment for multiple testing. Significance threshold adj. p < 0.05.
2. **Gene list construction** — three objective lists, no hand-picking:
   - strongly induced: adj. p < 0.05 and |logFC| > 1 → 91 probes, **68 named genes**
   - all induced: adj. p < 0.05, any magnitude → **248 named genes**
   - all repressed: adj. p < 0.05, any magnitude → **75 named genes**
3. **Enrichment analysis** — g:Profiler (version `e114_eg62_p19_9dc92ac8`, accessed 13 Nov 2026), *Homo sapiens*, g:SCS multiple testing correction, threshold 0.05. Induced and repressed lists run as separate queries. Sources: GO (MF/BP/CC), KEGG, Reactome, WikiPathways, TRANSFAC (TF), miRTarBase (MIRNA), Human Protein Atlas, CORUM, HPO.

Fold changes throughout are reported as **post vs pre**, i.e. positive values indicate induction by sprinting.

## Results

### Overall

**416 probes changed significantly** (adj. p < 0.05): 308 induced, 108 repressed. Only 3 repressed probes exceeded 2-fold, versus 91 induced.

### The published result reproduces

The original paper's headline finding was induction of immediate early genes. All of them are at the top of this reanalysis:

| Gene | Fold change (post/pre) | adj. p | Rank |
|---|---|---|---|
| EGR1 | 34× | 1.5 × 10⁻¹² | 1 |
| MAFF | 35× | 1.5 × 10⁻¹² | 2 |
| PPARGC1A (PGC-1α) | 4.2× | 3.3 × 10⁻¹⁰ | 3 |
| FOS | 43× | 9.2 × 10⁻⁹ | 9 |
| NR4A3 | 30× | 9.2 × 10⁻⁹ | 10 |
| JUNB | 14× | 5.1 × 10⁻⁸ | 15 |

### Growth and breakdown are induced together

This is the central finding for the research question. Genes promoting muscle growth and genes driving protein breakdown were induced **simultaneously**:

**Pro-growth**
- `MYC` 4.5× — drives protein synthesis and ribosome biogenesis
- `MYOD1` 2.3× — master myogenic regulator, activates satellite cells
- `SLC7A5` 1.9× and `SLC3A2` 1.3× — together form the LAT1 leucine transporter upstream of mTORC1
- `SMAD7` 1.6× — inhibits TGF-β/myostatin signalling
- `MSTN` (myostatin) **0.45× (2.2-fold decrease)**, adj. p = 0.021 — release of the main brake on muscle growth
- `XIRP1` 3.2×, `CYR61` 4.3× — mechanical strain response and matrix remodelling

**Pro-breakdown**
- `DDIT4` (REDD1) 6.4× — inhibits mTORC1
- `FOXO1` 1.7× — master regulator of muscle proteolysis
- `TRIM63` (MuRF1) 2.3× — E3 ubiquitin ligase, a direct FOXO target
- `CDKN1A` (p21) 1.3× — growth arrest

Independent support from enrichment analysis:
- **"Exercise and hypertrophy in skeletal muscle"** (WikiPathways WP516), adj. p = 3.0 × 10⁻³
- muscle structure development (GO:0061061), adj. p = 1.5 × 10⁻⁷
- muscle tissue development (GO:0060537), adj. p = 1.6 × 10⁻⁷
- striated muscle tissue development (GO:0014706), adj. p = 2.2 × 10⁻⁶
- amino acid transport complex (GO:1990184), adj. p = 3.4 × 10⁻²
- SMAD3–SMAD4–cJun–cFos complex (CORUM:2692), adj. p = 3.3 × 10⁻³
- FOXO-mediated transcription (Reactome), adj. p = 7.2 × 10⁻³
- ubiquitin protein ligase binding (GO:0031625), adj. p = 6.8 × 10⁻³

**Interpretation:** sprinting initiates a muscle remodelling programme, but activates synthesis and degradation arms concurrently. This is consistent with elevated protein *turnover* rather than net accretion, and offers a transcriptional explanation for why sprint training improves muscle quality without reliably increasing muscle size.

### Two hormone axes

**Catecholamine–cAMP–CREB.** Transcription factor binding site enrichment was dominated by the CREB/ATF family — CREB, CREB1, CREM, ATF-1, ATF-2, ATF-3 (adj. p 10⁻⁷–10⁻⁴) — which share the cAMP response element (CRE, core motif TGACGT). This is the pathway downstream of β-adrenergic signalling, consistent with the large catecholamine response to all-out sprinting. Notably, the *PPARGC1A* promoter contains a CRE site, offering a mechanism for the 4.2× induction of PGC-1α observed here.

**Glucocorticoid.** Four independent hits:
- nuclear receptors meta pathway (WP:WP2882), adj. p = 4.1 × 10⁻⁸ — the most significant pathway result in the analysis
- glucocorticoid receptor pathway (WP:WP2880), adj. p = 3.1 × 10⁻⁶
- nuclear glucocorticoid receptor binding (GO:0035259), adj. p = 2.4 × 10⁻³
- response to glucocorticoid (GO:0051384)

Supporting transcript-level evidence for hormone action: `CISH` 4.0× (a canonical growth hormone response marker) and `IRS2` 2.0× (insulin signalling).

### Metabolic and nutrient stress

- response to starvation (GO:0042594), adj. p = 1.9 × 10⁻⁶
- cellular response to nutrient levels (GO:0031669), adj. p = 1.5 × 10⁻⁵
- `PRKAG2` 3.0× (AMPK γ2 subunit), `PPP1R3B` 1.4× (glycogen resynthesis)
- `FLCN` 1.4× and `FNIP2` 1.9×, with the FLCN–FNIP2 complex enriched (CORUM:7430, adj. p = 5.0 × 10⁻²) — a direct regulator of mTORC1 and AMPK

**Integrated stress response:** `DDIT3` (CHOP) 2.0×, `ATF3` 3.2×, `EIF2AK3` (PERK) 1.4×, `CHAC1` 2.6×, with the CHOP–ATF3 complex enriched (GO:1990622, adj. p = 3.4 × 10⁻²).

### Angiogenesis

- vasculature development (GO:0001944), adj. p = 2.4 × 10⁻⁶
- blood vessel development (GO:0001568), adj. p = 4.1 × 10⁻⁶
- `VEGFA` 2.5×, `NOS3` 1.4×, `ANGPTL4` 1.7×, `ENG`, `TEK`

Consistent with reports that sprint training increases muscle capillary density, and with the broader observation that sprinting produces endurance-like adaptations.

### The response is activation-dominated

The 75 repressed genes yielded almost no enrichment: 3 GO:BP terms (best adj. p = 8.9 × 10⁻³) and **no** transcription factor, KEGG, Reactome or WikiPathways enrichment whatsoever. At this timepoint the acute sprint response is a transcriptional activation programme, not a suppression programme.

Relatedly, although the muscle-specific microRNA *MIR1-1* was itself induced, no enrichment of mir-1, mir-133 or mir-206 target genes was detected — consistent with a 2 h timepoint capturing the first transcriptional wave before downstream repression has taken effect.

## Limitations

1. **Transcript ≠ protein.** mRNA induction does not establish increased protein abundance or activity. Claims here are about transcriptional programmes, not measured muscle remodelling.
2. **Unpaired statistics.** GEO2R treats pre and post samples as independent groups, but the design is paired (the same 14 participants sampled twice). A paired analysis would be more sensitive and is likely to recover additional genes. *(Planned: see Next steps.)*
3. **No time-matched resting control.** Circadian genes changed (`PER3` and `NR1D2` down, `BHLHE40` 3.9× up), and with biopsies hours apart, time-of-day effects cannot be separated from exercise effects.
4. **Single timepoint.** 2 h 20 min post-exercise captures the immediate early wave only.
5. **Enrichment artefacts.** Several highly ranked results reflect gene set composition rather than biology and were not interpreted: cancer pathways (KEGG breast/colorectal/"pathways in cancer"), which are rich in *FOS*, *JUN* and *MYC*; NTRK1/NGF-stimulated transcription (Reactome's top hits), whose gene sets are largely immediate early genes; cardiac morphogenesis terms; and poorly characterised GC-rich zinc finger motifs (ZNF253, ZNF138, ZXDL, Kaiso), which are commonly enriched in any promoter-rich gene set. Human Protein Atlas enrichment for "skeletal muscle" is circular given the tissue of origin and is reported only as a sanity check.
6. **Gene list threshold affects results.** The strict list (68 genes) recovered *skeletal muscle cell differentiation* as a highlighted driver term; the inclusive list (248 genes) did not, instead surfacing broader regulatory terms plus the specific amino acid transport and energy homeostasis findings. Both are reported rather than selecting the more favourable one.

## Files

| File | Contents |
|---|---|
| `GSE126296_GEO2R_top_table.tsv` | Full GEO2R output for all 33,297 probes: probe ID, gene symbol, gene title, log2 fold change, unadjusted p, Benjamini–Hochberg adjusted p, moderated t and B statistics. Groups ordered post vs pre, so positive logFC indicates induction. |
| `genes_induced_strong_68.txt` | 68 named genes: adj. p < 0.05 and \|logFC\| > 1. |
| `genes_induced_all_248.txt` | 248 named genes: adj. p < 0.05, any magnitude. |
| `genes_repressed_75.txt` | 75 named genes: adj. p < 0.05, any magnitude. |
| `gprofiler_multiquery_input.txt` | Both lists formatted for g:Profiler multiquery mode. |
| `figure1_volcano.png` | Volcano plot of differential expression, post vs pre. |
| `figure2_enrichment_multiquery_full.png` | Enrichment across annotation sources, induced and repressed, with the numbered driver-term table. |
| `Sprint_transcriptomics_report.docx` | Full scientific report with figures, references and appendices. |

Probes without a gene symbol were excluded from the derived lists, since enrichment tools cannot map them. Raw CEL files are not redistributed here; they are available from GEO under accession GSE126296.

## Reproducing this

1. Open [GSE126296](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE126296) → **Analyze with GEO2R**
2. Define groups `pre` and `post`, assign samples by timepoint, run
3. Download the full table
4. Filter as described in Methods
5. Submit gene lists to [g:Profiler](https://biit.cs.ut.ee/gprofiler/gost), *Homo sapiens*, multiquery enabled

## Next steps

- Paired differential expression in R (limma with participant as a blocking factor), which should be more sensitive than the unpaired GEO2R contrast
- Direct comparison against acute resistance exercise datasets, and cross-checking key transcripts (*MSTN*, *MYOD1*, *TRIM63*, *KLHL40*) in [MetaMEx](https://www.metamex.eu)

## References

- Rundqvist HC, Montelius A, Osterlund T, Norman B, Esbjornsson M, Jansson E. Acute sprint exercise transcriptome in human skeletal muscle. *PLoS ONE* 2019;14(10):e0223024.
- Pillon NJ, Gabriel BM, Dollet L, et al. Transcriptomic profiling of skeletal muscle adaptations to exercise and inactivity. *Nat Commun* 2020;11:470.
- Raudvere U, Kolberg L, Kuzmin I, et al. g:Profiler: a web server for functional enrichment analysis and conversions of gene lists. *Nucleic Acids Res* 2019;47(W1):W191–W198.
