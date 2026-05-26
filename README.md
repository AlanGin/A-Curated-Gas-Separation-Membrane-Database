# Membrane Data Infrastructure

A mechanism-aware data infrastructure project for membrane separation science. This repository is designed to support curated, versioned, and reproducible membrane datasets that connect material structure, preparation history, testing conditions, transport performance, and practical operating boundaries.

The central goal is not to build another performance ranking table. The goal is to convert heterogeneous membrane literature data into a reusable research infrastructure that can reveal testing bias, hidden trade-offs, mixed-gas penalties, humidity and aging penalties, failure modes, and realistic operating boundaries.

## Scientific Thesis

Membrane databases should not merely collect permeability, permeance, selectivity, flux, or rejection values. They should preserve the experimental and mechanistic context required to interpret those values.

This project is built around four principles:

1. **Mechanism-aware data**: Transport data should be connected to material family, pore structure, pore-wall chemistry, defect structure, morphology, and separation mechanism.
2. **Condition-aware comparison**: Performance values are only meaningful when testing temperature, pressure, feed composition, humidity, membrane thickness, membrane area, stability time, and measurement mode are preserved.
3. **Failure-aware evaluation**: Aging, plasticization, swelling, fouling, wetting, compaction, degradation, and cleaning recovery should be treated as core data fields, not secondary notes.
4. **Reproducible data-to-insight workflow**: Every figure, boundary analysis, quality score, and model output should be reproducible from versioned curated data.

## Intended Research Outputs

This repository is intended to support several research outputs:

- A versioned gas separation membrane database with DOI/CSTR-ready release files
- A data dictionary and minimum information standard for membrane separation data
- A reproducible cleaning and quality-rating pipeline
- Reported upper-bound and practical operating-boundary analyses
- Perspective, viewpoint, or roadmap manuscripts on FAIR membrane data infrastructure
- Future extensions to complex aqueous separations, high-salinity organic wastewater, nanofiltration, pervaporation, and membrane reactor datasets

## Repository Structure

```text
membrane-data-infrastructure/
├── AGENTS.md                         # Instructions for Codex and other coding agents
├── README.md                         # Project overview
├── pyproject.toml                    # Python project configuration
├── requirements.txt                  # Python dependencies
├── data/
│   ├── raw_pdfs/                     # Source PDFs, not committed if copyright-restricted
│   ├── extracted/                    # Machine-extracted candidate data
│   ├── curated/                      # Human-validated curated database files
│   ├── releases/                     # Versioned release datasets
│   └── reports/                      # Cleaning, validation, and quality reports
├── schema/
│   ├── gas_separation_schema.yaml    # Gas separation data schema
│   ├── aqueous_separation_schema.yaml# Future aqueous separation schema
│   └── data_dictionary.md            # Human-readable field definitions
├── src/
│   ├── extract_pdf.py                # PDF text and table extraction
│   ├── normalize.py                  # Unit conversion and field normalization
│   ├── validate_schema.py            # Schema validation
│   ├── quality_score.py              # Data completeness and reliability scoring
│   ├── boundary_analysis.py          # Upper-bound and operating-boundary analysis
│   └── utils.py                      # Shared utilities
├── notebooks/
│   ├── 01_reported_upper_bound.ipynb # Reported performance boundary analysis
│   ├── 02_operating_boundary.ipynb   # Practical operating boundary analysis
│   ├── 03_quality_landscape.ipynb    # Data quality and testing-condition bias
│   └── 04_mechanism_map.ipynb        # Mechanism-aware performance mapping
├── tests/
│   ├── test_schema.py
│   ├── test_normalization.py
│   ├── test_quality_score.py
│   └── test_boundary_analysis.py
└── docs/
    ├── curation_protocol.md          # Human curation rules
    ├── extraction_protocol.md        # PDF extraction rules
    ├── release_protocol.md           # Versioning and release rules
    └── perspective_outline.md        # Manuscript outline
```

## Data Workflow

The workflow follows a strict separation between machine extraction and human-curated data.

```text
PDF literature
    ↓
Raw PDF archive
    ↓
Text, table, and figure candidate extraction
    ↓
Structured candidate records with provenance
    ↓
Unit normalization and schema validation
    ↓
Quality scoring and anomaly detection
    ↓
Human curation and validation
    ↓
Versioned curated dataset
    ↓
Reproducible figures, models, and boundary analyses
```

Machine-extracted data must never be treated as final curated data. All extracted values must preserve their source location, extraction method, confidence level, and validation status.

## Provenance Requirements

Every extracted or curated record should preserve the following provenance fields whenever possible:

- Source DOI
- Source title
- Source authors
- Source journal
- Publication year
- PDF filename
- Page number
- Table number, figure number, or text location
- Raw extracted string
- Normalized value
- Unit before normalization
- Unit after normalization
- Extraction method
- Extraction confidence
- Human validation status
- Curator name or initials
- Curation date
- Notes on ambiguity or assumptions

## Core Gas Separation Fields

The initial gas separation schema should include, at minimum:

### Material and Membrane Identity

