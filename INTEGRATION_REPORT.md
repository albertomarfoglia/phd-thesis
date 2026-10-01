# Integration report — six papers merged into Chapters 3–5

## 11. Table sizing and running-header clearance (2026-10-01)

- Kept a common table-caption style in `phd-thesis.tex` (small caption text, bold label, 6 pt gap), but removed the global body-font override. Each table now retains its source/local font size so dense tables can stay reduced while shorter tables use the document's normal size.
- In `phd-thesis.sty`, reduced running-title text to `\small` and increased the clearances between the header, text body, and footer. This addresses the reported collisions without removing the chapter/subsection marks or changing table/figure content.
- No paper metadata values were changed. Paper 3 still has no citation line because the supplied source material has no bibliographic record; a record was not inferred or invented.
- Final compilation status for these layout changes: not verified. The local MiKTeX installation reports that its first-run setup must be completed and exits before LaTeX starts; no compilation result is claimed.

This report lists only the technical changes made to integrate the papers. No scientific text, number, result, caption or citation was rewritten. The only text changes are the mechanical ones listed in §5 and §8, each with its reason.

**Final status:** the thesis compiles with pdflatex → bibtex → pdflatex ×3. The result is 267 pages (81 before). There are 0 errors, 0 undefined citations, 0 undefined references and 0 multiply-defined labels.

---

## 1. Files integrated

| Chapter | Paper | Source used | Thesis file |
|---|---|---|---|
| 3 | P1 *Challenges of health data standard adoption and usage: a systematic review* | `papers/1-s2.0-S1532046426000468-main.pdf` (published article, 21 pp.) | `chapters/contributions/paper1.tex`, `paper1_table1.tex` |
| 3 | P2 *Towards real-world clinical data standardization…* | `…FHIR_driven_Transformation_Pipeline/elsarticle-template-num.tex`, `cas-refs.bib` | `chapters/contributions/paper2.tex` |
| 4 | P3 *MEDS-OWL…* | `meds_owl_JBI_2(1)/main.tex`, `supplementary.tex`, `cas-refs.bib` | `chapters/contributions/paper3.tex` (supplement included as the last subsection, "Supplementary Material") |
| 4 | P4 *Representation of ML models…* | `IEEE_Conference_MADTECC…/conference_101719.tex` (inline `thebibliography`) | `chapters/contributions/paper4.tex` |
| 5 | P5 *CONNECTED…* | `Frontiers___CONNECTED…/frontiers.tex`, `connected_v2.bib` | `chapters/contributions/paper5.tex` |
| 5 | P6 *A knowledge graph-driven framework…* | `_FGCS____DIGITA_25…/cas-dc-template.tex`, `cas-refs.bib` | `chapters/contributions/paper6.tex` |

- **New chapter files:** `chapters/chapter3.tex`, `chapter4.tex` and `chapter5.tex`. Each has the prescribed chapter title and one factual sentence that points back to the corresponding Chapter 2 stage section. The two papers follow, each as a `\section` titled with the paper title.
- **Per-paper opening (consistent across papers):** the sentence "This section contains the article \cite{…}", then authors, affiliations, corresponding author, e-mails/ORCID as given in the source, Abstract, Graphical abstract and Highlights (where present in the source), and Keywords. The body follows. The back-matter statements are kept as unnumbered subsections.
- **Main file:** `phd-thesis.tex` has a preamble block (§6) and three extra `\include` lines.
- **Unused sibling files:**
  - P2: the two other `elsarticle-template-*.tex` files are the stock Elsevier templates.
  - P3: `main_count.tex` is a word-count copy of `main.tex` without the abstract and statements.
  - P4: `conference_101719.pdf` is the **unmodified IEEE template**, not the paper.
  - P5: `frontiers_SupplementaryMaterial.tex` and `test.bib` are unmodified Frontiers template placeholders.
- **Not integrated:** class files, `.bst` files, logos, `doc/` and thumbnails.

## 2. Files / figures moved or renamed

Figures were copied into one folder per paper. Several papers use identical file names (for example `fig1.png` in P3, P4 and P6), and separate folders stop them from overwriting each other.

