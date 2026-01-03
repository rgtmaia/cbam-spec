---
layout: default
title: "CBAM Producer Data Package Specification"
description: "A standardised data exchange format for communicating embedded emissions between third-country producers and EU importers under the Carbon Border Adjustment Mechanism."
---

<!-- Quick Start Box -->
<div class="quick-start">
  <div class="quick-start-icon">
    <i class="fas fa-rocket"></i>
  </div>
  <div class="quick-start-content">
    <div class="quick-start-title">Getting Started?</div>
    <p class="quick-start-desc">Download the Schema, review an example, and validate your first XML file in minutes.</p>
  </div>
  <div class="quick-start-actions">
    <a href="{{ '/getting-started' | relative_url }}" class="quick-start-link">
      <i class="fas fa-play-circle"></i> Quick Start Guide
    </a>
    <a href="{{ '/examples/example-v2-complete.xml' | relative_url }}" class="quick-start-link">
      <i class="fas fa-code"></i> View Example
    </a>
  </div>
</div>

<!-- Alert Box -->
<div class="alert">
  <div class="alert-title">
    <i class="fas fa-exclamation-triangle"></i>
    Important Legal Notice
  </div>
  <p><strong>This document is NOT a CBAM submission report (QReport).</strong></p>
  <ul>
    <li>❌ <strong>CANNOT</strong> be submitted directly to the EU CBAM Registry</li>
    <li>❌ <strong>DOES NOT replace</strong> official European Commission forms</li>
    <li>❌ <strong>DOES NOT contain</strong> proprietary calculation methodologies</li>
  </ul>
</div>

## <i class="fas fa-users"></i> Who Should Use This Format?

<div class="cards-grid">
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%);">
      <i class="fas fa-industry"></i>
    </div>
    <h3>Producers</h3>
    <p>Third-country operators who need to provide emissions data to European customers in a standardised, machine-readable format.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #8b5cf6 0%, #6d28d9 100%);">
      <i class="fas fa-ship"></i>
    </div>
    <h3>Importers</h3>
    <p>EU-based companies that need to receive, validate, and process emissions data from suppliers for CBAM Registry submission.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);">
      <i class="fas fa-user-tie"></i>
    </div>
    <h3>Consultants</h3>
    <p>Compliance specialists, ESG advisors, and regulatory experts supporting organisations with CBAM obligations.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #ec4899 0%, #be185d 100%);">
      <i class="fas fa-laptop-code"></i>
    </div>
    <h3>Developers</h3>
    <p>Technical teams implementing system integrations to automate emissions data exchange and validation.</p>
  </div>
</div>

---

## <i class="fas fa-book-open"></i> Documentation

<div class="cards-grid">
  <a href="{{ '/docs/concept' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-lightbulb"></i>
    </div>
    <h3>Concept</h3>
    <p>Understanding the CBAM Producer Data Package: purpose, regulatory context, and data flow.</p>
  </a>
  
  <a href="{{ '/docs/structure' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-sitemap"></i>
    </div>
    <h3>XML Structure</h3>
    <p>Document hierarchy, data types, enumerations, and element reference.</p>
  </a>
  
  <a href="{{ '/docs/lifecycle' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-sync-alt"></i>
    </div>
    <h3>Dataset Lifecycle</h3>
    <p>Draft-to-final workflow, versioning, and data governance.</p>
  </a>
  
  <a href="{{ '/docs/legal-notices' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-balance-scale"></i>
    </div>
    <h3>Legal Notices</h3>
    <p>Disclaimers, licensing, and limitations of the format.</p>
  </a>
</div>

---

## <i class="fas fa-download"></i> Downloads

<div class="download-box">
  <div class="download-item featured">
    <div class="download-info">
      <div class="download-icon">
        <i class="fas fa-file-code"></i>
      </div>
      <div>
        <div class="download-name">Schema XSD v2.0</div>
        <div class="download-desc">XML Schema for package validation · Primary file</div>
      </div>
    </div>
    <a href="{{ '/schema/cbam-producer-data-package-v2.xsd' | relative_url }}" class="btn btn-primary">
      <i class="fas fa-download"></i> Download XSD
    </a>
  </div>
  
  <div class="download-item">
    <div class="download-info">
      <div class="download-icon" style="background: var(--color-info);">
        <i class="fas fa-file-alt"></i>
      </div>
      <div>
        <div class="download-name">Minimal Example</div>
        <div class="download-desc">Basic structure with 1 installation and 1 product</div>
      </div>
    </div>
    <a href="{{ '/examples/example-v2-minimal.xml' | relative_url }}" class="btn btn-secondary">
      <i class="fas fa-eye"></i> View Example
    </a>
  </div>
  
  <div class="download-item">
    <div class="download-info">
      <div class="download-icon" style="background: var(--color-success);">
        <i class="fas fa-file-alt"></i>
      </div>
      <div>
        <div class="download-name">Complete Example</div>
        <div class="download-desc">2 installations, 3 products, all features</div>
      </div>
    </div>
    <a href="{{ '/examples/example-v2-complete.xml' | relative_url }}" class="btn btn-secondary">
      <i class="fas fa-eye"></i> View Example
    </a>
  </div>
