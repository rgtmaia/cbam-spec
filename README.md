# CBAM Producer Data Package Specification

> **Versão:** 2.0  
> **Última Atualização:** Janeiro 2026  
> **Licença:** MIT

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

## Estrutura do Repositório

```
cbam-spec/
├── README.md                          # Este arquivo
├── docs/
│   ├── concept.md                     # Conceito e propósito do formato
│   ├── structure.md                   # Estrutura do documento XML
│   ├── lifecycle.md                   # Versionamento e ciclo de vida
│   └── legal-notices.md               # Avisos legais e disclaimers
├── schema/
│   └── cbam-producer-data-package-v2.xsd   # Schema XSD público
└── examples/
    ├── example-v2-minimal.xml         # Exemplo mínimo válido
    └── example-v2-complete.xml        # Exemplo completo com múltiplas instalações
```

---

## Documentação

| Documento | Descrição |
|-----------|-----------|
| [Conceito](docs/concept.md) | O que é o CBAM Producer Data Package e seu propósito |
| [Estrutura](docs/structure.md) | Visão geral da estrutura do documento XML |
| [Ciclo de Vida](docs/lifecycle.md) | Versionamento, estados (draft/final) e governança |
| [Avisos Legais](docs/legal-notices.md) | Disclaimers e limitações de responsabilidade |

---

## Uso Rápido

### Validação de um arquivo XML

```bash
# Usando xmllint
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

- **Produtores** de países terceiros que exportam para a UE
- **Importadores** europeus que precisam reportar emissões ao CBAM Registry
- **Consultorias** de compliance e sustentabilidade
- **Desenvolvedores** de sistemas de gestão ambiental e ERPs
- **Auditores** e verificadores de dados de emissões

---

## Setores Cobertos

O CBAM (conforme Anexo I do Regulamento UE 2023/956) cobre os seguintes setores:

| Setor | Produtos Típicos |
|-------|------------------|
| **Ferro e Aço** | Ferro-gusa, aços carbono, inoxidável, ligas |
| **Alumínio** | Alumínio primário e ligas |
| **Cimento** | Clínquer e cimento Portland |
| **Fertilizantes** | Amônia, nitratos, ureia |
| **Hidrogênio** | Hidrogênio (em fases futuras) |
| **Eletricidade** | Eletricidade importada |

---

## Classificação de Campos

O schema distingue claramente três tipos de campos:

### 🔴 REGULATÓRIOS (REGULATORY)
Campos exigidos pelo Regulamento UE 2023/956. São obrigatórios para compliance CBAM.

**Exemplos:** `DeterminationType`, `SpecificEmissions`, `RouteCode`

### 🟡 NÃO-REGULATÓRIOS (NON-REGULATORY)
Campos informativos para legibilidade humana, rastreabilidade ou integração com sistemas.

**Exemplos:** `Description`, `LegalName`, `ConsolidatedSummary`

### 🔵 INFORMATIVOS (INFORMATIVE)
Campos cuja responsabilidade final é do **importador**, não do produtor.

**Exemplos:** `CnCode`, `HsCode` (códigos aduaneiros)

---

## Exemplos

### Exemplo Mínimo

```xml
<CBAMProducerDataPackage 
    xmlns="https://cbam-spec.github.io/schema/package/v2"
    version="2.0" schemaVersion="2.0.0">
  
  <DatasetIdentification>
    <DatasetId>uuid-aqui</DatasetId>
    <Version>1.0</Version>
    <GenerationDate>2026-01-15</GenerationDate>
  </DatasetIdentification>
  
  <ReportingPeriod>
    <Year>2026</Year>
    <Quarter>1</Quarter>
    <PeriodId>2026-Q1</PeriodId>
  </ReportingPeriod>
  
  <Operator>
    <OperatorId>IDENTIFICADOR</OperatorId>
    <OperatorName>Nome da Empresa</OperatorName>
    <Address><Country>BR</Country></Address>
  </Operator>
  
  <Installations count="1">
    <Installation index="1">
      <!-- ... dados da instalação ... -->
    </Installation>
  </Installations>
  
</CBAMProducerDataPackage>
```

Veja exemplos completos em [examples/](examples/).

---

## Referências Regulatórias

| Documento | Descrição |
|-----------|-----------|
| [EU 2023/956](https://eur-lex.europa.eu/eli/reg/2023/956) | Regulamento CBAM principal |
| [EU 2023/1773](https://eur-lex.europa.eu/eli/reg_impl/2023/1773) | Regulamento de Implementação |
| [CBAM Registry](https://cbam.ec.europa.eu/) | Portal oficial da Comissão Europeia |

---

## Contribuições

Este é um formato aberto destinado a facilitar a comunicação de dados de emissões no contexto do CBAM. Sugestões de melhoria são bem-vindas através de Issues.

---

## Licença

MIT License - Uso livre para implementação e integração.

---

**Nota:** Este repositório contém apenas a especificação do formato de dados. Implementações específicas, ferramentas de cálculo e sistemas são mantidos separadamente.