| Folder | Content |
|---|---|
| `figures/paper1/` | 4 figures **extracted losslessly from the PDF** (native JPEG streams, 300 ppi), renamed `fig1-prisma.jpg`, `fig2-overview.jpg`, `fig3-dataset-magnitude.jpg` and `fig4-coverage.jpg` |
| `figures/paper2/` | `images/1-…4-*.png` and `grabs.pdf` (graphical abstract). `images/graphical_abstract.pdf` is byte-identical to `grabs.pdf`. |
| `figures/paper3/` | `figs/fig0–fig6.png` and `graphical_abstract.png` |
| `figures/paper4/` | `Connected.png`, `connected-ontology-and-model.png`, `patient-fhir-kg.png`. The `*.old.png`, `fig1.png` and `step.png` files are not referenced by the source. |
| `figures/paper5/` | `framework1.png`, `framework2.png` |
| `figures/paper6/` | `figs/fig1–fig11` |

All `\includegraphics` paths were updated. Every figure and every table of every paper is present:
- P1: 4 figures, 1 table (+ the uncaptioned significance box)
- P2: 4 figures, 7 tables
- P3: 7 figures (3 main + 4 supplementary), 17 tables (5 main + 12 supplementary)
- P4: 3 figures
- P5: 2 figures
- P6: 11 figure files, 4 tables

**Folder name:** the integrated paper files live in `chapters/contributions/`, not `chapters/papers/`. Your uncommitted `.gitignore` line `papers` matches *every* directory called `papers`, which would have silently excluded them from git.

## 3. Citation keys merged (same publication, one entry kept)

