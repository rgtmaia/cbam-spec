---
layout: default
title: "CBAM Producer Data Package Specification"
description: "Especificação técnica pública para troca de dados de emissões no contexto do CBAM europeu."
---

<!-- Quick Start Box -->
<div class="quick-start">
  <div class="quick-start-icon">
    <i class="fas fa-rocket"></i>
  </div>
  <div class="quick-start-content">
    <div class="quick-start-title">Começando?</div>
    <p class="quick-start-desc">Baixe o Schema, veja um exemplo, e valide seu primeiro arquivo XML em minutos.</p>
  </div>
  <div class="quick-start-actions">
    <a href="{{ '/getting-started' | relative_url }}" class="quick-start-link">
      <i class="fas fa-play-circle"></i> Guia Rápido
    </a>
    <a href="{{ '/examples/example-v2-complete.xml' | relative_url }}" class="quick-start-link">
      <i class="fas fa-code"></i> Ver Exemplo
    </a>
  </div>
</div>

<!-- Alert Box -->
<div class="alert">
  <div class="alert-title">
    <i class="fas fa-exclamation-triangle"></i>
    Aviso Legal Importante
  </div>
  <p><strong>Este documento NÃO é um relatório de submissão CBAM (QReport).</strong></p>
  <ul>
    <li>❌ <strong>NÃO pode</strong> ser submetido diretamente ao CBAM Registry da UE</li>
    <li>❌ <strong>NÃO substitui</strong> os formulários oficiais da Comissão Europeia</li>
    <li>❌ <strong>NÃO contém</strong> metodologias de cálculo ou algoritmos proprietários</li>
  </ul>
</div>

## <i class="fas fa-users"></i> Para Quem é Este Formato?

<div class="cards-grid">
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%);">
      <i class="fas fa-industry"></i>
    </div>
    <h3>Produtores</h3>
    <p>Empresas exportadoras que precisam fornecer dados de emissões para seus clientes europeus de forma estruturada e padronizada.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #8b5cf6 0%, #6d28d9 100%);">
      <i class="fas fa-ship"></i>
    </div>
    <h3>Importadores</h3>
    <p>Empresas europeias que precisam receber e validar dados de emissões de seus fornecedores para submissão ao CBAM Registry.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);">
      <i class="fas fa-user-tie"></i>
    </div>
    <h3>Consultores</h3>
    <p>Especialistas em compliance, ESG e regulamentação que assessoram empresas na conformidade com o CBAM.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #ec4899 0%, #be185d 100%);">
      <i class="fas fa-laptop-code"></i>
    </div>
    <h3>Desenvolvedores</h3>
    <p>Equipes técnicas que implementam integrações de sistemas para automatizar a troca de dados de emissões.</p>
  </div>
</div>

---

## <i class="fas fa-book-open"></i> Documentação

<div class="cards-grid">
  <a href="{{ '/docs/concept' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-lightbulb"></i>
    </div>
    <h3>Conceito</h3>
    <p>O que é o CBAM Producer Data Package, seu propósito e contexto regulatório.</p>
  </a>
  
  <a href="{{ '/docs/structure' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-sitemap"></i>
    </div>
    <h3>Estrutura XML</h3>
    <p>Hierarquia do documento, tipos de dados e enumerações disponíveis.</p>
  </a>
  
  <a href="{{ '/docs/lifecycle' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-sync-alt"></i>
    </div>
    <h3>Ciclo de Vida</h3>
    <p>Estados draft → final, versionamento e governança de dados.</p>
  </a>
  
  <a href="{{ '/docs/legal-notices' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-balance-scale"></i>
    </div>
    <h3>Avisos Legais</h3>
    <p>Disclaimers, responsabilidades e limitações do formato.</p>
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
        <div class="download-desc">Schema XML para validação de pacotes · Arquivo principal</div>
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
        <div class="download-name">Exemplo Mínimo</div>
        <div class="download-desc">Estrutura básica com 1 instalação e 1 produto</div>
      </div>
    </div>
    <a href="{{ '/examples/example-v2-minimal.xml' | relative_url }}" class="btn btn-secondary">
      <i class="fas fa-eye"></i> Ver Exemplo
    </a>
  </div>
  
  <div class="download-item">
    <div class="download-info">
      <div class="download-icon" style="background: var(--color-success);">
        <i class="fas fa-file-alt"></i>
      </div>
      <div>
        <div class="download-name">Exemplo Completo</div>
        <div class="download-desc">2 instalações, 3 produtos, todas funcionalidades</div>
      </div>
    </div>
    <a href="{{ '/examples/example-v2-complete.xml' | relative_url }}" class="btn btn-secondary">
      <i class="fas fa-eye"></i> Ver Exemplo
    </a>
  </div>
