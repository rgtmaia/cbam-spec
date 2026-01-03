---
layout: docs
title: "CBAM Producer Data Package Structure"
page_title: "XML Structure"
breadcrumb: "Structure"
description: "Detailed documentation of the XML structure of the CBAM Producer Data Package, including hierarchy, data types, and enumerations."
prev_page:
  url: /docs/concept
  title: "Concept"
next_page:
  url: /docs/lifecycle
  title: "Lifecycle"
---

## Hierarchical Overview

```
CBAMProducerDataPackage (root)
│
├── @version                    # Package version (e.g., "2.0")
├── @schemaVersion              # Schema version (e.g., "2.0.0")
│
├── DatasetIdentification       # Unique dataset identifier
│   ├── DatasetId               # Unique UUID
│   ├── Version                 # Dataset version (increments with each revision)
│   ├── GenerationDate          # Generation date
│   └── DatasetStatus           # draft | final
│
├── ReportingPeriod [REGULATORY]
│   ├── Year                    # Year (e.g., 2026)
│   ├── Quarter                 # Quarter (1-4)
│   ├── PeriodId                # Human-readable identifier (e.g., "2026-Q1")
│   └── SubmissionDeadline      # Submission deadline (optional)
│
├── Operator [REGULATORY]
│   ├── OperatorId              # Unique identifier (e.g., tax ID)
│   ├── OperatorName            # Trade name
│   ├── LegalName               # Legal name [NON-REGULATORY]
│   ├── Address
│   │   ├── Country             # ISO 3166-1 alpha-2 [REGULATORY]
│   │   ├── SubDivision         # State/Province [NON-REGULATORY]
│   │   ├── City                # City [NON-REGULATORY]
│   │   └── Street              # Address [NON-REGULATORY]
│   └── ContactDetails          # [NON-REGULATORY]
│
├── Installations               # List of installations
│   └── Installation[]
│       ├── @index              # Index (1-based)
│       ├── InstallationId      # Unique installation ID [REGULATORY]
│       ├── InstallationName    # Installation name [REGULATORY]
│       ├── Address             # (same structure as operator)
│       ├── ProductionProcess   # [REGULATORY]
│       │   ├── RouteCode       # Production route (BF-BOF, EAF, etc.)
│       │   ├── MethodologyCode # Methodology (TOM01, TOM02)
│       │   └── RegulatoryBasis # Regulatory reference [NON-REGULATORY]
│       └── Products
│           └── Product[]
│               ├── @index
│               ├── ProductId
│               ├── Description       # [NON-REGULATORY]
│               ├── Category          # [NON-REGULATORY]
│               ├── CommodityCode     # [INFORMATIVE]
│               ├── Production        # [REGULATORY]
│               └── EmbeddedEmissions # [REGULATORY]
│
├── ConsolidatedSummary         # [NON-REGULATORY] (optional)
│
└── PackageMetadata             # [NON-REGULATORY] (optional)
```

---

## Main Sections

### 1. DatasetIdentification

Uniquely identifies the data package.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Field</th><th>Type</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>DatasetId</code></td><td>UUID</td><td>Globally unique identifier</td></tr>
    <tr><td><code>Version</code></td><td>String</td><td>Dataset version (e.g., "1.0", "1.1")</td></tr>
    <tr><td><code>GenerationDate</code></td><td>Date</td><td>Generation date (YYYY-MM-DD)</td></tr>
    <tr><td><code>DatasetStatus</code></td><td>Enum</td><td><code>draft</code> or <code>final</code></td></tr>
  </tbody>
</table>
</div>

### 2. ReportingPeriod

Defines the reference quarter for the data.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Field</th><th>Type</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>Year</code></td><td>gYear</td><td>Reference year</td></tr>
    <tr><td><code>Quarter</code></td><td>1-4</td><td>Quarter (Q1, Q2, Q3, Q4)</td></tr>
    <tr><td><code>PeriodId</code></td><td>String</td><td>Human-readable identifier (e.g., "2026-Q1")</td></tr>
    <tr><td><code>SubmissionDeadline</code></td><td>Date</td><td>CBAM submission deadline</td></tr>
  </tbody>
</table>
</div>

### 3. Operator

Information about the producing company.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Field</th><th>Classification</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>OperatorId</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Tax ID (e.g., VAT number)</td></tr>
    <tr><td><code>OperatorName</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Trade name</td></tr>
    <tr><td><code>LegalName</code></td><td><span class="badge badge-yellow">NON-REGULATORY</span></td><td>Registered legal name</td></tr>
    <tr><td><code>Address.Country</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Country (ISO 3166-1)</td></tr>
  </tbody>
</table>
</div>

### 4. Installation