Merged bibliography: `phd-thesis.bib` goes from 216 to **414** entries. 11 thesis-internal duplicates were removed. 209 entries were added: P1 142, P2 20, P3 26, P4 13, P5 8, P6 0 (all of P6's cited works were already in the thesis bib). Only entries **cited** by a paper were imported, because the papers' uncited `.bib` entries were never printed in the papers themselves. The thesis's `\nocite{*}` is unchanged. Each duplicate was checked on DOI, title, authors, venue, year and pages.

**Thesis-internal duplicates.** These already existed before the merge and printed twice because of `\nocite{*}`. The key used by Chapters 1–2 was kept.

| Removed | Kept | Evidence |
|---|---|---|
| `croatti_integration_2020-1` | `croatti_integration_2020` | identical records |
| `chen_ethical_2021-1` | `chen_ethical_2021` | identical records |
| `marfoglia2025towards`, `MARFOGLIA2025109745` | `marfoglia_towards_2025` | same DOI 10.1016/j.compbiomed.2025.109745 |
| `arcobelli_fhir-standardized_2024` | `arcobelli2024fhir` | same title/authors/vol/pages (DOI 10.1038/s41597-024-03593-6) |
| `katsoulakis_digital_2024` | `Katsoulakis2024` | same DOI |
| `ricci_pervasive_2022` | `9325551_ricci` | same DOI |
| `marfoglia_representation_2024` | `marfoglia_2024_mimo` | same DOI |
| `bjornsson_digital_2019` | `Björnsson2019` | same DOI |
| `carbonaro_connected_2023` | `10.3389/fdgth.2023.1322428_carbonaro_connected` | same DOI |
| `rathee_semantic_2024` | `rathee_semantic_2025` | all 8 authors, title, journal, vol. 21, no. 1 identical; **years differ (2024 vs 2025)** — see §10 |

**Paper keys pointed to an existing entry** (the paper's `\cite` was rewritten to the retained key):
- **P2:** `THOMASON20241`→`thomason_data_2024`, `s24165175`→`seixas-lopes_musculoskeletal_2024`, `sinaci_data_2023`→`sinaci2023data`, `namli_2024`→`namli2024scalable`, `williams_standardized_2023`→`williams2023standardized`, `montazeri_developing_2023`→`montazeri2023developing`, `simon_2024`→`simon2024metadata`, `bennett_mimic-iv_2023`→`bennett2023mimic`, `soares_2023`→`soares2023omop`, `ladas_2022`→`ladas2022openehr`, `moscato2024fhir`→`arcobelli2024fhir`, `carbonaro_connected_2023`→`10.3389/…_carbonaro_connected`
- **P3:** `marfoglia_knowledge_2026`→`MARFOGLIA2026108380` (P3 cites P6), `toure_fairification_2023`→`toure2023`, `noy_ontology_2001`→`mcguninnes`, `schlichtkrull_modeling_2018`→`schlichtkrull_2018` (**P3 itself cited this paper under two keys**)
- **P5:** `ying_novel_2019`→`liu_novel_2019` (same DOI; the P5 record had the first author's name inverted), `bjornsson_digital_2019`→`Björnsson2019`, `ricci_pervasive_2022`→`9325551_ricci`
- **P6:** `MARFOGLIA2025109745`→`marfoglia_towards_2025`, `arcobelli_fhir-standardized_2024`→`arcobelli2024fhir`, `katsoulakis_digital_2024`→`Katsoulakis2024`, `ricci_pervasive_2022`→`9325551_ricci`, `carbonaro_connected_2023`→`10.3389/…`, `marfoglia_representation_2024`→`marfoglia_2024_mimo`
- **P4** (`\bibitem` keys): `b1`→`johnson_precision_2021`, `b13a`→`10.3389/…_carbonaro_connected`, `b14`→`wang_mobility_2022`, `b15`→`malakuti_four-layer_2019` (from P5), `b16`→`jinzhi_exploring_2022`, `b17`→`ricci_web_2022`, `b17a`→`martin2017clean`, `b19`→`Amith2022`. The other 11 bibitems became new entries transcribed from the bibitem text.
- **P1** (numbered references): [1]→`thomason_data_2024`, [13]→`gehrmann_what_2023`, [17]→`marfoglia_towards_2025`, [18]→`arcobelli_motu_2023`, [19]→`bennett2023mimic`, [20]→`williams2023standardized`, [23]→`arcobelli2024fhir`, [31]→`vorisek_fast_2022`, [86]→`sinaci2023data`. **P1 lists three works twice:** [101]=[30] (identical), [144]=[88] (identical), and [141]=[95] (same authors, title, journal, volume and year; [141] adds pp. 103–111, kept in the merged entry).

**Kept separate on purpose** (flagged for your judgement):
- `10.1145/2939672.2939778_ribeiro` (KDD'16) vs `ribeiro_why_2016` (arXiv): same work, different publication records (different DOIs).
- `agrawal_artificial_2018` vs `paul_artificial_2021`: same title, different publications.
- P1 [29] (a PubMed web page with no author/year) vs [92] (Bialke et al. 2022): same title, but [29] cannot be verified from the supplied material.

**Chapter 2:** one mechanical edit. `\cite{…marfoglia2025towards}` (two occurrences on one line) became `marfoglia_towards_2025`, because the removed key is a duplicate of that entry. **Chapter 1 is unchanged.**

## 4. Citation-key conflicts

No key was used for two different publications (checked across the thesis and all paper bibs). New keys for P1 and P4 follow the thesis's Zotero-style `author_word_year` scheme and were checked for uniqueness. P1 [133] is `dolin_vcf2fhir_2021_p1`, so it cannot clash with P2's uncited, non-imported `dolin_vcf2fhir_2021`.

## 5. Labels renamed

Every label in P2–P6 was prefixed systematically: `type:name` → `type:paperN_name`, and `name` → `paperN_name`. All matching `\ref` calls were updated. This avoids real collisions such as `sec:methods` (P2, P3), `sec:results`, `sec:discussion` (P2, P3, P6), `sec:related_work` (P3, P6) and `fig1`–`fig3` (P4, P6). Per paper:

| Paper | Labels | Refs |
|---|---|---|
| P2 | 15 | 20 |
| P3 | 30 + 22 supplementary | 97 |
| P4 | 3 | 3 |
| P5 | 3 | 5 |
| P6 | 24 | 25 |

P1 labels were created as `sec:paper1_*`, `fig:paper1_*` and `tab:paper1_summary`. Each paper section is labelled `sec:paperN`.

**Text-level cross-reference fixes:**
- P4's hard-coded "Section II/III/IV/V" became `Section~\ref{…}`. Labels were added to its five sections because the IEEE numbering no longer exists.
- P1's "Fig. 1–4" and "Table 1" became `\ref`s. The Zenodo file names "Table 1_extended" and "Table 1_summary" were left untouched.

## 6. Packages / preamble

Added in `phd-thesis.tex`, with a comment on each line:
- `amssymb`, `array`, `multirow`, `booktabs`, `subcaption` (required by the paper bodies)
- `longtable`, `pdflscape` (P1 Table 1)
- `placeins` (`\FloatBarrier`)
- P6's `L`/`C` column types and `\tblwidth`, copied from Elsevier `cas-common.sty`
- `\setcounter{secnumdepth}{3}`, so that a paper's internal "Section \ref{…}" resolves to a numbered unit. This does not affect Chapters 1–2, which have no sub-subsections.

Not added: `natbib`, because `\citep` (P3's only natbib command) was mechanically changed to `\cite`. Also not added: `xr-hyper` (the supplement is now internal), `cite`, `algorithmic` (unused), `tabularx` (only in commented code), and the journal classes. The document class is unchanged.

**Removed from the paper sources:**
- preambles and `\begin{document}`/`\end{document}`
- `\maketitle`, `\linenumbers`, `\onehalfspacing`
- the per-paper `\bibliography`/`\bibliographystyle`
- the supplement's title page and ToC, its S-numbering and three `\clearpage`
- the IEEE/cas front-matter macros (their content was transcribed into the metadata block)

## 7. Paper 1: PDF-to-LaTeX conversion

**No Word document was supplied.** Paper 1 exists only as the published PDF, so the conversion used that PDF's text layer. The method was chosen to avoid retyping and interpretation:

- **Body text:** each paragraph was taken verbatim from `pdftotext`. Paragraph boundaries come from the default mode; hyphenation (soft vs. hard hyphens) comes from the `-raw` mode. Numeric citations and ranges were converted to `\cite{…}` through the reference map, and all 154 references are cited. Special characters were converted to LaTeX.
- **Verification:** all 331 body sentences of the original were checked against the compiled thesis and the LaTeX source. None is missing.
- **Table 1 (99 rows):** the published table is typeset with columns that do not visually line up with their rows. The PDF's content stream, however, is row-ordered, so rows were rebuilt from it deterministically, using the closed vocabularies of the Standard, Scale, Category, Type, Area and Use columns. Where a cell's text continues across a page break (after "Table 1 (continued)"), that continuation was put back into the cell it continues. This happened in 5 places:
  - the rows of Chechulina, Sinaci, Li 2022 and Sathappan (2 cells)
  - one hyphenated word split across the page break before Lamer et al.
- **Figures:** 4 raster images at their original resolution, with the original captions.
- **References:** transcribed to BibTeX from the printed list. "et al." is encoded as `and others`. Titles are brace-protected so the thesis `alpha` style keeps the published capitalisation.

**Source inconsistencies reproduced as published (not corrected):**
- **Table 1:**
  - The two "Kim et al., 2021" rows carry each other's Objective, Scale and Category (the polysomnography row has the osteoporosis objective, and vice versa).
  - The "Lenert et al., 2021" row repeats Lamer et al.'s title.
  - The "Li et al., 2021" row carries Lenert et al.'s title.
  - In stream order, the Baumgartner row's Objective also contains "Harmonize heterogeneous data into the OMOP-CDM…", which the PDF renders beside the Bhattacharjee row.
- **Text:**
  - Stray dashes: "demonstrating– how", "“OMOP–onFHIR”", "for –real-time", "tractio–n", "OMOP–CDM".
  - "Structure Maps17,23" is printed as plain digits; these are possibly citations [17,23], but that cannot be determined.
  - The clinical-medicine citation list "[24,32,38,41–43,…]" is kept as printed.
  - The PDF's "Declaration of competing interest" text is split across the page by the Acknowledgements; it was rejoined.
- **Reference [59]** has no journal (BibTeX warns "empty journal").
- **Not reproducible:** the online Supplementary Material (search query "Text 1") and the Zenodo extended table [44] were not supplied. The references to them are kept as text.

## 8. Content not integrated faithfully / items needing your decision

- **P3 has no bibliographic record** in any supplied file, so its section has no "contains the article \cite{…}" line. Chapter 2 does not cite it either.
- **P4 does not match Chapter 2's description.** Chapter 2 says P4 introduces "MIMO … developed in Protégé … OWL Description Logic reasoner". The supplied P4 source mentions only "Manifest" and contains none of these. That material appears in **P6**. The paper was integrated as supplied, and Chapter 2 was not changed.
- **P2 venue:** the source says `\journal{Journal of Biomedical Informatics}` (a template leftover), but the thesis bib record is *Computers in Biology and Medicine* 187 (2025). The venue is shown only through the citation.
- **Statements not printed:** P6 has `\credit{}` data, but its `\printcredits` is commented out, so no CRediT statement is printed (as in the source). P3's highlights are commented out in its source and are not included. P3's `\printcredits` was rendered as a CRediT subsection built from its `\credit{}` values.
- **Retained records:** where the retained thesis entry is less complete than the paper's own, the thesis record was kept (per the instruction to preserve thesis keys). Examples: `ladas2022openehr` (no venue or pages; BibTeX warns), and `arcobelli2024fhir` (no DOI, though the thesis style does not print DOIs).
- **Comments:** commented-out text in the sources, such as old versions and "CHANGED" notes, is kept as LaTeX comments. It is never typeset.

## 9. Final compilation status

- **Build:** pdflatex → bibtex → pdflatex ×3. Compiled in an isolated copy of the project; the `papers/` folder is not needed. 267 pages.
- **Clean:** 0 LaTeX errors, 0 undefined citations or references, 0 multiply-defined labels, no missing files.
- **Floats:** all 62 figure/table labels are typeset inside their own paper. `\FloatBarrier` sits at the end of each paper and before P3's supplement.
- **Layout-only adjustments** (no text or data changed):
  - narrower `p{}` widths for P3 tables sized for the two-column journal page
  - `\resizebox` on two wide P6 tables (the papers already use it elsewhere)
  - Table 1 as a landscape `longtable` with `\newgeometry{margin=2cm}` on its pages
  - ragged-right metadata blocks
  - `\emergencystretch` from Chapter 3 onward, so Chapters 1–2 are typeset exactly as before
- **Overfull boxes:** about 316 after the first merge build, now 11 in the merged content (9 hbox, 2 vbox), all under 25 pt except the ones noted below.

## 10. Remaining warnings needing manual inspection

- **BibTeX (6 warnings):**
  - sort key missing: `qeuropean` (P2 bib), `noauthor_21st_2020` (P2 bib), `noauthor_darpas_nodate` (thesis, pre-existing)
  - `de_analyzing_2021`: empty journal (as printed in P1)
  - `ladas2022openehr`: empty publisher (thesis, pre-existing)
  - `sham_empowering_nodate`: empty year (thesis, pre-existing)
- **Overfull boxes:**
  - The bibliography's P4 VentureBeat URL (81 pt).
  - P2 Kahn-framework table (vbox, 43 pt). Its `\multirow{3}{=}{…}` text is taller than its rows by the source's own design.
  - P3 inline `\texttt{…}` identifiers (up to 43 pt).
  - `front.tex` and `chapter2.tex:225` (50 pt) were already overfull before the merge.
- **Year conflict:** `rathee_semantic_2025` is the merged record; the removed duplicate said 2024. Please confirm the year.
- **Near-empty page:** there is a mostly empty page before P1 Table 1, caused by the unavoidable page break into landscape.
- **Editor build files:** `phd-thesis.pdf`, `.fdb_latexmk` and `.synctex.gz` in the project root come from an editor-triggered latexmk build (19:22), not from this integration.
