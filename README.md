# Curve Speed Potential Assessment Tool (v2.7.2)

An independent engineering calculation and assessment tool designed for railway civil engineering professionals to compute curve speed potential, evaluate cant/transition constraints, and plan remediation alternatives referencing standard engineering baselines (such as IRPWM and IRSOD).

## User manual and formula book

Open **Help → User Guide** (F1) or [the offline manual](assets/help/user_guide.html).
The source-reviewed manual covers the seven tabs, four remediation scenarios, 17 formula references,
worked examples, reports, saved records, diagnostics and updates. It distinguishes accessible workflows
from supporting dialogs that are not wired into the current UI.
Run `python scripts/build_user_manual.py` after editing the manual source to synchronize both bundled copies.
The action index and completeness tests help detect missing controls and broken help navigation.

---

## Software Architecture & Version Specification

| Component | Version | Description & Authority |
| :--- | :---: | :--- |
| **Application & GUI Suite** | `v2.7.2` | Comprehensive user interface, batch register processing, multi-format reporting, and remediation workshop (`src/application/version.py`). |
| **Protected Calculation Engine** | `v2.1.0` | Calculation engine identifier for historical snapshot compatibility (`src/domain/standards.py`), verified by SHA-256 manifest. |
| **Standards Compliance Baseline** | `IRPWM-2024 (ACS-07 calculation baseline) / IRSOD-2022` | Governing Indian Railways regulatory baselines and physical constant definitions. |

The 2.7.2 planning calculator is a release candidate. The bug register records its outstanding verification work. Historical protected-core manifests describe their respective archived versions.

---

## Project Status, Independence and Limitations

> [!IMPORTANT]
> **Independent Software Identity & Regulatory Disclaimer**
> 
> - **Independent Development:** This software is an independently developed Curve Speed Potential Calculation and Engineering Assessment Tool.
> - **No Official Affiliation:** It is **not** developed, owned, approved, certified, endorsed, or officially issued by Indian Railways, the Ministry of Railways, the Government of India, the Research Designs and Standards Organisation (RDSO), the Commission of Railway Safety (CRS), the Railway Board, or any public authority or statutory body.
> - **Technical Standards as Calculation Baselines:** References within the software, reports, formula cards, or documentation to technical manuals (e.g., Indian Railways Permanent Way Manual [IRPWM], Indian Railways Schedule of Dimensions [IRSOD]) represent mathematical and engineering calculation baselines only.
> - **Calculation Result Only:** All outputs, figures, speed indicators, feasibility assessments, and PDF dossiers produced by this software are engineering calculation results only.
> - **Strict Mandatory Constraint Enforcement:** An overall `PASS` (`CALCULATED`) state is strictly barred whenever any mandatory engineering constraint fails. Specifically, under IRPWM Para 404(3), freight cant-excess at booked goods speed $V_g$ ($C_e = C_a - \frac{13.76 V_g^2}{R}$) must not exceed the configured limit (standard $75.0\text{ mm}$). Any violation immediately triggers `NON_COMPLIANT` status and disqualifies remediation alternatives.
> - **Geometric Distinction — Spiral Shift vs. Track Realignment Slew:** Calculations for transition modifications compute the spiral shift offset at tangent points ($S = \frac{L^2}{24R}$ or $\Delta S = \frac{L_{\text{prop}}^2 - L_{\text{exist}}^2}{24R_{\text{prop}}}$). This local spiral offset must not be conflated with 2D curve body realignment slew, which requires total station traverse surveying, intersection angle ($\Delta$) measurement, and land boundary clearance checks.
> - **Missing Field Survey Data Flagged as Conditional:** In the absence of measured circular arc lengths or tangent clearances, realignment scenarios are flagged with `"UNSURVEYED"` provenance and conditioned on complete field revalidation before execution.
> - **No Operating Sanction:** This software does not grant, constitute, or replace operational speed sanction, engineering approval, or any other authorization required under applicable rules. Formal operational speed authorization remains strictly contingent upon sanctioned operating drawings, field track monitoring (OMS/TRC) validation, Rolling Stock Speed Certificates, and competent authority approval as determined under current statutory rules.

