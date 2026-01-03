---
layout: docs
title: "Dataset Lifecycle"
page_title: "Lifecycle"
breadcrumb: "Lifecycle"
description: "How a CBAM Producer Data Package is created, versioned, transmitted, and archived over time."
prev_page:
  url: /docs/structure
  title: "XML Structure"
next_page:
  url: /docs/legal-notices
  title: "Legal Notices"
---

## Overview

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  CREATION   │───►│  REVISION   │───►│ TRANSMISSION│───►│  ARCHIVAL   │
│   (draft)   │    │   (draft)   │    │   (final)   │    │   (final)   │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
     │                   │                   │                   │
     ▼                   ▼                   ▼                   ▼
  Dataset v1.0       Dataset v1.x       Dataset final      10yr retention
```

---

## Dataset States

### DatasetStatus

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Status</th><th>Description</th><th>Editable</th></tr>
  </thead>
  <tbody>
    <tr><td><code>draft</code></td><td>In progress, subject to changes</td><td>✅ Yes</td></tr>
    <tr><td><code>final</code></td><td>Closed, for reference only</td><td>❌ No</td></tr>
  </tbody>
</table>
</div>

### State Transitions

```
          ┌──────────────┐
          │    DRAFT     │◄────────────────┐
          └──────┬───────┘                 │
                 │                         │
        [revision]                         │
                 │                         │
                 ▼                         │
          ┌──────────────┐                 │
          │    DRAFT     │────────────────►│ (new version)
          │   (v1.x)     │                 │
          └──────┬───────┘                 │
                 │                         │
          [finalisation]                   │
                 │                         │
                 ▼                         │
          ┌──────────────┐                 │
          │    FINAL     │ ───────────────►│ (post-final correction)
          │   (vN.0)     │                 │
          └──────────────┘                 │
```

---

## Versioning

### Version Rules

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Change Type</th><th>Version</th><th>Example</th></tr>
  </thead>
  <tbody>
    <tr><td>Initial creation</td><td><code>1.0</code></td><td>First dataset for the period</td></tr>
    <tr><td>Draft revision</td><td><code>1.x</code></td><td>1.1, 1.2, 1.3...</td></tr>
    <tr><td>Post-final correction</td><td><code>N.0</code></td><td>2.0, 3.0 (supersedes previous)</td></tr>
  </tbody>
</table>
</div>

### Versioning Fields

```xml
<DatasetIdentification>
  <DatasetId>550e8400-e29b-41d4-a716-446655440000</DatasetId>
  <Version>1.2</Version>
  <GenerationDate>2026-03-15</GenerationDate>
  <DatasetStatus>draft</DatasetStatus>
</DatasetIdentification>
```

### Version History

```xml
<PackageMetadata>
  <VersionHistory>
    <PreviousVersion>
      <DatasetId>550e8400-e29b-41d4-a716-446655440000</DatasetId>
      <Version>1.1</Version>
    </PreviousVersion>
  </VersionHistory>
</PackageMetadata>
```

---

## Data Flow

### Actors

```
┌──────────────┐        ┌──────────────┐        ┌──────────────┐
│   PRODUCER   │        │   IMPORTER   │        │   EUROPEAN   │
│ (3rd country)│        │     (EU)     │        │  COMMISSION  │
└──────┬───────┘        └──────┬───────┘        └──────┬───────┘
       │                       │                       │
       │   XML Package         │                       │
       │──────────────────────►│                       │
       │                       │                       │
       │                       │   CBAM Report         │
       │                       │──────────────────────►│
       │                       │                       │
       │                       │◄──────────────────────│
       │                       │   Feedback            │
       │                       │                       │
```

### Responsibilities

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Actor</th><th>Responsibility</th></tr>
  </thead>
  <tbody>
    <tr><td><strong>Producer</strong></td><td>Generate XML with emissions data</td></tr>
    <tr><td><strong>Importer</strong></td><td>Validate and supplement data (CN/HS codes)</td></tr>
    <tr><td><strong>Importer</strong></td><td>Submit CBAM report to the transitional registry</td></tr>
    <tr><td><strong>Commission</strong></td><td>Verify and process declarations</td></tr>
  </tbody>
</table>
</div>

---

## Reporting Quarters

### CBAM Deadlines (Transitional Period)

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Quarter</th><th>Period</th><th>Deadline</th></tr>
  </thead>
  <tbody>
    <tr><td>Q1</td><td>Jan–Mar</td><td>30 April</td></tr>
    <tr><td>Q2</td><td>Apr–Jun</td><td>31 July</td></tr>
    <tr><td>Q3</td><td>Jul–Sep</td><td>31 October</td></tr>
    <tr><td>Q4</td><td>Oct–Dec</td><td>31 January (following year)</td></tr>
  </tbody>
</table>
</div>

### ReportingPeriod Example

```xml
<ReportingPeriod>
  <Year>2026</Year>
  <Quarter>1</Quarter>
  <PeriodId>2026-Q1</PeriodId>
  <SubmissionDeadline>2026-04-30</SubmissionDeadline>
</ReportingPeriod>
```

---

## Corrections and Amendments

### Before Finalisation (draft)

1. Create a new dataset version (`Version` +0.1)
2. Update `GenerationDate`
3. Keep the same `DatasetId`
4. Update `VersionHistory`

### After Finalisation (final)

1. Create a **new** dataset with `Version` +1.0
2. Generate a **new** `DatasetId`
3. Reference the previous dataset in `PreviousVersion`
4. Mark as `draft` until importer approval

---

## Archival

### Requirements

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Aspect</th><th>Requirement</th></tr>
  </thead>
  <tbody>
    <tr><td><strong>Retention</strong></td><td>Minimum 10 years from generation</td></tr>
    <tr><td><strong>Integrity</strong></td><td>SHA-256 hash of the XML file</td></tr>
    <tr><td><strong>Traceability</strong></td><td>Version history preserved</td></tr>
    <tr><td><strong>Accessibility</strong></td><td>Available for audits</td></tr>
  </tbody>
</table>
</div>

### Archival Metadata

```xml
<PackageMetadata>
  <FileIntegrity>
    <HashAlgorithm>SHA-256</HashAlgorithm>
    <HashValue>abc123...</HashValue>
  </FileIntegrity>
  <RetentionPolicy>
    <MinimumRetentionYears>10</MinimumRetentionYears>
    <ArchiveDate>2026-05-01</ArchiveDate>
  </RetentionPolicy>
</PackageMetadata>
```

---

## Complete Example

### Scenario

1. Producer creates Q1/2026 dataset on 10 Mar
2. Revision on 20 Mar after internal review
3. Sent to importer on 25 Mar
4. Importer completes and finalises on 15 Apr
5. Archived for audit purposes

### Dataset Evolution

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Stage</th><th>Version</th><th>Status</th><th>Date</th></tr>
  </thead>
  <tbody>
    <tr><td>Creation</td><td>1.0</td><td>draft</td><td>2026-03-10</td></tr>
    <tr><td>Revision</td><td>1.1</td><td>draft</td><td>2026-03-20</td></tr>
    <tr><td>Transmission</td><td>1.1</td><td>draft</td><td>2026-03-25</td></tr>
    <tr><td>Finalisation</td><td>1.1</td><td>final</td><td>2026-04-15</td></tr>
    <tr><td>Archival</td><td>1.1</td><td>final</td><td>2026-04-15</td></tr>
  </tbody>
</table>
</div>
