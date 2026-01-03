---
layout: docs
title: "Ciclo de Vida e Versionamento"
page_title: "Ciclo de Vida"
breadcrumb: "Ciclo de Vida"
description: "Como funciona o ciclo de vida do CBAM Producer Data Package, incluindo estados draft/final, versionamento e governança de dados."
prev_page:
  url: /docs/structure
  title: "Estrutura XML"
next_page:
  url: /docs/legal-notices
  title: "Avisos Legais"
---

Este documento descreve o ciclo de vida de um CBAM Producer Data Package, incluindo estados, versionamento e governança dos dados.

---

## Estados do Dataset

O campo `DatasetStatus` indica o estado atual do pacote de dados:

<div class="cards-grid" style="margin: 1.5rem 0;">
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);">
      <i class="fas fa-pencil-alt"></i>
    </div>
    <h3>Draft (Rascunho)</h3>
    <p><strong>Mutável.</strong> O período ainda não foi fechado. Dados podem ser alterados, recalculados ou corrigidos.</p>
  </div>
  
  <div class="card">
    <div class="card-icon" style="background: linear-gradient(135deg, #22c55e 0%, #15803d 100%);">
      <i class="fas fa-check-circle"></i>
    </div>
    <h3>Final</h3>
    <p><strong>Imutável.</strong> O período foi oficialmente fechado. Representa a versão oficial para o período.</p>
  </div>
</div>

### Draft (Rascunho)

- O período de reporte ainda não foi fechado
- Dados podem ser alterados, recalculados ou corrigidos
- Novas versões podem ser geradas
- **Uso:** Compartilhamento preliminar, revisões internas

### Final (Final)

- O período de reporte foi oficialmente fechado
- Dados são considerados **imutáveis**
- Representa a versão oficial para o período
- **Uso:** Submissão ao importador para relatório CBAM

---

## Versionamento

O pacote utiliza dois níveis de versionamento:

### 1. Versão do Schema (`@schemaVersion`)

Indica a versão do formato/estrutura XML. Segue versionamento semântico:

```
X.Y.Z
│ │ │
│ │ └── Patch: correções, melhorias de documentação
│ └──── Minor: novos campos opcionais, retrocompatível
└────── Major: mudanças estruturais incompatíveis
```

**Exemplo:** `2.0.0`

### 2. Versão do Dataset (`DatasetIdentification.Version`)

Indica a revisão dos dados para um mesmo período:

<div class="table-wrapper">

| Versão | Significado |
|--------|-------------|
| `1.0` | Geração inicial |
| `1.1` | Correção de dados de entrada |
| `2.0` | Recálculo completo com nova metodologia |

</div>

---

## Ciclo de Vida Típico

<div class="info-box">
  <div class="info-box-title">
    <i class="fas fa-sync-alt"></i> Fluxo do Ciclo de Vida
  </div>
  <p><strong>Entrada de dados</strong> (draft v1.0) → <strong>Cálculo/Verificação</strong> (draft v1.x) → <strong>Período Fechado</strong> (final v1.x) → <strong>Envio ao Importador</strong> (final v1.x)</p>
</div>

---

## Eventos de Versionamento

### Quando Incrementar a Versão

<div class="table-wrapper">

| Evento | Ação |
|--------|------|
| Correção de dados de entrada (ex: quantidade) | Minor increment (1.0 → 1.1) |
| Recálculo de emissões | Minor increment (1.1 → 1.2) |
| Mudança de metodologia | Major increment (1.x → 2.0) |
| Fechamento do período | Não incrementa (apenas muda status) |

</div>

### Imutabilidade do Final

Uma vez que o status muda para `final`:

- ❌ Não é possível alterar dados
- ❌ Não é possível gerar nova versão para o mesmo período
- ✅ O pacote pode ser exportado múltiplas vezes (mesmo conteúdo)

---

## Identificação Única

### DatasetId

Identificador único global do pacote. Recomenda-se usar **UUID v4**:

```xml
<DatasetId>550e8400-e29b-41d4-a716-446655440000</DatasetId>
```

**Características:**
- Permanece o mesmo entre versões do mesmo dataset
- Permite rastreabilidade entre produtor e importador
- Vinculação com documentos de suporte (notas fiscais, certificados)

### PeriodId

Identificador legível do período de reporte:

```xml
<PeriodId>2026-Q1</PeriodId>
```

**Formato:** `YYYY-QN` onde N é o trimestre (1-4)

---

## Integridade dos Dados

### Hash de Integridade

O campo `IntegrityHash` (em PackageMetadata) permite verificar que o pacote não foi alterado:

```xml
<IntegrityHash>sha256:a3f8c2d1e5b9f7a2c4d6e8f0a1b3c5d7e9f1a2b4c6d8e0f2a4b6c8d0e2f4a6b8</IntegrityHash>
```

**Uso:**
- Validação de que o arquivo não foi corrompido em trânsito
- Auditoria e rastreabilidade
- Prova de que dados não foram alterados após fechamento

---

## Fluxo de Dados

<div class="info-box">
  <div class="info-box-title">
    <i class="fas fa-exchange-alt"></i> Comunicação Produtor ↔ Importador
  </div>
  <div style="font-family: monospace; font-size: 0.875rem; line-height: 1.8;">
    PRODUTOR → Gera v1.0 (draft) → IMPORTADOR<br>
    PRODUTOR ← Solicitação de correção ← IMPORTADOR<br>
    PRODUTOR → Gera v1.1 (draft) → IMPORTADOR<br>
    PRODUTOR → Fecha período: v1.1 (final) → IMPORTADOR<br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↓<br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CBAM REGISTRY
  </div>
</div>

---

## Boas Práticas

### Para Produtores

1. **Mantenha histórico** de todas as versões geradas
2. **Documente** as razões de cada nova versão
3. **Feche o período** apenas quando os dados estiverem verificados
4. **Inclua justificativas** para uso de valores default

### Para Importadores

1. **Valide** o pacote contra o schema antes de processar
2. **Verifique** a integridade usando o hash (quando disponível)
3. **Confirme** o status do pacote (preferir `final`)
4. **Arquive** os pacotes recebidos para auditoria

---

## Governança

### Quem Pode Gerar Pacotes

- Apenas sistemas autorizados pelo operador (produtor)
- Identificados pelo campo `PackageMetadata.GeneratingSoftware`

### Rastreabilidade

Cada pacote inclui metadados para auditoria:

<div class="table-wrapper">

| Campo | Descrição |
|-------|-----------|
| `GeneratingSoftware.Name` | Nome do sistema gerador |
| `GeneratingSoftware.Version` | Versão do sistema |
| `GeneratedAt` | Timestamp de geração |
| `ClosedAt` | Timestamp de fechamento (se final) |

</div>

### Retenção

Recomenda-se manter os pacotes arquivados por pelo menos:

- **5 anos** para fins de auditoria CBAM
- **Conforme legislação local** para fins tributários e comerciais
