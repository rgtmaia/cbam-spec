---
layout: docs
title: "Legal Notices"
page_title: "Legal Notices"
breadcrumb: "Legal Notices"
description: "Licensing, responsibilities, and compliance information relating to the CBAM Producer Data Package."
prev_page:
  url: /docs/lifecycle
  title: "Lifecycle"
---

This document contains legal and compliance information relating to the CBAM Producer Data Package.

---

## Licensing

### Specification and Schema

The CBAM Producer Data Package Specification and its associated files are made available under the **Apache 2.0** licence.

```
Copyright 2024-2026 CBAM Spec Contributors

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

### Covered Files

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>File</th><th>Licence</th></tr>
  </thead>
  <tbody>
    <tr><td><code>cbam-producer-data-package-v2.xsd</code></td><td>Apache 2.0</td></tr>
    <tr><td>Documentation (Markdown)</td><td>Apache 2.0</td></tr>
    <tr><td>Examples (XML)</td><td>Apache 2.0</td></tr>
  </tbody>
</table>
</div>

---

## Disclaimer

### Purpose

This specification was developed to:

1. **Standardise** the communication of emissions data between producers and importers
2. **Facilitate** compliance with CBAM obligations during the transitional period
3. **Promote** interoperability between systems of different organisations

### Limitations

> **IMPORTANT NOTICE**
>
> This specification is a community initiative and is **NOT** an official document of the European Union or any regulatory authority.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Aspect</th><th>Status</th></tr>
  </thead>
  <tbody>
    <tr><td>Official recognition by the EU</td><td>❌ No</td></tr>
    <tr><td>Validation by the European Commission</td><td>❌ No</td></tr>
    <tr><td>Replacement of official forms</td><td>❌ No</td></tr>
    <tr><td>Use as an auxiliary format</td><td>✅ Yes</td></tr>
  </tbody>
</table>
</div>

### Responsibility

- **Users** are responsible for verifying the compliance of their data with regulatory requirements
- **Importers** must use the official CBAM Transitional Registry forms and systems for submissions
- **Developers** of this specification make no warranty of fitness for particular purposes

---

## Regulatory References

### Legal Basis

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Document</th><th>Reference</th></tr>
  </thead>
  <tbody>
    <tr><td>CBAM Regulation</td><td>EU 2023/956</td></tr>
    <tr><td>Implementing Regulation</td><td>EU 2023/1773</td></tr>
    <tr><td>Commission Guidance</td><td>C(2023) 5512</td></tr>
  </tbody>
</table>
</div>

### Official Links

- [CBAM – Taxation and Customs Union](https://taxation-customs.ec.europa.eu/carbon-border-adjustment-mechanism_en)
- [CBAM Transitional Registry](https://cbam.ec.europa.eu/)
- [EU Climate Action](https://climate.ec.europa.eu/eu-action/carbon-border-adjustment-mechanism_en)

---

## Contributing

### How to Contribute

1. **Issues**: Report problems or suggestions via GitHub Issues
2. **Pull Requests**: Submit corrections or improvements
3. **Discussions**: Participate in repository discussions

### Code of Conduct

Contributors must follow the [Contributor Covenant](https://www.contributor-covenant.org/) version 2.1.

### Review Process

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Type</th><th>Approval</th><th>Timeframe</th></tr>
  </thead>
  <tbody>
    <tr><td>Typo / minor fix</td><td>1 maintainer</td><td>~3 days</td></tr>
    <tr><td>Documentation improvement</td><td>1 maintainer</td><td>~7 days</td></tr>
    <tr><td>Schema change</td><td>2 maintainers</td><td>~14 days</td></tr>
    <tr><td>Breaking change</td><td>Consensus + RFC</td><td>~30 days</td></tr>
  </tbody>
</table>
</div>

---

## Schema Versioning

### Version Policy

This specification follows [Semantic Versioning 2.0.0](https://semver.org/):

- **MAJOR** (X.0.0): Incompatible changes
- **MINOR** (2.X.0): Backwards-compatible additions
- **PATCH** (2.0.X): Backwards-compatible fixes

### Version History

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Version</th><th>Date</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td>2.0.0</td><td>Jan 2026</td><td>Current version with field classification</td></tr>
    <tr><td>1.0.0</td><td>Oct 2024</td><td>Initial release</td></tr>
  </tbody>
</table>
</div>

### Version Support

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Version</th><th>Status</th><th>Supported Until</th></tr>
  </thead>
  <tbody>
    <tr><td>2.x</td><td>✅ Active</td><td>—</td></tr>
    <tr><td>1.x</td><td>⚠️ Legacy</td><td>Dec 2026</td></tr>
  </tbody>
</table>
</div>

---

## Contact

### Maintainers

For questions relating to the specification:

- **GitHub**: [rgtmaia/cbam-spec](https://github.com/rgtmaia/cbam-spec)
- **Issues**: Use the GitHub Issues system

### Commercial Support

This specification is community-maintained. For commercial support or enterprise implementation, please contact the maintainers.

---

## Acknowledgements

This project was inspired by:

- Environmental data standardisation initiatives
- The CBAM compliance community
- Open-source contributors

We thank all who have contributed feedback and improvements.