---

## Key Features

- **Authoritative Geometry Calculation Core:** Computes circular curve speed potential ($V_{\text{circ}} = 0.27 \sqrt{R(C_a + C_d)}$) and transition entry/exit constraints ($L / (\alpha \cdot C_a)$, Newton-Raphson cubic solver for $C_d(V)$).
- **Multi-Alternative Remediation Planner:** Evaluates operational revision, cant optimization via tamping, transition extension, and curve realignment options.
- **Precision PDF Dossiers:** High-density vector PDF generation conforming strictly to 2-page, 4-page, and 6-page budgets.
- **Cryptographic Auditability:** Dual SHA-256 canonical hashing of all input parameters and calculation outputs to ensure tamper evidence.
- **Batch Curve Register Ingestion:** Standard 12-column CSV/XLSX parser with backward-compatible 10-column fallback, track line tracking, curve direction, and circular length verification.
- **Multi-Format Export:** Multi-curve batch register XLSX exports, georeferenced/schematic KML exports, and standalone calculation sheets.

---

## Curve Register Ingestion Formats

The application provides a flexible, multi-format divisional curve register parser supporting CSV and Excel (`.xlsx`) files across three standardized formats:

### 1. Recommended 15-Column Template (Sample Export Standard)
Exported directly by the UI via `Download Sample CSV` / `Download Sample Excel` (`generate_sample_csv` / `generate_sample_xlsx`):

| # | Column Header | Type | Required | Description |
| :-: | :--- | :--- | :-: | :--- |
| **1** | `SL` | Integer | Optional | Serial row number. |
| **2** | `Curve Number` | Text | **Yes** | Unique curve identifier (e.g. `C-01`, `CURVE-19`). |
| **3** | `Section` | Text | Optional | Section identifier (defaults to global settings if omitted). |
| **4** | `Line Type` | Text | **Yes** | Track line assignment (`UP`, `DN`, `SL`, `Single`). |
| **5** | `Direction` | Text | Optional | Curve direction (`LH` or `RH`, default: `RH`). |
| **6** | `From Chainage (km)` | Float | **Yes** | Tangent-to-Spiral start chainage (km). |
| **7** | `To Chainage (km)` | Float | **Yes** | Spiral-to-Tangent end chainage (km). |
| **8** | `Radius (m)` | Float | **Yes** | Curve radius ($R > 0$). |
| **9** | `Actual Cant (mm)` | Float | **Yes** | Actual cross-level super-elevation ($C_a \ge 0$). |
| **10** | `Transition L1 (m)` | Float | **Yes** | Entry transition length ($L_1 \ge 0$). |
| **11** | `Transition L2 (m)` | Float | **Yes** | Exit transition length ($L_2 \ge 0$). |
| **12** | `Circular Arc Length (m)` | Float | Optional | Pure circular curve arc length ($L_c \ge 0$). |
| **13** | `Circular Arc Provenance` | Text | Optional | Data source provenance (`MEASURED`, `DERIVED`, `MISSING`). |
| **14** | `Latitude` | Float | Optional | WGS84 latitude ($-90$ to $+90$). |
| **15** | `Longitude` | Float | Optional | WGS84 longitude ($-180$ to $+180$). |

### 2. Standard 12-Column Specification