</div>

### Complete Example Features

<div class="features-list">
  <div class="feature-item"><i class="fas fa-check-circle"></i> 2 installations (BF-BOF and EAF)</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> 3 distinct products</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> Both actual and default values</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> Precursor emissions</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> Consolidated summary</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> Multilingual disclaimers</div>
</div>

---

## <i class="fas fa-code"></i> XML Reference

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CBAMProducerDataPackage 
    xmlns="https://rgtmaia.github.io/cbam-spec/schema/package/v2"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://rgtmaia.github.io/cbam-spec/schema/package/v2 
                        https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd"
    version="2.0"
    schemaVersion="2.0.0">
  <!-- content -->
</CBAMProducerDataPackage>
```

### Command-Line Validation

```bash
# Download the Schema
curl -O https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd

# Validate an XML file (Linux/Mac)
xmllint --schema cbam-producer-data-package-v2.xsd your-file.xml --noout

# Windows (PowerShell) - install xmllint via: choco install xsltproc
```

---

## <i class="fas fa-tags"></i> Field Classification

The schema distinguishes three field types with different compliance implications:

<div class="table-wrapper">
<table>
  <thead>
    <tr>
      <th>Type</th>
      <th>Badge</th>
      <th>Description</th>
      <th>Examples</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>REGULATORY</strong></td>
      <td><span class="badge badge-red">🔴 Regulatory</span></td>
      <td>Required by EU 2023/956</td>
      <td><code>DeterminationType</code>, <code>SpecificEmissions</code></td>
    </tr>
    <tr>
      <td><strong>NON-REGULATORY</strong></td>
      <td><span class="badge badge-yellow">🟡 Non-Regulatory</span></td>
      <td>Informational / traceability</td>
      <td><code>Description</code>, <code>LegalName</code></td>
    </tr>
    <tr>
      <td><strong>INFORMATIVE</strong></td>
      <td><span class="badge badge-blue">🔵 Informative</span></td>
      <td>Importer responsibility</td>
      <td><code>CnCode</code>, <code>HsCode</code></td>
    </tr>
  </tbody>
</table>
</div>

---

## <i class="fas fa-industry"></i> Covered Sectors

The CBAM (as per Annex I of Regulation EU 2023/956) applies to the following sectors:

<div class="table-wrapper">
<table>
  <thead>
    <tr>
      <th>Sector</th>
      <th>Typical Products</th>
      <th>CN Codes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Iron and Steel</strong></td>
      <td>Pig iron, carbon steel, stainless steel</td>
      <td>72xx</td>
    </tr>
    <tr>
      <td><strong>Aluminium</strong></td>
      <td>Primary aluminium and alloys</td>
      <td>76xx</td>
    </tr>
    <tr>
      <td><strong>Cement</strong></td>
      <td>Clinker and Portland cement</td>
      <td>2523</td>
    </tr>
    <tr>
      <td><strong>Fertilisers</strong></td>
      <td>Ammonia, nitrates, urea</td>
      <td>2808, 3102</td>
    </tr>
    <tr>
      <td><strong>Hydrogen</strong></td>
      <td>Hydrogen</td>
      <td>2804</td>
    </tr>
    <tr>
      <td><strong>Electricity</strong></td>
      <td>Imported electricity</td>
      <td>2716</td>
    </tr>
  </tbody>
</table>
</div>

---

## <i class="fas fa-gavel"></i> Regulatory References

<div class="table-wrapper">
<table>
  <thead>
    <tr>
      <th>Document</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://eur-lex.europa.eu/eli/reg/2023/956">EU 2023/956</a></td>
      <td>CBAM Regulation (primary legislation)</td>
    </tr>
    <tr>
      <td><a href="https://eur-lex.europa.eu/eli/reg_impl/2023/1773">EU 2023/1773</a></td>
      <td>Implementing Regulation</td>
    </tr>
    <tr>
      <td><a href="https://cbam.ec.europa.eu/">CBAM Registry</a></td>
      <td>Official European Commission portal</td>
    </tr>
    <tr>
      <td><a href="https://taxation-customs.ec.europa.eu/customs-4/calculation-customs-duties/customs-tariff/combined-nomenclature_en">Combined Nomenclature</a></td>
      <td>Official CN codes reference</td>
    </tr>
  </tbody>
</table>
</div>

---

## <i class="fas fa-file-contract"></i> Licence

**MIT License** – Free to use for implementation and integration.

This is an open format designed to facilitate emissions data communication in the CBAM context.
Improvement suggestions are welcome via [GitHub Issues]({{ site.github.repository_url }}/issues).
