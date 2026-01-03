---
layout: default
title: "Estrutura do CBAM Producer Data Package"
description: "Documentação detalhada da estrutura XML do CBAM Producer Data Package, incluindo hierarquia, tipos de dados e enumerações."
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

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `DatasetId` | UUID | Identificador global único |
| `Version` | String | Versão do dataset (ex: "1.0", "1.1") |
| `GenerationDate` | Date | Data de geração (YYYY-MM-DD) |
| `DatasetStatus` | Enum | `draft` ou `final` |

### 2. ReportingPeriod

Define o trimestre de referência dos dados.

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `Year` | gYear | Ano de referência |
| `Quarter` | 1-4 | Trimestre (Q1, Q2, Q3, Q4) |
| `PeriodId` | String | Identificador legível (ex: "2026-Q1") |
| `SubmissionDeadline` | Date | Prazo para submissão CBAM |

### 3. Operator

Informações sobre a empresa produtora.

| Campo | Classificação | Descrição |
|-------|---------------|-----------|
| `OperatorId` | REGULATORY | CNPJ (Brasil), CIN (Índia), etc. |
| `OperatorName` | REGULATORY | Nome comercial |
| `LegalName` | NON-REGULATORY | Razão social |
| `Address.Country` | REGULATORY | País (ISO 3166-1) |

### 4. Installation

Dados de cada planta produtora.

| Campo | Classificação | Descrição |
|-------|---------------|-----------|
| `InstallationId` | REGULATORY | Identificador único da instalação |
| `InstallationName` | REGULATORY | Nome da instalação |
| `ProductionProcess` | REGULATORY | Rota e metodologia de produção |

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
| Código | Descrição |
|--------|-----------|
| `01` | Dados reais (medidos/calculados) |
| `02` | Valores default (período transitório) |

#### RouteCode
| Código | Descrição |
|--------|-----------|
| `BF-BOF` | Alto-forno + Convertedor |
| `EAF` | Forno elétrico a arco |
| `DRI-EAF` | Redução direta + EAF |
| `DRI-BOF` | Redução direta + BOF |
| `COREX` | Redução por fusão |
| `OTHER` | Outra rota |

#### MethodologyCode
| Código | Descrição |
|--------|-----------|
| `TOM01` | Balanço de massa |
| `TOM02` | Monitoramento contínuo (CEMS) |

#### ElectricitySourceCode
| Código | Descrição |
|--------|-----------|
| `SOE01` | Contrato específico (PPA) |
| `SOE02` | Fator médio do grid nacional |
| `SOE03` | Outra fonte |

#### DatasetStatus
| Valor | Descrição |
|-------|-----------|
| `draft` | Rascunho, sujeito a alterações |
| `final` | Final, período fechado |

---

## Cardinalidade

| Elemento | Min | Max | Descrição |
|----------|-----|-----|-----------|
| `CBAMProducerDataPackage` | 1 | 1 | Elemento raiz |
| `Installation` | 1 | ∞ | Pelo menos uma instalação |
| `Product` | 1 | ∞ | Pelo menos um produto por instalação |
| `ConsolidatedSummary` | 0 | 1 | Opcional |
| `PackageMetadata` | 0 | 1 | Opcional |

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