Data for each production facility.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Field</th><th>Classification</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>InstallationId</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Unique installation identifier</td></tr>
    <tr><td><code>InstallationName</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Installation name</td></tr>
    <tr><td><code>ProductionProcess</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Production route and methodology</td></tr>
  </tbody>
</table>
</div>

### 5. Product

Data for each manufactured product.

```
Product
├── ProductId           # Unique product identifier
├── Description         # Text description
├── Category            # CBAM category (steel, aluminium, etc.)
├── CommodityCode       # CN/HS codes [INFORMATIVE]
│   ├── CnCode          # 8 digits
│   └── HsCode          # 6 digits
├── Production          # Production data
│   ├── QuantityType    # TOTAL_PRODUCTION | EU_EXPORT | REPORTED_BATCH
│   ├── Quantity        # Produced quantity
│   └── MeasurementUnit # t | kg | MWh
└── EmbeddedEmissions   # Embedded emissions
    ├── DirectEmissions
    ├── IndirectEmissions
    ├── PrecursorEmissions (optional)
    └── TotalSpecificEmissions
```

### 6. EmbeddedEmissions

Structure of each emission type:

```
DirectEmissions / IndirectEmissions
├── DeterminationType    # 01 (actual) | 02 (default)
├── MethodologyCode      # TOM01 | TOM02 (optional)
├── DeterminationDetails # Text details (optional)
├── Justification        # Justification for default values (optional)
├── ElectricityFactor    # For IndirectEmissions only
│   ├── SourceCode       # SOE01 | SOE02 | SOE03
│   ├── Value            # Factor value
│   └── Unit             # Unit (tCO2e/MWh)
└── SpecificEmissions
    ├── Value            # Numeric value
    └── Unit             # tCO2e/t or tCO2e/MWh
```

---

## Data Types

### Enumerations

#### DeterminationType

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Code</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>01</code></td><td>Actual data (measured/calculated)</td></tr>
    <tr><td><code>02</code></td><td>Default values (transitional period)</td></tr>
  </tbody>
</table>
</div>

#### RouteCode

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Code</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>BF-BOF</code></td><td>Blast Furnace – Basic Oxygen Furnace</td></tr>
    <tr><td><code>EAF</code></td><td>Electric Arc Furnace</td></tr>
    <tr><td><code>DRI-EAF</code></td><td>Direct Reduced Iron + EAF</td></tr>
    <tr><td><code>DRI-BOF</code></td><td>Direct Reduced Iron + BOF</td></tr>
    <tr><td><code>COREX</code></td><td>Smelting reduction</td></tr>
    <tr><td><code>OTHER</code></td><td>Other route</td></tr>
  </tbody>
</table>
</div>

#### MethodologyCode

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Code</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>TOM01</code></td><td>Mass balance</td></tr>
    <tr><td><code>TOM02</code></td><td>Continuous emissions monitoring system (CEMS)</td></tr>
  </tbody>
</table>
</div>

#### ElectricitySourceCode

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Code</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>SOE01</code></td><td>Specific contract (PPA)</td></tr>
    <tr><td><code>SOE02</code></td><td>National grid average factor</td></tr>
    <tr><td><code>SOE03</code></td><td>Other source</td></tr>
  </tbody>
</table>
</div>

#### DatasetStatus

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Value</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>draft</code></td><td>Draft, subject to changes</td></tr>
    <tr><td><code>final</code></td><td>Final, period closed</td></tr>
  </tbody>
</table>
</div>

---

## Cardinality

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Element</th><th>Min</th><th>Max</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>CBAMProducerDataPackage</code></td><td>1</td><td>1</td><td>Root element</td></tr>
    <tr><td><code>Installation</code></td><td>1</td><td>∞</td><td>At least one installation required</td></tr>
    <tr><td><code>Product</code></td><td>1</td><td>∞</td><td>At least one product per installation</td></tr>
    <tr><td><code>ConsolidatedSummary</code></td><td>0</td><td>1</td><td>Optional</td></tr>
    <tr><td><code>PackageMetadata</code></td><td>0</td><td>1</td><td>Optional</td></tr>
  </tbody>
</table>
</div>

---

## Special Attributes

### NON-REGULATORY Fields

```xml
<LegalName regulatory="false" optional="true">...</LegalName>
```

### INFORMATIVE Fields

```xml
<CnCode informative="true" status="to_be_confirmed_by_importer">72083900</CnCode>
```

Possible `status` values for unprovided codes:
- `to_be_confirmed_by_importer`
- `not_provided`

---

## Validation

The XSD schema ensures:

1. **Correct data types** (strings, numbers, dates)
2. **Enumerations** with permitted values
3. **Formats** (CN Code = 8 digits, Country = 2 letters)
4. **Uniqueness** of IDs (Installation and Product)
5. **Cardinality** (minimum and maximum element counts)
