---
layout: docs
title: "Getting Started with the CBAM Producer Data Package"
page_title: "Getting Started"
breadcrumb: "Getting Started"
description: "A quick guide to creating, validating, and using the CBAM Producer Data Package format."
prev_page:
  url: /
  title: "Home"
next_page:
  url: /docs/concept
  title: "Concept"
---

## Overview

This guide will help you get started with the **CBAM Producer Data Package** in a few minutes. By the end, you will have:

1. ✅ Downloaded the XSD Schema
2. ✅ Created your first XML file
3. ✅ Validated the file against the schema

---

## Step 1: Download the XSD Schema

The XSD schema defines the valid structure of the data package. You need it to validate your XML files.

### Direct Download

<a href="{{ '/schema/cbam-producer-data-package-v2.xsd' | relative_url }}" class="btn btn-primary" style="margin: 1rem 0;">
  <i class="fas fa-download"></i> Download Schema XSD v2.0
</a>

### Command Line

```bash
# Linux/Mac
curl -O https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd

# Windows (PowerShell)
Invoke-WebRequest -Uri "https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd" -OutFile "cbam-producer-data-package-v2.xsd"
```

---

## Step 2: Basic XML Structure

Every CBAM Producer Data Package follows this basic structure:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CBAMProducerDataPackage 
    xmlns="https://rgtmaia.github.io/cbam-spec/schema/package/v2"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://rgtmaia.github.io/cbam-spec/schema/package/v2 
                        https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd"
    version="2.0"
    schemaVersion="2.0.0">

  <!-- Package Metadata -->
  <PackageMetadata>
    <PackageId>PKG-2024-001</PackageId>
    <GenerationTimestamp>2024-01-15T10:30:00Z</GenerationTimestamp>
    <Status>draft</Status>
  </PackageMetadata>

  <!-- Operator (Producer) Information -->
  <Operator>
    <OperatorId>OP-XX-001</OperatorId>
    <LegalName>Example Producer Ltd.</LegalName>
    <Country>XX</Country>
  </Operator>

  <!-- Installations -->
  <Installations>
    <Installation>
      <!-- installation data -->
    </Installation>
  </Installations>

  <!-- Products -->
  <Products>
    <Product>
      <!-- product data -->
    </Product>
  </Products>

</CBAMProducerDataPackage>
```

---

## Step 3: Use a Ready-Made Example

The easiest way to get started is to use one of our examples as a template:

<div class="cards-grid" style="margin: 1.5rem 0;">
  <a href="{{ '/examples/example-v2-minimal.xml' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon" style="background: linear-gradient(135deg, var(--color-info) 0%, #1d4ed8 100%);">
      <i class="fas fa-file-alt"></i>
    </div>
    <h3>Minimal Example</h3>
    <p>Basic structure with 1 installation and 1 product. Ideal for understanding the format.</p>
  </a>
  
  <a href="{{ '/examples/example-v2-complete.xml' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon" style="background: linear-gradient(135deg, var(--color-success) 0%, #15803d 100%);">
      <i class="fas fa-file-code"></i>
    </div>
    <h3>Complete Example</h3>
    <p>2 installations, 3 products, precursor emissions. Demonstrates all features.</p>
  </a>
</div>

### Download Examples via Terminal

```bash
# Minimal Example
curl -O https://rgtmaia.github.io/cbam-spec/examples/example-v2-minimal.xml

# Complete Example
curl -O https://rgtmaia.github.io/cbam-spec/examples/example-v2-complete.xml
```

---

## Step 4: Validate Your File

After creating or modifying your XML file, you should validate it against the XSD schema.

### Linux/Mac (xmllint)

```bash
# Install xmllint (if not already installed)
# Ubuntu/Debian: sudo apt install libxml2-utils
# Mac: brew install libxml2

# Validate
xmllint --schema cbam-producer-data-package-v2.xsd your-file.xml --noout
```

### Windows (PowerShell)

```powershell
# Using .NET (native to Windows)
$schema = [System.Xml.Schema.XmlSchema]::Read(
    [System.Xml.XmlReader]::Create("cbam-producer-data-package-v2.xsd"), 
    $null
)

$settings = New-Object System.Xml.XmlReaderSettings
$settings.Schemas.Add($schema)
$settings.ValidationType = [System.Xml.ValidationType]::Schema

$reader = [System.Xml.XmlReader]::Create("your-file.xml", $settings)
while ($reader.Read()) { }
$reader.Close()

Write-Host "Validation completed successfully!"
```

### Python

```python
from lxml import etree

# Load schema
with open('cbam-producer-data-package-v2.xsd', 'rb') as f:
    schema_doc = etree.parse(f)
    schema = etree.XMLSchema(schema_doc)

# Load and validate XML
with open('your-file.xml', 'rb') as f:
    doc = etree.parse(f)

if schema.validate(doc):
    print("✅ XML is valid!")
else:
    print("❌ Validation errors:")
    for error in schema.error_log:
        print(f"  Line {error.line}: {error.message}")
```

---

## Step 5: Understanding Field Categories

Fields are classified into three categories:

<div class="table-wrapper">
<table>
  <thead>
    <tr>
      <th>Category</th>
      <th>Badge</th>
      <th>What it means</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>REGULATORY</strong></td>
      <td><span class="badge badge-red">🔴 Regulatory</span></td>
      <td>Required by Regulation EU 2023/956. Mandatory.</td>
    </tr>
    <tr>
      <td><strong>NON-REGULATORY</strong></td>
      <td><span class="badge badge-yellow">🟡 Non-Regulatory</span></td>
      <td>For traceability and human readability. Recommended.</td>
    </tr>
    <tr>
      <td><strong>INFORMATIVE</strong></td>
      <td><span class="badge badge-blue">🔵 Informative</span></td>
      <td>Importer responsibility. Optional for producers.</td>
    </tr>
  </tbody>
</table>
</div>

<div class="info-box">
  <div class="info-box-title">
    <i class="fas fa-info-circle"></i> Tip
  </div>
  <p>For rapid implementation, focus first on <strong>REGULATORY</strong> fields. Other fields can be added later.</p>
</div>

---

## Next Steps

Now that you have created and validated your first file, explore the full documentation:

<div class="cards-grid" style="margin: 1.5rem 0;">
  <a href="{{ '/docs/concept' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-lightbulb"></i>
    </div>
    <h3>Concept</h3>
    <p>Understand the regulatory context and the purpose of the format.</p>
  </a>
  
  <a href="{{ '/docs/structure' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-sitemap"></i>
    </div>
    <h3>XML Structure</h3>
    <p>Complete reference of all elements and attributes.</p>
  </a>
</div>

---

## Need Help?

- 📖 Read the [full documentation]({{ '/docs/concept' | relative_url }})
- 🐛 Report issues on [GitHub Issues]({{ site.github.repository_url }}/issues)
- 💬 Questions? Open a [Discussion]({{ site.github.repository_url }}/discussions)
