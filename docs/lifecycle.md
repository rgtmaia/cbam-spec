---
title: "Ciclo de Vida e Versionamento"
description: "Como funciona o ciclo de vida do CBAM Producer Data Package, incluindo estados draft/final, versionamento e governança de dados."
---

# Ciclo de Vida e Versionamento

[← Estrutura](structure.md) | [Avisos Legais →](legal-notices.md)

---

**Navegação:** [Início](../README.md) • [Conceito](concept.md) • [Estrutura](structure.md) • **Ciclo de Vida** • [Avisos Legais](legal-notices.md)

---

Este documento descreve o ciclo de vida de um CBAM Producer Data Package, incluindo estados, versionamento e governança dos dados.

---

## Estados do Dataset

O campo `DatasetStatus` indica o estado atual do pacote de dados:

```
┌────────────┐          ┌────────────┐
│   DRAFT    │─────────▶│   FINAL    │
│            │          │            │
└────────────┘          └────────────┘
    Mutável               Imutável
```

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

| Versão | Significado |
|--------|-------------|
| `1.0` | Geração inicial |
| `1.1` | Correção de dados de entrada |
| `2.0` | Recálculo completo com nova metodologia |

---

## Ciclo de Vida Típico

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        CICLO DE VIDA DO PACKAGE                         │
└─────────────────────────────────────────────────────────────────────────┘

  PRODUÇÃO               REVISÃO              FECHAMENTO          EXPORTAÇÃO
      │                     │                     │                   │
      ▼                     ▼                     ▼                   ▼
┌───────────┐         ┌───────────┐         ┌───────────┐       ┌───────────┐
│  Entrada  │────────▶│ Cálculo/  │────────▶│  Período  │──────▶│ Envio ao  │
│  de dados │         │ Verificação│        │  Fechado  │       │ Importador│
└───────────┘         └───────────┘         └───────────┘       └───────────┘
     │                     │                     │                   │
     │                     │                     │                   │
  Status:               Status:               Status:            Status:
  draft                 draft                 final              final
  Version: 1.0          Version: 1.x         Version: 1.x       Version: 1.x
```

---

## Eventos de Versionamento

### Quando Incrementar a Versão

| Evento | Ação |
|--------|------|
| Correção de dados de entrada (ex: quantidade) | Minor increment (1.0 → 1.1) |
| Recálculo de emissões | Minor increment (1.1 → 1.2) |
| Mudança de metodologia | Major increment (1.x → 2.0) |
| Fechamento do período | Não incrementa (apenas muda status) |

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

```
PRODUTOR                                              IMPORTADOR
   │                                                      │
   ├─── Gera package v1.0 (draft) ───────────────────────▶│
   │                                                      │
   │◀── Solicitação de correção ─────────────────────────┤
   │                                                      │
   ├─── Gera package v1.1 (draft) ───────────────────────▶│
   │                                                      │
   ├─── Fecha período: v1.1 (final) ─────────────────────▶│
   │                                                      │
   │                                         Valida e converte
   │                                                      │
   │                                         Submete ao Registry
   │                                                      ▼
                                                   CBAM REGISTRY
```

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

| Campo | Descrição |
|-------|-----------|
| `GeneratingSoftware.Name` | Nome do sistema gerador |
| `GeneratingSoftware.Version` | Versão do sistema |
| `GeneratedAt` | Timestamp de geração |
| `ClosedAt` | Timestamp de fechamento (se final) |

### Retenção

Recomenda-se manter os pacotes arquivados por pelo menos:

- **5 anos** para fins de auditoria CBAM
- **Conforme legislação local** para fins tributários e comerciais

---

**Anterior:** [← Estrutura](structure.md) | **Próximo:** [Avisos Legais →](legal-notices.md)

