---
layout: docs
title: "Ciclo de Vida do Dataset"
page_title: "Ciclo de Vida"
breadcrumb: "Ciclo de Vida"
description: "Como um CBAM Producer Data Package é criado, versionado, transmitido e arquivado ao longo do tempo."
prev_page:
  url: /docs/structure
  title: "Estrutura XML"
next_page:
  url: /docs/legal-notices
  title: "Avisos Legais"
---

Este documento descreve o ciclo de vida completo de um CBAM Producer Data Package, desde sua criação até o arquivamento.

---

## Visão Geral

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   CRIAÇÃO   │───►│  REVISÃO    │───►│ TRANSMISSÃO │───►│ ARQUIVAMENTO│
│   (draft)   │    │  (draft)    │    │   (final)   │    │   (final)   │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
     │                   │                   │                   │
     ▼                   ▼                   ▼                   ▼
  Dataset v1.0       Dataset v1.x       Dataset final      Retenção 10a
```

---

## Estados do Dataset

### DatasetStatus

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Status</th><th>Descrição</th><th>Editável</th></tr>
  </thead>
  <tbody>
    <tr><td><code>draft</code></td><td>Em elaboração, sujeito a alterações</td><td>✅ Sim</td></tr>
    <tr><td><code>final</code></td><td>Fechado, apenas para referência</td><td>❌ Não</td></tr>
  </tbody>
</table>
</div>

### Transição de Estados

```
          ┌──────────────┐
          │    DRAFT     │◄────────────────┐
          └──────┬───────┘                 │
                 │                         │
        [revisão]│                         │
                 │                         │
                 ▼                         │
          ┌──────────────┐                 │
          │    DRAFT     │────────────────►│ (nova versão)
          │   (v1.x)     │                 │
          └──────┬───────┘                 │
                 │                         │
       [fechamento]                        │
                 │                         │
                 ▼                         │
          ┌──────────────┐                 │
          │    FINAL     │ ───────────────►│ (correção pós-fechamento)
          │   (vN.0)     │                 │
          └──────────────┘                 │
```

---

## Versionamento

### Regras de Versão

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Tipo de Alteração</th><th>Versão</th><th>Exemplo</th></tr>
  </thead>
  <tbody>
    <tr><td>Criação inicial</td><td><code>1.0</code></td><td>Primeiro dataset do período</td></tr>
    <tr><td>Revisão em draft</td><td><code>1.x</code></td><td>1.1, 1.2, 1.3...</td></tr>
    <tr><td>Correção pós-final</td><td><code>N.0</code></td><td>2.0, 3.0 (substitui anterior)</td></tr>
  </tbody>
</table>
</div>

### Campos de Versionamento

```xml
<DatasetIdentification>
  <DatasetId>550e8400-e29b-41d4-a716-446655440000</DatasetId>
  <Version>1.2</Version>
  <GenerationDate>2026-03-15</GenerationDate>
  <DatasetStatus>draft</DatasetStatus>
</DatasetIdentification>
```

### Histórico de Versões

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

## Fluxo de Dados

### Atores

```
┌──────────────┐        ┌──────────────┐        ┌──────────────┐
│   PRODUTOR   │        │  IMPORTADOR  │        │   COMISSÃO   │
│   (3º país)  │        │     (UE)     │        │   EUROPEIA   │
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

### Responsabilidades

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Ator</th><th>Responsabilidade</th></tr>
  </thead>
  <tbody>
    <tr><td><strong>Produtor</strong></td><td>Gerar XML com dados de emissão</td></tr>
    <tr><td><strong>Importador</strong></td><td>Validar e complementar dados (CN/HS codes)</td></tr>
    <tr><td><strong>Importador</strong></td><td>Submeter relatório CBAM ao registro transitório</td></tr>
    <tr><td><strong>Comissão</strong></td><td>Verificar e processar declarações</td></tr>
  </tbody>
</table>
</div>

---

## Trimestres de Referência

### Prazos CBAM (Período Transitório)

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Trimestre</th><th>Período</th><th>Deadline</th></tr>
  </thead>
  <tbody>
    <tr><td>Q1</td><td>Jan–Mar</td><td>30 de Abril</td></tr>
    <tr><td>Q2</td><td>Abr–Jun</td><td>31 de Julho</td></tr>
    <tr><td>Q3</td><td>Jul–Set</td><td>31 de Outubro</td></tr>
    <tr><td>Q4</td><td>Out–Dez</td><td>31 de Janeiro (ano seguinte)</td></tr>
  </tbody>
</table>
</div>

### Exemplo de ReportingPeriod

```xml
<ReportingPeriod>
  <Year>2026</Year>
  <Quarter>1</Quarter>
  <PeriodId>2026-Q1</PeriodId>
  <SubmissionDeadline>2026-04-30</SubmissionDeadline>
</ReportingPeriod>
```

---

## Correções e Retificações

### Antes do Fechamento (draft)

1. Criar nova versão do dataset (`Version` +0.1)
2. Atualizar `GenerationDate`
3. Manter mesmo `DatasetId`
4. Atualizar `VersionHistory`

### Após o Fechamento (final)

1. Criar **novo** dataset com `Version` +1.0
2. Gerar **novo** `DatasetId`
3. Referenciar dataset anterior em `PreviousVersion`
4. Marcar como `draft` até aprovação do importador

---

## Arquivamento

### Requisitos

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Aspecto</th><th>Requisito</th></tr>
  </thead>
  <tbody>
    <tr><td><strong>Retenção</strong></td><td>Mínimo 10 anos após geração</td></tr>
    <tr><td><strong>Integridade</strong></td><td>Hash SHA-256 do arquivo XML</td></tr>
    <tr><td><strong>Rastreabilidade</strong></td><td>Histórico de versões preservado</td></tr>
    <tr><td><strong>Acessibilidade</strong></td><td>Disponível para auditorias</td></tr>
  </tbody>
</table>
</div>

### Metadados de Arquivamento

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

## Exemplo Completo

### Cenário

1. Produtor cria dataset Q1/2026 em 10/Mar
2. Revisão em 20/Mar após verificação interna
3. Envio ao importador em 25/Mar
4. Importador complementa e fecha em 15/Abr
5. Arquivamento para auditoria

### Evolução do Dataset

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Etapa</th><th>Versão</th><th>Status</th><th>Data</th></tr>
  </thead>
  <tbody>
    <tr><td>Criação</td><td>1.0</td><td>draft</td><td>2026-03-10</td></tr>
    <tr><td>Revisão</td><td>1.1</td><td>draft</td><td>2026-03-20</td></tr>
    <tr><td>Envio</td><td>1.1</td><td>draft</td><td>2026-03-25</td></tr>
    <tr><td>Fechamento</td><td>1.1</td><td>final</td><td>2026-04-15</td></tr>
    <tr><td>Arquivamento</td><td>1.1</td><td>final</td><td>2026-04-15</td></tr>
  </tbody>
</table>
</div>