</div>

### O que o exemplo completo demonstra

<div class="features-list">
  <div class="feature-item"><i class="fas fa-check-circle"></i> 2 instalações (BF-BOF e EAF)</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> 3 produtos diferentes</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> Dados reais e valores default</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> Emissões de precursores</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> Resumo consolidado</div>
  <div class="feature-item"><i class="fas fa-check-circle"></i> Disclaimers PT/EN</div>
</div>

---

## <i class="fas fa-code"></i> Referência no XML

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

### Validação via Terminal

```bash
# Download do Schema
curl -O https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd

# Validar arquivo XML (Linux/Mac)
xmllint --schema cbam-producer-data-package-v2.xsd seu-arquivo.xml --noout

# Validar arquivo XML (Windows com PowerShell)
# Instale xmllint via chocolatey: choco install xsltproc
```

---

## <i class="fas fa-tags"></i> Classificação de Campos

O schema distingue três tipos de campos com responsabilidades diferentes:

<div class="table-wrapper">

| Tipo | Badge | Descrição | Exemplos |
|------|-------|-----------|----------|
| **REGULATORY** | <span class="badge badge-red">🔴 Regulatório</span> | Exigidos pelo EU 2023/956 | `DeterminationType`, `SpecificEmissions` |
| **NON-REGULATORY** | <span class="badge badge-yellow">🟡 Não-Regulatório</span> | Informativos/rastreabilidade | `Description`, `LegalName` |
| **INFORMATIVE** | <span class="badge badge-blue">🔵 Informativo</span> | Responsabilidade do importador | `CnCode`, `HsCode` |

</div>

---

## <i class="fas fa-industry"></i> Setores Cobertos

O CBAM (conforme Anexo I do Regulamento UE 2023/956) cobre os seguintes setores:

<div class="table-wrapper">

| Setor | Produtos Típicos | Códigos CN |
|-------|------------------|------------|
| **Ferro e Aço** | Ferro-gusa, aços carbono, inoxidável | 72xx |
| **Alumínio** | Alumínio primário e ligas | 76xx |
| **Cimento** | Clínquer e cimento Portland | 2523 |
| **Fertilizantes** | Amônia, nitratos, ureia | 2808, 3102 |
| **Hidrogênio** | Hidrogênio | 2804 |
| **Eletricidade** | Eletricidade importada | 2716 |

</div>

---

## <i class="fas fa-gavel"></i> Referências Regulatórias

<div class="table-wrapper">

| Documento | Descrição |
|-----------|-----------|
| [EU 2023/956](https://eur-lex.europa.eu/eli/reg/2023/956) | Regulamento CBAM principal |
| [EU 2023/1773](https://eur-lex.europa.eu/eli/reg_impl/2023/1773) | Regulamento de Implementação |
| [CBAM Registry](https://cbam.ec.europa.eu/) | Portal oficial da Comissão Europeia |
| [Combined Nomenclature](https://taxation-customs.ec.europa.eu/customs-4/calculation-customs-duties/customs-tariff/combined-nomenclature_en) | Códigos CN oficiais |

</div>

---

## <i class="fas fa-file-contract"></i> Licença

**MIT License** - Uso livre para implementação e integração.

Este é um formato aberto destinado a facilitar a comunicação de dados de emissões no contexto do CBAM. 
Sugestões de melhoria são bem-vindas através de [Issues no GitHub]({{ site.github.repository_url }}/issues).
