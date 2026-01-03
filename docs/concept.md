# Conceito do CBAM Producer Data Package

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

```
┌─────────────────────────────────────────────────────────────────────┐
│                        CADEIA DE DADOS CBAM                         │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   PRODUTOR          PACOTE DE DADOS         IMPORTADOR    REGISTRY │
│  (ex: Brasil)        (este spec)              (EU)          (UE)   │
│                                                                     │
│  ┌──────────┐      ┌──────────────┐       ┌──────────┐   ┌───────┐ │
│  │ Cálculo  │─────▶│   Producer   │──────▶│ Validação│──▶│QReport│ │
│  │ emissões │      │ Data Package │       │ e uso    │   │       │ │
│  └──────────┘      └──────────────┘       └──────────┘   └───────┘ │
│                            ▲                                        │
│                            │                                        │
│                   Este formato define                               │
│                   a estrutura de dados                              │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Escopo Regulatório vs. Não-Regulatório

### Campos Regulatórios

São campos diretamente exigidos pelo Regulamento EU 2023/956 e seus regulamentos de implementação. Exemplos:

| Campo | Descrição |
|-------|-----------|
| `DeterminationType` | Se os dados são reais (01) ou default (02) |
| `SpecificEmissions` | Emissões específicas em tCO2e por tonelada |
| `RouteCode` | Rota produtiva (BF-BOF, EAF, etc.) |
| `MethodologyCode` | Metodologia de cálculo (TOM01, TOM02) |

### Campos Não-Regulatórios

Campos informativos para facilitar a leitura humana, rastreabilidade ou integração:

| Campo | Descrição |
|-------|-----------|
| `Description` | Descrição textual do produto |
| `LegalName` | Razão social da empresa |
| `ConsolidatedSummary` | Resumo agregado (apenas informativo) |
| `PackageMetadata` | Metadados de geração do pacote |

### Campos Informativos

Campos cuja responsabilidade final de classificação é do **importador**:

| Campo | Descrição |
|-------|-----------|
| `CnCode` | Código da Nomenclatura Combinada (8 dígitos) |
| `HsCode` | Código do Sistema Harmonizado (6 dígitos) |

⚠️ **Importante:** O produtor fornece sua melhor estimativa, mas a responsabilidade legal pela classificação aduaneira correta é do importador.

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

```
┌──────────────────────────────────────────────────────────────────┐
│                    EMISSÕES INCORPORADAS                         │
│                  (Embedded Emissions)                            │
├────────────────────┬────────────────────┬───────────────────────┤
│   DIRETAS          │   INDIRETAS        │   PRECURSORES         │
│   (Scope 1)        │   (Scope 2)        │                       │
├────────────────────┼────────────────────┼───────────────────────┤
│ • Queima de        │ • Consumo de       │ • Emissões de         │
│   combustíveis     │   eletricidade     │   materiais de        │
│                    │   da rede          │   entrada que são     │
│ • Reações          │                    │   produtos CBAM       │
│   químicas         │                    │   (ex: ferro-gusa     │
│                    │                    │   usado em aço)       │
│ • Processos        │                    │                       │
│   industriais      │                    │                       │
└────────────────────┴────────────────────┴───────────────────────┘
```

### Emissões Específicas

O CBAM utiliza primariamente **emissões específicas** (por unidade de produto):

| Unidade | Uso |
|---------|-----|
| `tCO2e/t` | Toneladas de CO2eq por tonelada de produto |
| `tCO2e/MWh` | Para eletricidade |

---

## Período de Reporte

O CBAM opera em ciclos trimestrais:

| Trimestre | Período | Deadline de Submissão |
|-----------|---------|----------------------|
| Q1 | Janeiro - Março | 30 de Abril |
| Q2 | Abril - Junho | 31 de Julho |
| Q3 | Julho - Setembro | 31 de Outubro |
| Q4 | Outubro - Dezembro | 31 de Janeiro (ano seguinte) |

---

## Referências

- [Regulamento EU 2023/956 (CBAM)](https://eur-lex.europa.eu/eli/reg/2023/956)
- [Regulamento de Implementação EU 2023/1773](https://eur-lex.europa.eu/eli/reg_impl/2023/1773)
- [Portal CBAM da Comissão Europeia](https://cbam.ec.europa.eu/)