| # | Column Name | Type / Allowed Values | Required | Engineering Function & Guidance |
| :-: | :--- | :--- | :-: | :--- |
| **1** | `Curve Number` | Text (e.g. `C-01`, `CURVE-19`) | **Yes** | Unique curve identifier across the section. |
| **2** | `Line Type` | `UP`, `DN`, `SL`, or `Single` | **Yes** | Operating track assignment (UP Main, DN Main, Single Line). |
| **3** | `Direction` | `LH` (Left Hand) or `RH` (Right Hand) | Optional | Curve slew and track-center clearance orientation (default: `RH`). |
| **4** | `From Chainage (km)` | Float (e.g. `142.350`) | **Yes** | Curve tangent point (TC) start chainage. |
| **5** | `To Chainage (km)` | Float (e.g. `143.120`) | **Yes** | Curve tangent point (CT) end chainage. |
| **6** | `Radius (m)` | Float (e.g. `875.0`) | **Yes** | Radius of circular curve arc ($R$). |
| **7** | `Actual Cant (mm)` | Float (e.g. `90.0`) | **Yes** | Built actual cross-level super-elevation ($C_a$). |
| **8** | `Transition L1 (m)` | Float (e.g. `65.0`) | **Yes** | Entry transition spiral length ($L_1$). |
| **9** | `Transition L2 (m)` | Float (e.g. `65.0`) | **Yes** | Exit transition spiral length ($L_2$). |
| **10** | `Circular Length (m)` | Float (e.g. `120.0`) | Optional | Surveyed pure circular arc length ($L_c$). Flags advisory if $< 30.0\text{ m}$. |
| **11** | `Latitude` | Float (e.g. `28.6139`) | Optional | WGS84 decimal latitude for georeferenced GIS KML export. |
| **12** | `Longitude` | Float (e.g. `77.2090`) | Optional | WGS84 decimal longitude for georeferenced GIS KML export. |

### 3. Legacy 10-Column Backward Compatibility
Existing 10-column registers (`Curve Number, Line Type, From Chainage, To Chainage, Radius, Actual Cant, Transition L1, Transition L2, Latitude, Longitude`) are automatically detected and parsed seamlessly without user intervention. Missing direction defaults to `"RH"` and missing circular length is tagged with `"UNSURVEYED"` provenance.

---

## User Interface & Workflow Architecture

The application is structured into streamlined functional tabs:

1. **Tab 0: Settings & Standards** — Global divisional parameters, route classification (Group A/B/C/D/E), maximum sanctioned speed (Sectional MPS), booked freight speed ($V_g$), cant limits, and statutory authority preferences.
2. **Tab 1: Single Curve Assessment** — Interactive individual curve calculator with live parameter substitution, constraint evaluation, and instant PDF calculation book export.
3. **Tab 2: Curve Register & Batch Ingestion** — Divisional batch ingestion and management:
   - **User Guidance Discovery Ribbon:** Informs engineers of one-click drilldown: `💡 Tip: Double-click any curve row to inspect its full assessment and remediation in Results View.`
   - **14-Column Enriched Table:** Real-time visibility of Line Type (`UP`/`DN`), Chainage, Radius, Cant, Transitions, Circular Arc (with `⚠️` warning if $< 30\text{ m}$), Sectional MPS, $V_{\text{geom}}$, $V_{\text{ops}}$, and Governing Status.
   - **Row-Level Tooltips:** Hovering any cell provides direct double-click navigation prompts.
   - **Multi-Curve Actions:** Filter, sort, execute bulk assessments, export batch registers to Excel, and generate georeferenced KML track overlays.
4. **Tab 3: Results & Remediation Workshop (Screen D)** — Modernized 2-tab diagnostic workspace:
   - **Sub-Tab 1: Baseline Assessment & Telemetry:** Diagnostic Candidates Speed Hierarchy table, enriched track physical telemetry (theoretical vs measured versine, cant gradients, rates of cant change), and dual cryptographic SHA-256 hashes.
   - **Sub-Tab 2: Remediation Workshop:** Zero-popup target speed evaluation ($V_{\text{target}}$) with side-by-side 4-alternative feasibility matrix (Operational Revision, Cant Optimization, Transition Extension, Realignment).

---

## Installation & Execution

### Prerequisites & Runtime Environment
- **Python**: Version 3.10 to 3.14
- **Dependencies**: `PySide6>=6.8.0`, `openpyxl>=3.1.2`, `pypdf>=3.0.0`, `matplotlib>=3.8.0`, `pytest>=8.0.0`
- Install dependencies via standard pip:
  ```bash
  pip install -r requirements.txt
  ```

### Quick Start
```bash
# Launch GUI application
python main.py

# Run standalone executable (if built)
run_app.bat

# Run comprehensive test suite
python -m unittest discover tests
```

