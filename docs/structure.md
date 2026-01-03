---
layout: docs
title: "Estrutura do CBAM Producer Data Package"
page_title: "Estrutura XML"
breadcrumb: "Estrutura"
description: "Documentação detalhada da estrutura XML do CBAM Producer Data Package, incluindo hierarquia, tipos de dados e enumerações."
prev_page:
  url: /docs/concept
  title: "Conceito"
next_page:
  url: /docs/lifecycle
  title: "Ciclo de Vida"
---

Este documento descreve a estrutura conceitual do documento XML do CBAM Producer Data Package.

---

## Visão Hierárquica

```
CBAMProducerDataPackage (root)
│
├── @version                    # Versão do pacote (ex: "2.0")
├── @schemaVersion              # Versão do schema (ex: "2.0.0")
│
├── DatasetIdentification       # Identificação única do dataset
│   ├── DatasetId               # UUID único
│   ├── Version                 # Versão do dataset (incrementa a cada revisão)
│   ├── GenerationDate          # Data de geração
│   └── DatasetStatus           # draft | final
│
├── ReportingPeriod [REGULATORY]
│   ├── Year                    # Ano (ex: 2026)
│   ├── Quarter                 # Trimestre (1-4)
│   ├── PeriodId                # Identificador legível (ex: "2026-Q1")
│   └── SubmissionDeadline      # Prazo de submissão (opcional)
│
├── Operator [REGULATORY]
│   ├── OperatorId              # Identificador único (ex: CNPJ)
│   ├── OperatorName            # Nome comercial
│   ├── LegalName               # Razão social [NON-REGULATORY]
│   ├── Address
│   │   ├── Country             # ISO 3166-1 alpha-2 [REGULATORY]
│   │   ├── SubDivision         # Estado/Província [NON-REGULATORY]
│   │   ├── City                # Cidade [NON-REGULATORY]
│   │   └── Street              # Endereço [NON-REGULATORY]
│   └── ContactDetails          # [NON-REGULATORY]
│
├── Installations               # Lista de instalações
│   └── Installation[]
│       ├── @index              # Índice (1-based)
│       ├── InstallationId      # ID único da instalação [REGULATORY]
│       ├── InstallationName    # Nome da instalação [REGULATORY]
│       ├── Address             # (mesma estrutura do operador)
│       ├── ProductionProcess   # [REGULATORY]
│       │   ├── RouteCode       # Rota produtiva (BF-BOF, EAF, etc.)
│       │   ├── MethodologyCode # Metodologia (TOM01, TOM02)
│       │   └── RegulatoryBasis # Referência regulatória [NON-REGULATORY]
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
├── ConsolidatedSummary         # [NON-REGULATORY] (opcional)
│
└── PackageMetadata             # [NON-REGULATORY] (opcional)
```

---

## Seções Principais

### 1. DatasetIdentification

Identifica unicamente o pacote de dados.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Campo</th><th>Tipo</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>DatasetId</code></td><td>UUID</td><td>Identificador global único</td></tr>
    <tr><td><code>Version</code></td><td>String</td><td>Versão do dataset (ex: "1.0", "1.1")</td></tr>
    <tr><td><code>GenerationDate</code></td><td>Date</td><td>Data de geração (YYYY-MM-DD)</td></tr>
    <tr><td><code>DatasetStatus</code></td><td>Enum</td><td><code>draft</code> ou <code>final</code></td></tr>
  </tbody>
</table>
</div>

### 2. ReportingPeriod

Define o trimestre de referência dos dados.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Campo</th><th>Tipo</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>Year</code></td><td>gYear</td><td>Ano de referência</td></tr>
    <tr><td><code>Quarter</code></td><td>1-4</td><td>Trimestre (Q1, Q2, Q3, Q4)</td></tr>
    <tr><td><code>PeriodId</code></td><td>String</td><td>Identificador legível (ex: "2026-Q1")</td></tr>
    <tr><td><code>SubmissionDeadline</code></td><td>Date</td><td>Prazo para submissão CBAM</td></tr>
  </tbody>
</table>
</div>

### 3. Operator

Informações sobre a empresa produtora.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Campo</th><th>Classificação</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>OperatorId</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>CNPJ (Brasil), CIN (Índia), etc.</td></tr>
    <tr><td><code>OperatorName</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Nome comercial</td></tr>
    <tr><td><code>LegalName</code></td><td><span class="badge badge-yellow">NON-REGULATORY</span></td><td>Razão social</td></tr>
    <tr><td><code>Address.Country</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>País (ISO 3166-1)</td></tr>
  </tbody>
</table>
</div>

### 4. Installation

Dados de cada planta produtora.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Campo</th><th>Classificação</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>InstallationId</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Identificador único da instalação</td></tr>
    <tr><td><code>InstallationName</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Nome da instalação</td></tr>
    <tr><td><code>ProductionProcess</code></td><td><span class="badge badge-red">REGULATORY</span></td><td>Rota e metodologia de produção</td></tr>
  </tbody>
