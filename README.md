---
title: "CBAM Producer Data Package Specification"
description: "Especificação técnica pública do formato de troca de dados de emissões entre produtores de países terceiros e importadores europeus no contexto do CBAM (Carbon Border Adjustment Mechanism)."
keywords: "CBAM, Carbon Border Adjustment Mechanism, emissions data, EU regulation, XML schema, producer data package, embedded emissions, carbon footprint, international trade"
lang: pt-BR
---

# CBAM Producer Data Package Specification

> **Versão:** 2.0  
> **Última Atualização:** Janeiro 2026  
> **Licença:** MIT

---

## 📑 Sumário

- [Sobre](#sobre)
- [Aviso Legal](#️-aviso-legal-importante)
- [Contexto Regulatório](#contexto-regulatório)
- [Recursos Rápidos](#-recursos-rápidos)
- [Documentação](#-documentação)
- [Uso Rápido](#uso-rápido)
- [Público-Alvo](#público-alvo)
- [Setores Cobertos](#setores-cobertos)
- [Classificação de Campos](#classificação-de-campos)
- [Exemplos](#exemplos)
- [Referências Regulatórias](#referências-regulatórias)
- [Contribuições](#contribuições)
- [Licença](#licença)

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

## 🔗 Recursos Rápidos

| Recurso | Link Direto | Descrição |
|---------|-------------|-----------|
| 📐 **Schema XSD** | [cbam-producer-data-package-v2.xsd](schema/cbam-producer-data-package-v2.xsd) | Schema XML para validação |
| 📄 **Exemplo Mínimo** | [example-v2-minimal.xml](examples/example-v2-minimal.xml) | Estrutura básica válida |
| 📄 **Exemplo Completo** | [example-v2-complete.xml](examples/example-v2-complete.xml) | Múltiplas instalações e produtos |

### Download Direto

```bash
# Schema XSD
curl -O https://raw.githubusercontent.com/SEU-USUARIO/cbam-spec/main/schema/cbam-producer-data-package-v2.xsd

# Exemplo Mínimo
curl -O https://raw.githubusercontent.com/SEU-USUARIO/cbam-spec/main/examples/example-v2-minimal.xml

# Exemplo Completo
curl -O https://raw.githubusercontent.com/SEU-USUARIO/cbam-spec/main/examples/example-v2-complete.xml
```

---

## 📚 Documentação

| Documento | Descrição |
|-----------|-----------|
| 📘 [Conceito](docs/concept.md) | O que é o CBAM Producer Data Package e seu propósito |
| 🏗️ [Estrutura](docs/structure.md) | Visão geral da estrutura do documento XML |
| 🔄 [Ciclo de Vida](docs/lifecycle.md) | Versionamento, estados (draft/final) e governança |
| ⚖️ [Avisos Legais](docs/legal-notices.md) | Disclaimers e limitações de responsabilidade |

### Estrutura do Repositório

```
cbam-spec/
├── README.md                                    # Este arquivo
├── docs/
│   ├── concept.md                               # Conceito e propósito
│   ├── structure.md                             # Estrutura do XML
│   ├── lifecycle.md                             # Versionamento
│   └── legal-notices.md                         # Avisos legais
├── schema/
│   └── cbam-producer-data-package-v2.xsd        # Schema XSD
└── examples/
    ├── example-v2-minimal.xml                   # Exemplo mínimo
    └── example-v2-complete.xml                  # Exemplo completo
```

---

## Uso Rápido

### Validação de um arquivo XML

```bash
# Usando xmllint (Linux/macOS/WSL)
xmllint --schema schema/cbam-producer-data-package-v2.xsd seu-arquivo.xml --noout

# Usando xmllint (Windows com Chocolatey)
choco install libxml2
xmllint --schema schema/cbam-producer-data-package-v2.xsd seu-arquivo.xml --noout
```

### Namespace e Atributos

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CBAMProducerDataPackage 
    xmlns="https://cbam-spec.github.io/schema/package/v2"
    version="2.0"
    schemaVersion="2.0.0">
  <!-- conteúdo -->
</CBAMProducerDataPackage>
```

---

## Público-Alvo

- 🏭 **Produtores** de países terceiros que exportam para a UE
- 🚢 **Importadores** europeus que precisam reportar emissões ao CBAM Registry
- 📊 **Consultorias** de compliance e sustentabilidade
- 💻 **Desenvolvedores** de sistemas de gestão ambiental e ERPs
- 🔍 **Auditores** e verificadores de dados de emissões

---

## Setores Cobertos

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

## Classificação de Campos

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

➡️ Veja detalhes em [docs/structure.md](docs/structure.md)

---

## Exemplos

### Exemplo Mínimo

📄 **Arquivo:** [examples/example-v2-minimal.xml](examples/example-v2-minimal.xml)

```xml
<CBAMProducerDataPackage 
    xmlns="https://cbam-spec.github.io/schema/package/v2"
    version="2.0" schemaVersion="2.0.0">
  
  <DatasetIdentification>
    <DatasetId>a1b2c3d4-e5f6-7890-abcd-ef1234567890</DatasetId>
    <Version>1.0</Version>
    <GenerationDate>2026-01-15</GenerationDate>
  </DatasetIdentification>
  
  <ReportingPeriod>
    <Year>2026</Year>
    <Quarter>1</Quarter>
    <PeriodId>2026-Q1</PeriodId>
  </ReportingPeriod>
  
  <Operator>
    <OperatorId>00.000.000/0001-00</OperatorId>
    <OperatorName>Exemplo Metalúrgica S.A.</OperatorName>
    <Address><Country>BR</Country></Address>
  </Operator>
  
  <Installations count="1">
    <Installation index="1">
      <!-- ... dados da instalação ... -->
    </Installation>
  </Installations>
  
</CBAMProducerDataPackage>
```

### Exemplo Completo

📄 **Arquivo:** [examples/example-v2-complete.xml](examples/example-v2-complete.xml)

Inclui:
- 2 instalações (BF-BOF e EAF)
- 3 produtos
- Uso de dados reais e valores default
- Emissões de precursores
- Resumo consolidado
- Disclaimers legais em PT/EN

---

## Referências Regulatórias

| Documento | Descrição |
|-----------|-----------|
| 📜 [EU 2023/956](https://eur-lex.europa.eu/eli/reg/2023/956) | Regulamento CBAM principal |
| 📜 [EU 2023/1773](https://eur-lex.europa.eu/eli/reg_impl/2023/1773) | Regulamento de Implementação |
| 🌐 [CBAM Registry](https://cbam.ec.europa.eu/) | Portal oficial da Comissão Europeia |
| 📋 [Combined Nomenclature](https://taxation-customs.ec.europa.eu/customs-4/calculation-customs-duties/customs-tariff/combined-nomenclature_en) | Códigos CN oficiais |

---

## Contribuições

Este é um formato aberto destinado a facilitar a comunicação de dados de emissões no contexto do CBAM. Sugestões de melhoria são bem-vindas através de Issues.

### Como Contribuir

1. Abra uma **Issue** para reportar problemas ou sugerir melhorias
2. Faça um **Fork** e submeta um **Pull Request** para alterações
3. Siga as convenções de nomenclatura e documentação existentes

---

## Licença

MIT License - Uso livre para implementação e integração.

---

<p align="center">
  <strong>CBAM Producer Data Package Specification</strong><br>
  <em>Facilitando a comunicação de dados de emissões no contexto do CBAM</em>
</p>

---

**Nota:** Este repositório contém apenas a especificação do formato de dados. Implementações específicas, ferramentas de cálculo e sistemas são mantidos separadamente.
