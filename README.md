---
title: "CBAM Producer Data Package Specification"
description: "CBAM Producer Data Package Specification - open technical standard for emissions data exchange under EU CBAM regulation between third-country producers and European importers."
keywords: "CBAM, Carbon Border Adjustment Mechanism, emissions data, EU regulation, XML schema, producer data package, embedded emissions, carbon footprint, international trade, EU 2023/956"
lang: pt-BR
---

<!-- SEO Meta Tags -->
<meta name="description" content="CBAM Producer Data Package Specification - open technical standard for emissions data exchange under EU CBAM regulation.">
<meta name="keywords" content="CBAM, Carbon Border Adjustment Mechanism, emissions data, XML schema, EU regulation, embedded emissions">
<meta name="author" content="CBAM Spec Contributors">
<meta property="og:title" content="CBAM Producer Data Package Specification">
<meta property="og:description" content="Especificação técnica pública do formato de troca de dados de emissões no contexto do CBAM europeu.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://rgtmaia.github.io/cbam-spec/">

# CBAM Producer Data Package Specification

> **Versão:** 2.0  
> **Última Atualização:** Janeiro 2026  
> **Licença:** MIT  
> **Namespace:** `https://rgtmaia.github.io/cbam-spec/schema/package/v2`

---

## 📑 Navegação Rápida