</table>
</div>

### 5. Product

Dados de cada produto fabricado.

```
Product
├── ProductId           # Identificador único do produto
├── Description         # Descrição textual
├── Category            # Categoria CBAM (aco, aluminio, etc.)
├── CommodityCode       # Códigos CN/HS [INFORMATIVE]
│   ├── CnCode          # 8 dígitos
│   └── HsCode          # 6 dígitos
├── Production          # Dados de produção
│   ├── QuantityType    # TOTAL_PRODUCTION | EU_EXPORT | REPORTED_BATCH
│   ├── Quantity        # Quantidade produzida
│   └── MeasurementUnit # t | kg | MWh
└── EmbeddedEmissions   # Emissões incorporadas
    ├── DirectEmissions
    ├── IndirectEmissions
    ├── PrecursorEmissions (opcional)
    └── TotalSpecificEmissions
```

### 6. EmbeddedEmissions

Estrutura das emissões de cada tipo:

```
DirectEmissions / IndirectEmissions
├── DeterminationType    # 01 (real) | 02 (default)
├── MethodologyCode      # TOM01 | TOM02 (opcional)
├── DeterminationDetails # Detalhes textuais (opcional)
├── Justification        # Justificativa para default (opcional)
├── ElectricityFactor    # Apenas para IndirectEmissions
│   ├── SourceCode       # SOE01 | SOE02 | SOE03
│   ├── Value            # Valor do fator
│   └── Unit             # Unidade (tCO2e/MWh)
└── SpecificEmissions
    ├── Value            # Valor numérico
    └── Unit             # tCO2e/t ou tCO2e/MWh
```

---

## Tipos de Dados

### Enumerações

#### DeterminationType

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Código</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>01</code></td><td>Dados reais (medidos/calculados)</td></tr>
    <tr><td><code>02</code></td><td>Valores default (período transitório)</td></tr>
  </tbody>
</table>
</div>

#### RouteCode

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Código</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>BF-BOF</code></td><td>Alto-forno + Convertedor</td></tr>
    <tr><td><code>EAF</code></td><td>Forno elétrico a arco</td></tr>
    <tr><td><code>DRI-EAF</code></td><td>Redução direta + EAF</td></tr>
    <tr><td><code>DRI-BOF</code></td><td>Redução direta + BOF</td></tr>
    <tr><td><code>COREX</code></td><td>Redução por fusão</td></tr>
    <tr><td><code>OTHER</code></td><td>Outra rota</td></tr>
  </tbody>
</table>
</div>

#### MethodologyCode

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Código</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>TOM01</code></td><td>Balanço de massa</td></tr>
    <tr><td><code>TOM02</code></td><td>Monitoramento contínuo (CEMS)</td></tr>
  </tbody>
</table>
</div>

#### ElectricitySourceCode

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Código</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>SOE01</code></td><td>Contrato específico (PPA)</td></tr>
    <tr><td><code>SOE02</code></td><td>Fator médio do grid nacional</td></tr>
    <tr><td><code>SOE03</code></td><td>Outra fonte</td></tr>
  </tbody>
</table>
</div>

#### DatasetStatus

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Valor</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>draft</code></td><td>Rascunho, sujeito a alterações</td></tr>
    <tr><td><code>final</code></td><td>Final, período fechado</td></tr>
  </tbody>
</table>
</div>

---

## Cardinalidade

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Elemento</th><th>Min</th><th>Max</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>CBAMProducerDataPackage</code></td><td>1</td><td>1</td><td>Elemento raiz</td></tr>
    <tr><td><code>Installation</code></td><td>1</td><td>∞</td><td>Pelo menos uma instalação</td></tr>
    <tr><td><code>Product</code></td><td>1</td><td>∞</td><td>Pelo menos um produto por instalação</td></tr>
    <tr><td><code>ConsolidatedSummary</code></td><td>0</td><td>1</td><td>Opcional</td></tr>
    <tr><td><code>PackageMetadata</code></td><td>0</td><td>1</td><td>Opcional</td></tr>
  </tbody>
</table>
</div>

---

## Atributos Especiais

### Campos NON-REGULATORY

```xml
<LegalName regulatory="false" optional="true">...</LegalName>
```

### Campos INFORMATIVE

```xml
<CnCode informative="true" status="to_be_confirmed_by_importer">72083900</CnCode>
```

Os atributos `status` possíveis para códigos não fornecidos:
- `to_be_confirmed_by_importer`
- `not_provided`

---

## Validação

O schema XSD garante:

1. **Tipos de dados** corretos (strings, números, datas)
2. **Enumerações** com valores permitidos
3. **Formatos** (CN Code = 8 dígitos, Country = 2 letras)
4. **Unicidade** de IDs (Installation e Product)
5. **Cardinalidade** mínima e máxima de elementos
