# Multiple spillovers of H5N1 clade 2.3.4.4b into US dairy cattle

Code and analysis files accompanying *The emergence and molecular evolution of H5N1 influenza viruses in United States dairy cattle*.

BEAST XML configuration files are provided for all primary Bayesian phylogenetic analyses and sensitivity analyses described in the manuscript.

## Repository structure

### `code/`

Jupyter notebooks for generating figures and tables from BEAST output files and HyPhy results.

| Notebook | Produces |
|----------|----------|
| `fig1.ipynb` | Figure 1: epidemiological curves (genome counts by host, outbreak counts by state) |
| `figs2-3.tmrca_phylogeny.ipynb` | Figures 2–3: B3.13 and D1.1 time-calibrated phylogenies, tMRCA/tPMRCA extraction from posterior tree distributions, segment-level tMRCA comparisons, skygrid reconstructions |
| `fig4.b313.rate_dnds.ipynb` | Figure 4: B3.13 evolutionary rates and dN/dS from BEAST log files |
| `fig5.d11.rate_dnds.ipynb` | Figure 5: D1.1 evolutionary rates and dN/dS extracted from posterior tree distributions via robust counting |
| `fig6.relax.results.ipynb` | Figure 6: RELAX results for B3.13 and D1.1, including K parameter estimates and omega distributions |

### `trees/`

Maximum likelihood trees (MAPLE) and Bayesian maximum clade credibility trees (BEAST) for B3.13 and D1.1.

- `*.maple_tree.mpRooted.edit.tree` — ML trees for individual B3.13 segments
- `*.PA-HA-NA-MP.mpRooted.edit.tree` — ML tree for the B3.13 concatenated A1 alignment
- `*.wholeGenome.maple_tree.rooted.tree` — ML tree for the B3.13 whole-genome alignment
- `*.avian_cattle.hipstr.tree` — BEAST HIPSTR tree for B3.13 (combined avian + cattle)
- `d11.subset1098.maple_tree.mpRooted.tree` — ML tree for D1.1
- `d11.fixedLocalClock.hipstr.tree` – BEAST HIPSTR tree for D1.1 when using a fixed local clock for D1.1 in dairy cattle
- `d11.ucld.hipstr.tree` — BEAST HIPSTR tree for D1.1 when using a shared evolutionary rate for D1.1 in wild birds and dairy cattle

### `XMLs/`

BEAST XML configuration files for all Bayesian phylogenetic analyses.

**`b3.13_combined_avian_cattle/`** — Joint analyses of avian background and dairy cattle outbreak datasets with a shared tree and joint population model (constant size for avian, exponential for cattle). 

- `{segment}.avian_outbreak.jointCE.transitionBranch.cleaned.xml`

**`b3.13_separate_avian_cattle_robustCounting/`** — Separate analyses of avian and cattle datasets with robust counting (RC) for inferring host-specific dN/dS and evolutionary rates.

- `{segment}.bird_skunk.relaxed.RC.cleaned.xml` — avian background (uncorrelated relaxed clock, robust counting)
- `{segment}.cattle_human.relaxed.RC.cleaned.xml` — dairy cattle outbreak (uncorrelated relaxed clock, robust counting)
- `PA-HA-NA-MP.unlinkedSubClock.{host}.cleaned.xml` — concatenated A1 alignment with segment-specific clock rates

**`d1.1/`** — D1.1 analyses including primary and sensitivity analyses.

| D1.1 XML | Description |
|-----|-------------|
| `*.flClockConstrainedNoStem.noRC.cleaned.xml` | Primary phylogenetic analysis. Host-partitioned, with a fixed local clock for D1.1 in dairy cattle, no robust counting |
| `*.flClockConstrainedNoStem.RC.empirical.cleaned.xml` | Primary robust counting analysis. Host-partitioned, with a fixed local clock for D1.1 in dairy cattle, robust counting on empirical tree distribution|
| `*.flClockConstrainedNoStem.noRC.widerCattleRatePrior.cleaned.xml` | Host-partitioned with a fixed local clock for D1.1 in dairy cattle, with a wider prior on the cattle rate |
| `*.UCLD.noRC.cleaned.xml` | Shared clock, no robust counting |
| `*.UCLD.RC.empirical.cleaned.xml` | Shared clock, with robust counting on empirical tree distribution |
| `*.UCLD.noRC.moreTipUncertainty.cleaned.xml` | Shared clock with wider tip-date priors (± 21 days) |


## Additional analyses

- **RELAX and FUBAR** analyses were performed using HyPhy v2.5.1. Output JSON files are parsed and visualized in `fig6.relax.results.ipynb`.
- **GARD and PHI** reassortment tests were performed using HyPhy (GARD) and PhiPack (PHI). See Methods for parameterization.
- **Phenotypic marker identification** was performed using FluMutGUI v3.2.0.
- **Protein structure visualization** was performed using PyMOL v3.1.0 on PDB structures 9DWE (HA), 3NSS (NA), and 8R1J (polymerase complex).

Raw sequence data were obtained from GISAID and NCBI (see Methods for accession details). 