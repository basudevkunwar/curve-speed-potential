# Curve Speed Potential Assessment Tool

![Version](https://img.shields.io/badge/Version-2.7.2-blue)
![Language](https://img.shields.io/badge/Language-Python-blue)
![Framework](https://img.shields.io/badge/Framework-PySide6-green)
![Gauge](https://img.shields.io/badge/Track-Broad%20Gauge-orange)
![Status](https://img.shields.io/badge/Software-Unofficial-yellow)
![Repository](https://img.shields.io/badge/Repository-Private-red)

**Independently Developed | Unofficial Engineering Software**

## Overview

**Curve Speed Potential Assessment Tool (IR-CSP)** is an independently developed railway engineering desktop application designed for the assessment of existing curve speed potential and target speed enhancement feasibility on Indian Railways Broad Gauge (BG) tracks.

The software provides a structured calculation environment for analysing railway curve geometry, determining permissible speed under configured engineering limits, comparing alternative improvement scenarios and generating detailed technical reports.

This application is an independent engineering calculation utility and is not an official product of Indian Railways.

## Key Features

### 1. Curve Speed Potential Assessment

- Existing curve speed potential calculation
- Maximum permissible speed assessment
- Geometric speed potential calculation
- Identification of governing speed constraints
- Comparison with existing sectional maximum permissible speed (MPS)
- Target speed feasibility assessment

### 2. Curve Geometry & Engineering Calculations

- Curve radius and degree of curve
- Actual cant (Ca)
- Equilibrium cant
- Cant deficiency (Cd)
- Cant excess (Ce)
- Entry and exit transition lengths (L1 & L2)
- Circular curve length
- Cant gradient
- Rate of change of cant
- Rate of change of cant deficiency
- Minimum transition length requirements
- Theoretical transition shift calculations

### 3. Target Speed Enhancement Analysis

The software evaluates alternative geometric configurations to assess the mathematical feasibility of achieving a specified target speed.

| Scenario | Improvement Strategy |
|---|---|
| Scenario 1 | Cant modification |
| Scenario 2 | Transition length modification |
| Scenario 3 | Combined cant and transition modification |
| Scenario 4 | Curve radius modification and realignment assessment |

Each scenario provides calculated speed potential, proposed geometric parameters, applicable numerical constraints and comparative assessment.

### 4. Excel Integration

- Excel-based curve data import
- Curve register management
- Multiple curve data handling
- Export of calculation results
- Structured engineering data reporting

### 5. Calculation PDF

Detailed calculation reports presenting:

- Existing curve particulars
- Input parameters
- Engineering formulae and calculations
- Applicable numerical limits
- Governing speed constraints
- Calculated permissible speed
- Assessment results

### 6. Remediation Dossier

Detailed target speed enhancement reports presenting:

- Existing curve geometry and speed potential
- Target speed requirements
- Existing geometric limitations
- Scenario-wise improvement calculations
- Proposed cant and transition modifications
- Curve radius alternatives
- Comparative speed potential assessment
- Calculated improvement feasibility and suggested alternatives

## Calculation Framework

The application is intended to support railway curve assessment with reference to applicable provisions and configured engineering parameters derived from the Indian Railways Permanent Way Manual (IRPWM).

The calculation framework considers:

- Curve radius
- Actual cant
- Permissible cant deficiency
- Permissible cant excess
- Transition length
- Cant gradient
- Rate of change of cant and cant deficiency
- Sectional speed restrictions
- Applicable rolling stock and route parameters

## Application Workflow

1. Enter or import existing curve data.
2. Configure applicable calculation parameters.
3. Calculate existing curve speed potential.
4. Specify the desired target speed.
5. Evaluate alternative improvement scenarios.
6. Compare calculated speed potential and geometric requirements.
7. Generate Calculation PDF and Remediation Dossier.
8. Export and maintain engineering records.

## Technology Stack

| Component | Technology |
|---|---|
| Programming Language | Python |
| Graphical User Interface | PySide6 / Qt |
| Application Type | Desktop Application |
| Data Integration | Microsoft Excel |
| Technical Reporting | PDF |
| Track Gauge | Broad Gauge (1676 mm) |
| Version Control | Git / GitHub |

## Intended Users

- Railway Civil Engineering Professionals
- Permanent Way Engineers
- Track Engineering Personnel
- Railway Speed Enhancement Planning Teams
- Railway Infrastructure Engineering Professionals

## Version Information

| Particular | Details |
|---|---|
| Software | Curve Speed Potential Assessment Tool |
| Short Name | IR-CSP |
| Current Version | 2.7.2 |
| Development | Independent |
| Official Status | Unofficial |
| Application Type | Engineering Calculation Utility |

Software updates, bug fixes and feature enhancements are maintained through repository version control and release management.

## Development & Repository

This repository is privately maintained for independent software development, source code management, testing, documentation and version control.

**Developer:** Basudev Kunwar

**Repository:** curve-speed-potential

Unauthorized access, reproduction, distribution or modification of proprietary project source code is not permitted. Third-party components remain subject to their respective licences.

## Engineering Disclaimer

**IR-CSP is an independently developed, unofficial engineering calculation and assessment tool.**

This software is not an official product of Indian Railways, the Ministry of Railways, (RDSO), and is not affiliated with or endorsed by these organizations.

References to Indian Railways manuals, standards, formulae and engineering provisions are solely for technical calculation and assessment purposes.

The software is intended to assist engineering calculations, comparative analysis and preliminary speed enhancement assessments.

Calculated speed potential and scenario-wise feasibility results do not constitute official engineering approval, track design approval, speed sanction or authorization for train operation.

All calculation results must be independently verified against applicable railway manuals, standards, amendments, instructions and actual field conditions before engineering implementation.
