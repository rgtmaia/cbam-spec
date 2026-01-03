---
layout: default
title: "CBAM Producer Data Package Specification"
description: "CBAM Producer Data Package Specification - open technical standard for emissions data exchange under EU CBAM regulation between third-country producers and European importers."
---

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
| [🏗️ Estrutura XML](docs/structure.md) | Hierarquia e tipos de dados |
| [🔄 Versionamento](docs/lifecycle.md) | Ciclo de vida draft → final |
| [⚖️ Avisos Legais](docs/legal-notices.md) | Disclaimers e limitações |

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

O formato serve exclusivamente como **contrato de dados** entre produtores e importadores.

---

## 📥 Download do Schema (XSD)

| Arquivo | URL Pública |
|---------|-------------|
| **Schema XSD v2** | [cbam-producer-data-package-v2.xsd](schema/cbam-producer-data-package-v2.xsd) |

```bash
# Download do Schema XSD
curl -O https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd
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

| Exemplo | Descrição | Link |
|---------|-----------|------|
| **Mínimo** | Estrutura básica com 1 instalação e 1 produto | [example-v2-minimal.xml](examples/example-v2-minimal.xml) |
| **Completo** | 2 instalações, 3 produtos, todas funcionalidades | [example-v2-complete.xml](examples/example-v2-complete.xml) |

### O que o exemplo completo demonstra:

- ✅ 2 instalações com rotas diferentes (BF-BOF e EAF)
- ✅ 3 produtos com diferentes características
- ✅ Uso de dados reais (`DeterminationType: 01`) e valores default (`02`)
- ✅ Emissões de precursores
- ✅ Resumo consolidado
- ✅ Disclaimers legais em PT e EN

---

## 📚 Documentação

| Documento | Descrição |
|-----------|-----------|
| [📘 Conceito](docs/concept.md) | O que é o CBAM Producer Data Package e seu propósito |
| [🏗️ Estrutura](docs/structure.md) | Visão geral da estrutura do documento XML |
| [🔄 Ciclo de Vida](docs/lifecycle.md) | Versionamento, estados (draft/final) e governança |
| [⚖️ Avisos Legais](docs/legal-notices.md) | Disclaimers e limitações de responsabilidade |

---

## 🏷️ Classificação de Campos

O schema distingue três tipos de campos:

| Tipo | Cor | Descrição | Exemplos |
|------|-----|-----------|----------|
| **REGULATORY** | 🔴 | Exigidos pelo EU 2023/956 | `DeterminationType`, `SpecificEmissions` |
| **NON-REGULATORY** | 🟡 | Informativos/rastreabilidade | `Description`, `LegalName` |
| **INFORMATIVE** | 🔵 | Responsabilidade do importador | `CnCode`, `HsCode` |

---

## 🏭 Setores Cobertos

| Setor | Produtos Típicos | Códigos CN |
|-------|------------------|------------|
| **Ferro e Aço** | Ferro-gusa, aços carbono, inoxidável | 72xx |
| **Alumínio** | Alumínio primário e ligas | 76xx |
| **Cimento** | Clínquer e cimento Portland | 2523 |
| **Fertilizantes** | Amônia, nitratos, ureia | 2808, 3102 |
| **Hidrogênio** | Hidrogênio | 2804 |
| **Eletricidade** | Eletricidade importada | 2716 |

---

## 📜 Referências Regulatórias

| Documento | Descrição |
|-----------|-----------|
| [EU 2023/956](https://eur-lex.europa.eu/eli/reg/2023/956) | Regulamento CBAM principal |
| [EU 2023/1773](https://eur-lex.europa.eu/eli/reg_impl/2023/1773) | Regulamento de Implementação |
| [CBAM Registry](https://cbam.ec.europa.eu/) | Portal oficial da Comissão Europeia |

---

## 📄 Licença

MIT License - Uso livre para implementação e integração.

---

<p align="center">
  <strong>CBAM Producer Data Package Specification v2.0</strong><br>
  <em>Facilitando a comunicação de dados de emissões no contexto do CBAM</em><br><br>
  <a href="schema/cbam-producer-data-package-v2.xsd">📥 Download XSD</a> •
  <a href="docs/concept.md">📘 Documentação</a> •
  <a href="examples/example-v2-complete.xml">📄 Exemplo</a>
</p>