- Material name
- Material family
- Polymer, MOF, COF, 2D material, silica, zeolite, carbon, mixed-matrix membrane, or other class
- Membrane morphology
- Selective layer thickness
- Support material
- Preparation method
- Post-treatment or activation condition

### Testing Conditions

- Pure-gas or mixed-gas measurement
- Gas pair or gas mixture
- Feed composition
- Temperature
- Pressure difference
- Upstream pressure
- Downstream pressure
- Sweep gas condition
- Humidity or water activity
- Testing duration
- Effective membrane area
- Measurement method

### Performance Metrics

- Permeability
- Permeance
- Selectivity
- Separation factor
- Flux
- Stage cut, if applicable
- Mixed-gas penalty
- Humidity penalty
- Aging penalty
- Plasticization pressure
- Stability metric

### Mechanistic and Reliability Fields

- Proposed transport mechanism
- Molecular sieving indicator
- Sorption-controlled transport indicator
- Diffusion-controlled transport indicator
- Competitive adsorption flag
- Defect sensitivity flag
- Swelling or plasticization flag
- Aging or physical relaxation flag
- Quality score
- Comparability class

## Quality Rating Philosophy

The quality score should not reward high performance by itself. It should reward interpretability, reproducibility, and practical relevance.

A high-quality record should include:

- Complete testing conditions
- Clear distinction between pure-gas and mixed-gas data
- Defined temperature and pressure
- Defined feed composition
- Reported membrane thickness or effective area where relevant
- Stability or repeatability information
- Explicit source provenance
- Clear units
- No unresolved ambiguity in extraction or normalization

A low-quality record may still be retained, but it should be clearly flagged and should not dominate boundary analysis or model training.

## Boundary Analysis Concept

This repository is designed to support a shift from reported performance boundaries to practical operating boundaries.

A reported upper bound captures the best values reported under ideal or heterogeneous testing conditions. A practical operating boundary should consider penalties arising from mixed-gas operation, humidity, aging, plasticization, long-term testing, fouling, and other real operating constraints.

The intended analytical progression is:

1. Reproduce conventional reported performance plots.
2. Annotate records by testing completeness and quality score.
3. Compare pure-gas and mixed-gas performance.
4. Quantify operating penalties where data allow.
5. Identify material families that retain performance under realistic conditions.
6. Define practical operating boundaries rather than only reported upper bounds.

## Codex Usage Pattern

Codex or other coding agents should be used for engineering tasks, not for final scientific judgment.

Appropriate tasks for Codex include:

- Creating repository structure
- Designing schema files
- Writing extraction scripts
- Writing cleaning and normalization pipelines
- Implementing unit conversion
- Creating validation tests
- Generating reproducible notebooks
- Building dashboards or simple APIs
- Drafting documentation
- Creating pull requests with clear change summaries

Tasks that require human scientific judgment include:

- Deciding which fields are scientifically necessary
- Determining whether a reported value is comparable
- Judging whether an outlier is a true breakthrough or a testing artifact
- Interpreting transport mechanisms
- Defining operating boundaries
- Writing final scientific claims
- Approving curated records

## Minimal Starting Plan

The recommended first milestone is deliberately small.

1. Select 5 to 10 well-known membrane papers as a gold-standard benchmark.
2. Manually curate their key data into `data/curated/gold_standard.csv`.
3. Build the schema and validation pipeline around this gold standard.
4. Run machine extraction on the same PDFs.
5. Compare machine extraction against the gold standard.
6. Improve extraction and normalization rules.
7. Generate the first reported upper-bound and quality-landscape figures.
8. Expand to 50 papers only after the benchmark workflow is reliable.

## Suggested Commands

Install dependencies:

```bash
pip install -r requirements.txt
```

Run tests:

```bash
pytest
```

Validate curated data:

```bash
python src/validate_schema.py --input data/curated/gold_standard.csv --schema schema/gas_separation_schema.yaml
```

Extract candidate data from PDFs:

```bash
python src/extract_pdf.py --input data/raw_pdfs --output data/extracted
```

Normalize extracted records:

```bash
python src/normalize.py --input data/extracted --output data/reports/normalization_report.csv
```

Generate quality scores:

```bash
python src/quality_score.py --input data/curated/gold_standard.csv --output data/reports/quality_scores.csv
```

## Release Philosophy

Each public release should include:

- Version number
- Release date
- Curated dataset file
- Data dictionary
- Schema file
- Changelog
- Known limitations
- Citation information
- Reproducibility notebooks
- Validation report

A release should not be made unless the curated data can reproduce the key figures and the validation report is available.

## Citation

Citation information should be added after the first formal dataset release. If the dataset is deposited in ScienceDB or another repository with DOI/CSTR registration, the persistent identifiers should be listed here.

## License

The code license and data license should be specified separately. Literature-derived curated data may require careful licensing and citation practice. Raw PDFs should not be redistributed unless redistribution rights are clear.

## Status

This repository is under active development. The current priority is to establish a reliable schema, extraction workflow, curation protocol, and reproducible figure pipeline before expanding the dataset scale.