| Seção | Descrição |
|-------|-----------|
| [📘 Conceito](docs/concept.md) | O que é o formato e seu propósito |
| [🎯 Escopo](docs/concept.md#escopo-regulatório-vs-não-regulatório) | Campos regulatórios vs informativos |
| [👥 Papéis](docs/concept.md#o-que-o-produtor-fornece) | Responsabilidades produtor vs importador |
| [🏗️ Estrutura XML](docs/structure.md) | Hierarquia e tipos de dados |
| [🔄 Versionamento](docs/lifecycle.md) | Ciclo de vida draft → final |
| [📖 Glossário](docs/concept.md#tipos-de-emissões) | Termos e definições |
| [📄 Exemplos](#-download-de-exemplos) | Arquivos XML de exemplo |

---

## Sobre

O **CBAM Producer Data Package** é um formato estruturado de dados para troca de informações de emissões entre produtores de países terceiros (não-UE) e importadores europeus, no contexto do **Carbon Border Adjustment Mechanism** (CBAM) da União Europeia.

Este repositório contém a especificação técnica pública do formato, incluindo:

- 📘 Documentação conceitual e estrutural
- 📐 Schema XML (XSD) para validação
- 📄 Exemplos de arquivos XML válidos

---

## ⚠️ Aviso Legal Importante

> **Este documento NÃO é um relatório de submissão CBAM (QReport).**

O CBAM Producer Data Package:

- ❌ **NÃO pode** ser submetido diretamente ao CBAM Registry da União Europeia
- ❌ **NÃO substitui** os formulários oficiais da Comissão Europeia
- ❌ **NÃO contém** metodologias de cálculo ou algoritmos proprietários

O formato serve exclusivamente como **contrato de dados** entre produtores e importadores, facilitando a comunicação padronizada de emissões incorporadas em bens exportados para a UE.

---

## Contexto Regulatório

O CBAM (Regulamento UE 2023/956) estabelece que importadores europeus devem reportar trimestralmente as emissões incorporadas em determinados produtos importados. Os produtores de países terceiros precisam fornecer esses dados aos seus clientes na UE.

```
┌─────────────────┐     ┌───────────────────────┐     ┌─────────────────┐
│    PRODUTOR     │────▶│  Producer Data        │────▶│   IMPORTADOR    │
│  (País Terceiro)│     │  Package (este spec)  │     │      (UE)       │
└─────────────────┘     └───────────────────────┘     └────────┬────────┘
                                                               │
                                                               ▼
                                                      ┌─────────────────┐
                                                      │  CBAM Registry  │
                                                      │  (Submissão UE) │
                                                      └─────────────────┘
```

---

## 📥 Download do Schema (XSD)

### Link Direto Público

| Arquivo | URL Pública |
|---------|-------------|
| **Schema XSD v2** | [https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd](https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd) |

### Download via Terminal

```bash
# Download do Schema XSD
curl -O https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd

# Ou via wget
wget https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd
```

### Referência no XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CBAMProducerDataPackage 
    xmlns="https://rgtmaia.github.io/cbam-spec/schema/package/v2"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://rgtmaia.github.io/cbam-spec/schema/package/v2 
                        https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd"
    version="2.0"
    schemaVersion="2.0.0">
  <!-- conteúdo -->
</CBAMProducerDataPackage>
```

---

## 📄 Download de Exemplos

### Exemplo Mínimo (`example-v2-minimal.xml`)

| | |
|---|---|
| **Arquivo** | [example-v2-minimal.xml](examples/example-v2-minimal.xml) |
| **URL Pública** | [https://rgtmaia.github.io/cbam-spec/examples/example-v2-minimal.xml](https://rgtmaia.github.io/cbam-spec/examples/example-v2-minimal.xml) |
| **Descrição** | Estrutura mínima válida com 1 instalação e 1 produto |
| **Uso** | Ideal para compreender a estrutura básica do formato |

```bash
curl -O https://rgtmaia.github.io/cbam-spec/examples/example-v2-minimal.xml
```

### Exemplo Completo (`example-v2-complete.xml`)

| | |
|---|---|
| **Arquivo** | [example-v2-complete.xml](examples/example-v2-complete.xml) |
| **URL Pública** | [https://rgtmaia.github.io/cbam-spec/examples/example-v2-complete.xml](https://rgtmaia.github.io/cbam-spec/examples/example-v2-complete.xml) |
| **Descrição** | Exemplo completo demonstrando todas as funcionalidades |
| **Uso** | Referência para implementações completas |

**O exemplo completo demonstra:**
- ✅ 2 instalações com rotas diferentes (BF-BOF integrada e EAF elétrica)
- ✅ 3 produtos com diferentes características
- ✅ Uso de dados reais (`DeterminationType: 01`) e valores default (`02`)
- ✅ Emissões de precursores (materiais de entrada)
- ✅ Resumo consolidado (`ConsolidatedSummary`)
- ✅ Metadados completos com disclaimers legais em PT e EN
- ✅ Fatores de emissão de eletricidade (grid nacional)

```bash
curl -O https://rgtmaia.github.io/cbam-spec/examples/example-v2-complete.xml
```

---

## 📚 Documentação Completa

| Seção | Documento | Descrição |
|-------|-----------|-----------|
| **Conceito** | [📘 concept.md](docs/concept.md) | O que é o CBAM Producer Data Package e seu propósito |
| **Escopo** | [📘 concept.md#escopo](docs/concept.md#escopo-regulatório-vs-não-regulatório) | Campos regulatórios vs não-regulatórios |
| **Papéis** | [📘 concept.md#papéis](docs/concept.md#o-que-o-produtor-fornece) | Responsabilidades produtor vs importador |
| **Estrutura** | [🏗️ structure.md](docs/structure.md) | Hierarquia do XML e tipos de dados |
| **Versionamento** | [🔄 lifecycle.md](docs/lifecycle.md) | Estados draft/final e ciclo de vida |
| **Avisos Legais** | [⚖️ legal-notices.md](docs/legal-notices.md) | Disclaimers e limitações |

### Estrutura do Repositório

```
cbam-spec/
├── README.md                                    # Este arquivo
├── _config.yml                                  # Configuração GitHub Pages
├── docs/
│   ├── concept.md                               # Conceito e propósito
│   ├── structure.md                             # Estrutura do XML
│   ├── lifecycle.md                             # Versionamento
│   └── legal-notices.md                         # Avisos legais
├── schema/
│   └── cbam-producer-data-package-v2.xsd        # Schema XSD público
└── examples/
    ├── example-v2-minimal.xml                   # Exemplo mínimo
    └── example-v2-complete.xml                  # Exemplo completo
```

---

## 🔧 Uso Rápido

### Validação de um arquivo XML

```bash
# Linux/macOS/WSL
xmllint --schema https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd seu-arquivo.xml --noout

# Windows (com schema local)
choco install libxml2
curl -O https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd
xmllint --schema cbam-producer-data-package-v2.xsd seu-arquivo.xml --noout
```

### Validação Programática (exemplo)

```python
# Python com lxml
from lxml import etree

schema_url = "https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd"
schema = etree.XMLSchema(etree.parse(schema_url))
doc = etree.parse("seu-arquivo.xml")
schema.validate(doc)  # True se válido
```

---

## 👥 Público-Alvo

- 🏭 **Produtores** de países terceiros que exportam para a UE
- 🚢 **Importadores** europeus que precisam reportar emissões ao CBAM Registry
- 📊 **Consultorias** de compliance e sustentabilidade
- 💻 **Desenvolvedores** de sistemas de gestão ambiental e ERPs
- 🔍 **Auditores** e verificadores de dados de emissões

---

## 🏭 Setores Cobertos

O CBAM (conforme Anexo I do Regulamento UE 2023/956) cobre os seguintes setores:

| Setor | Produtos Típicos | Códigos CN |
|-------|------------------|------------|
| **Ferro e Aço** | Ferro-gusa, aços carbono, inoxidável, ligas | 72xx |
| **Alumínio** | Alumínio primário e ligas | 76xx |
| **Cimento** | Clínquer e cimento Portland | 2523 |
| **Fertilizantes** | Amônia, nitratos, ureia | 2808, 3102 |
| **Hidrogênio** | Hidrogênio (em fases futuras) | 2804 |
| **Eletricidade** | Eletricidade importada | 2716 |

---

## 🏷️ Classificação de Campos

O schema distingue claramente três tipos de campos:

### 🔴 REGULATÓRIOS (REGULATORY)
Campos exigidos pelo Regulamento UE 2023/956. São obrigatórios para compliance CBAM.

**Exemplos:** `DeterminationType`, `SpecificEmissions`, `RouteCode`, `MethodologyCode`

### 🟡 NÃO-REGULATÓRIOS (NON-REGULATORY)
Campos informativos para legibilidade humana, rastreabilidade ou integração com sistemas.

**Exemplos:** `Description`, `LegalName`, `ConsolidatedSummary`, `Justification`

### 🔵 INFORMATIVOS (INFORMATIVE)
Campos cuja responsabilidade final é do **importador**, não do produtor.

**Exemplos:** `CnCode`, `HsCode` (códigos aduaneiros)

➡️ Veja detalhes completos em [docs/structure.md](docs/structure.md)

---

## 📜 Referências Regulatórias

| Documento | Descrição |
|-----------|-----------|
| 📜 [EU 2023/956](https://eur-lex.europa.eu/eli/reg/2023/956) | Regulamento CBAM principal |
| 📜 [EU 2023/1773](https://eur-lex.europa.eu/eli/reg_impl/2023/1773) | Regulamento de Implementação |
| 🌐 [CBAM Registry](https://cbam.ec.europa.eu/) | Portal oficial da Comissão Europeia |
| 📋 [Combined Nomenclature](https://taxation-customs.ec.europa.eu/customs-4/calculation-customs-duties/customs-tariff/combined-nomenclature_en) | Códigos CN oficiais |

---

## 🤝 Contribuições

Este é um formato aberto destinado a facilitar a comunicação de dados de emissões no contexto do CBAM. Sugestões de melhoria são bem-vindas através de Issues.

### Como Contribuir

1. Abra uma **Issue** para reportar problemas ou sugerir melhorias
2. Faça um **Fork** e submeta um **Pull Request** para alterações
3. Siga as convenções de nomenclatura e documentação existentes

---

## 📄 Licença

MIT License - Uso livre para implementação e integração.

---

<p align="center">
  <strong>CBAM Producer Data Package Specification v2.0</strong><br>
  <em>Facilitando a comunicação de dados de emissões no contexto do CBAM</em><br><br>
  <a href="https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd">📥 Download XSD</a> •
  <a href="docs/concept.md">📘 Documentação</a> •
  <a href="examples/example-v2-complete.xml">📄 Exemplo</a>
</p>
