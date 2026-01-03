---
layout: docs
title: "CBAM Producer Data Package Concept"
page_title: "Concept"
breadcrumb: "Concept"
description: "Understanding what the CBAM Producer Data Package is, its purpose, and how it fits into the EU regulatory framework."
prev_page:
  url: /getting-started
  title: "Getting Started"
next_page:
  url: /docs/structure
  title: "XML Structure"
---

## What is CBAM?

The **Carbon Border Adjustment Mechanism** (CBAM) is an EU regulatory instrument established by Regulation (EU) 2023/956, which entered into force in October 2023. Its objectives are:

1. Prevent "carbon leakage" (the relocation of industrial production to countries with less stringent environmental regulations)
2. Level the playing field between EU producers (subject to EU ETS) and importers
3. Incentivise global decarbonisation of industrial production

---

## What is the CBAM Producer Data Package?

The **CBAM Producer Data Package** is a structured data format that enables standardised communication of emissions information between:

- **Producers** located in third countries (non-EU)
- **Importers** based in the EU who purchase and import these products

### Purpose

<div class="info-box">
  <div class="info-box-title">
    <i class="fas fa-info-circle"></i> CBAM Data Flow
  </div>
  <p><strong>PRODUCER</strong> → generates <strong>Producer Data Package</strong> → sends to <strong>IMPORTER</strong> → who submits <strong>QReport</strong> to the <strong>CBAM Registry</strong></p>
</div>

The format defines the data structure that enables producers to provide emissions information in a standardised way, allowing importers to:

1. **Validate** the consistency of received data
2. **Convert** to the official CBAM Registry format
3. **Submit** quarterly reports (QReport) to the competent authorities

---

## Regulatory vs. Non-Regulatory Scope

### Regulatory Fields

Fields directly required by Regulation EU 2023/956 and its implementing regulations. Examples:

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Field</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>DeterminationType</code></td><td>Whether data is actual (01) or default (02)</td></tr>
    <tr><td><code>SpecificEmissions</code></td><td>Specific embedded emissions in tCO2e per tonne</td></tr>
    <tr><td><code>RouteCode</code></td><td>Production route (BF-BOF, EAF, etc.)</td></tr>
    <tr><td><code>MethodologyCode</code></td><td>Calculation methodology (TOM01, TOM02)</td></tr>
  </tbody>
</table>
</div>

### Non-Regulatory Fields

Informational fields for human readability, traceability, or system integration:

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Field</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>Description</code></td><td>Product text description</td></tr>
    <tr><td><code>LegalName</code></td><td>Company legal name</td></tr>
    <tr><td><code>ConsolidatedSummary</code></td><td>Aggregated summary (informational only)</td></tr>
    <tr><td><code>PackageMetadata</code></td><td>Package generation metadata</td></tr>
  </tbody>
</table>
</div>

### Informative Fields

Fields where the final classification responsibility lies with the **importer**:

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Field</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><code>CnCode</code></td><td>Combined Nomenclature code (8 digits)</td></tr>
    <tr><td><code>HsCode</code></td><td>Harmonised System code (6 digits)</td></tr>
  </tbody>
</table>
</div>

<div class="warning-box">
  <div class="warning-box-title">
    <i class="fas fa-exclamation-triangle"></i> Important
  </div>
  <p>The producer provides their best estimate, but <strong>legal responsibility for correct customs classification lies with the importer</strong>.</p>
</div>

---

## What the Producer Provides

The producer is responsible for supplying:

1. **Company identification** (operator)
2. **Installation data** (production facilities)
3. **Manufactured products** and their quantities
4. **Embedded emissions**:
   - Direct emissions (Scope 1)
   - Indirect emissions (Scope 2, electricity consumption)
   - Precursor emissions (where applicable)
5. **Methodology used** for emissions determination

---

## What the Importer Does

The EU importer receives the data package and:

1. **Validates** data consistency and completeness
2. **Confirms** customs classification (CN/HS codes)
3. **Converts** data to the CBAM Registry format
4. **Submits** the quarterly report (QReport) to the competent authority
5. **Purchases** CBAM certificates corresponding to the embedded emissions

---

## Types of Emissions

CBAM considers three categories of embedded emissions:

<div class="cards-grid" style="margin: 1.5rem 0;">
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #ef4444 0%, #b91c1c 100%);">
      <i class="fas fa-fire"></i>
    </div>
    <h3>Direct Emissions</h3>
    <p><strong>Scope 1:</strong> Fuel combustion, chemical reactions, industrial processes at the installation.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);">
      <i class="fas fa-bolt"></i>
    </div>
    <h3>Indirect Emissions</h3>
    <p><strong>Scope 2:</strong> Electricity consumption from the grid.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #8b5cf6 0%, #6d28d9 100%);">
      <i class="fas fa-cubes"></i>
    </div>
    <h3>Precursors</h3>
    <p>Emissions from input materials that are themselves CBAM goods (e.g., pig iron used in steel production).</p>
  </div>
</div>

### Specific Emissions

CBAM primarily uses **specific embedded emissions** (per unit of product):

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Unit</th><th>Usage</th></tr>
  </thead>
  <tbody>
    <tr><td><code>tCO2e/t</code></td><td>Tonnes of CO2eq per tonne of product</td></tr>
    <tr><td><code>tCO2e/MWh</code></td><td>For electricity</td></tr>
  </tbody>
</table>
</div>

---

## Reporting Period

CBAM operates on quarterly cycles:

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Quarter</th><th>Period</th><th>Submission Deadline</th></tr>
  </thead>
  <tbody>
    <tr><td>Q1</td><td>January – March</td><td>30 April</td></tr>
    <tr><td>Q2</td><td>April – June</td><td>31 July</td></tr>
    <tr><td>Q3</td><td>July – September</td><td>31 October</td></tr>
    <tr><td>Q4</td><td>October – December</td><td>31 January (following year)</td></tr>
  </tbody>
</table>
</div>

---

## References

- [Regulation EU 2023/956 (CBAM)](https://eur-lex.europa.eu/eli/reg/2023/956)
- [Implementing Regulation EU 2023/1773](https://eur-lex.europa.eu/eli/reg_impl/2023/1773)
- [European Commission CBAM Portal](https://cbam.ec.europa.eu/)
