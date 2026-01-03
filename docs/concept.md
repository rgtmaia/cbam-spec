---
layout: docs
title: "Conceito do CBAM Producer Data Package"
page_title: "Conceito"
breadcrumb: "Conceito"
description: "Entenda o que é o CBAM Producer Data Package, seu propósito e como ele se encaixa no contexto regulatório europeu."
prev_page:
  url: /getting-started
  title: "Começar"
next_page:
  url: /docs/structure
  title: "Estrutura XML"
---

## O que é o CBAM?

O **Carbon Border Adjustment Mechanism** (CBAM) é um instrumento regulatório da União Europeia estabelecido pelo Regulamento (UE) 2023/956, que entrou em vigor em outubro de 2023. Seu objetivo é:

1. Evitar a "fuga de carbono" (relocação de produção industrial para países com menores restrições ambientais)
2. Nivelar condições de competição entre produtores europeus (sujeitos ao EU ETS) e importadores
3. Incentivar a descarbonização global da produção industrial

---

## O que é o CBAM Producer Data Package?

O **CBAM Producer Data Package** é um formato de dados estruturado que permite a comunicação padronizada de informações de emissões entre:

- **Produtores** localizados em países terceiros (não-UE)
- **Importadores** europeus que compram e importam esses produtos

### Propósito

<div class="info-box">
  <div class="info-box-title">
    <i class="fas fa-info-circle"></i> Cadeia de Dados CBAM
  </div>
  <p><strong>PRODUTOR</strong> → gera <strong>Producer Data Package</strong> → enviado para <strong>IMPORTADOR</strong> → que submete <strong>QReport</strong> ao <strong>CBAM Registry</strong></p>
</div>

O formato define a estrutura de dados que permite que produtores forneçam informações de emissões de forma padronizada para que importadores possam:

1. **Validar** a consistência dos dados recebidos
2. **Converter** para o formato oficial do CBAM Registry
3. **Submeter** relatórios trimestrais (QReport) às autoridades

---

## Escopo Regulatório vs. Não-Regulatório

### Campos Regulatórios

São campos diretamente exigidos pelo Regulamento EU 2023/956 e seus regulamentos de implementação. Exemplos:

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Campo</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>DeterminationType</code></td><td>Se os dados são reais (01) ou default (02)</td></tr>
    <tr><td><code>SpecificEmissions</code></td><td>Emissões específicas em tCO2e por tonelada</td></tr>
    <tr><td><code>RouteCode</code></td><td>Rota produtiva (BF-BOF, EAF, etc.)</td></tr>
    <tr><td><code>MethodologyCode</code></td><td>Metodologia de cálculo (TOM01, TOM02)</td></tr>
  </tbody>
</table>
</div>

### Campos Não-Regulatórios

Campos informativos para facilitar a leitura humana, rastreabilidade ou integração:

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Campo</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>Description</code></td><td>Descrição textual do produto</td></tr>
    <tr><td><code>LegalName</code></td><td>Razão social da empresa</td></tr>
    <tr><td><code>ConsolidatedSummary</code></td><td>Resumo agregado (apenas informativo)</td></tr>
    <tr><td><code>PackageMetadata</code></td><td>Metadados de geração do pacote</td></tr>
  </tbody>
</table>
</div>

### Campos Informativos

Campos cuja responsabilidade final de classificação é do **importador**:

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Campo</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td><code>CnCode</code></td><td>Código da Nomenclatura Combinada (8 dígitos)</td></tr>
    <tr><td><code>HsCode</code></td><td>Código do Sistema Harmonizado (6 dígitos)</td></tr>
  </tbody>
</table>
</div>

<div class="warning-box">
  <div class="warning-box-title">
    <i class="fas fa-exclamation-triangle"></i> Importante
  </div>
  <p>O produtor fornece sua melhor estimativa, mas a <strong>responsabilidade legal pela classificação aduaneira correta é do importador</strong>.</p>
</div>

---

## O que o Produtor Fornece

O produtor é responsável por informar:

1. **Identificação da empresa** (operador)
2. **Dados das instalações** (plantas produtoras)
3. **Produtos fabricados** e suas quantidades
4. **Emissões incorporadas**:
   - Emissões diretas (Scope 1)
   - Emissões indiretas (Scope 2, consumo de eletricidade)
   - Emissões de precursores (quando aplicável)
5. **Metodologia utilizada** para determinação das emissões

---

## O que o Importador Faz

O importador europeu recebe o pacote de dados e:

1. **Valida** a consistência e completude dos dados
2. **Confirma** a classificação aduaneira (códigos CN/HS)
3. **Converte** os dados para o formato do CBAM Registry
4. **Submete** o relatório trimestral (QReport) à autoridade competente
5. **Adquire** os certificados CBAM correspondentes às emissões

---

## Tipos de Emissões

O CBAM considera três categorias de emissões incorporadas:

<div class="cards-grid" style="margin: 1.5rem 0;">
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #ef4444 0%, #b91c1c 100%);">
      <i class="fas fa-fire"></i>
    </div>
    <h3>Emissões Diretas</h3>
    <p><strong>Scope 1:</strong> Queima de combustíveis, reações químicas, processos industriais.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);">
      <i class="fas fa-bolt"></i>
    </div>
    <h3>Emissões Indiretas</h3>
    <p><strong>Scope 2:</strong> Consumo de eletricidade da rede.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #8b5cf6 0%, #6d28d9 100%);">
      <i class="fas fa-cubes"></i>
    </div>
    <h3>Precursores</h3>
    <p>Emissões de materiais de entrada que são produtos CBAM (ex: ferro-gusa usado em aço).</p>
  </div>
</div>

### Emissões Específicas

O CBAM utiliza primariamente **emissões específicas** (por unidade de produto):

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Unidade</th><th>Uso</th></tr>
  </thead>
  <tbody>
    <tr><td><code>tCO2e/t</code></td><td>Toneladas de CO2eq por tonelada de produto</td></tr>
    <tr><td><code>tCO2e/MWh</code></td><td>Para eletricidade</td></tr>
  </tbody>
</table>
</div>

---

## Período de Reporte

O CBAM opera em ciclos trimestrais:

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Trimestre</th><th>Período</th><th>Deadline de Submissão</th></tr>
  </thead>
  <tbody>
    <tr><td>Q1</td><td>Janeiro - Março</td><td>30 de Abril</td></tr>
    <tr><td>Q2</td><td>Abril - Junho</td><td>31 de Julho</td></tr>
    <tr><td>Q3</td><td>Julho - Setembro</td><td>31 de Outubro</td></tr>
    <tr><td>Q4</td><td>Outubro - Dezembro</td><td>31 de Janeiro (ano seguinte)</td></tr>
  </tbody>
</table>
</div>

---

## Referências

- [Regulamento EU 2023/956 (CBAM)](https://eur-lex.europa.eu/eli/reg/2023/956)
- [Regulamento de Implementação EU 2023/1773](https://eur-lex.europa.eu/eli/reg_impl/2023/1773)
- [Portal CBAM da Comissão Europeia](https://cbam.ec.europa.eu/)
