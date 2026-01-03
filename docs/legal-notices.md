---
title: "Avisos Legais e Disclaimers"
description: "Avisos legais, disclaimers e limitações de responsabilidade para uso do CBAM Producer Data Package."
---

# Avisos Legais e Disclaimers

[← Ciclo de Vida](lifecycle.md) | [Voltar ao Início](../README.md)

---

**Navegação:** [Início](../README.md) • [Conceito](concept.md) • [Estrutura](structure.md) • [Ciclo de Vida](lifecycle.md) • **Avisos Legais**

---

Este documento contém avisos legais importantes sobre o uso e limitações do CBAM Producer Data Package.

---

## ⚠️ Aviso Principal

> **O CBAM Producer Data Package NÃO é um relatório de submissão CBAM (QReport).**
>
> Este documento não pode ser submetido diretamente ao CBAM Registry da União Europeia.

---

## Limitações do Formato

### O que este formato NÃO é

| ❌ NÃO é | Explicação |
|---------|------------|
| QReport oficial | Não substitui o formato oficial do CBAM Registry |
| Documento de compliance | Não comprova conformidade regulatória por si só |
| Certificado de emissões | Não é verificado por terceiros independentes |
| Schema oficial da UE | É um formato privado para troca de dados |

### O que este formato É

| ✅ É | Explicação |
|-----|------------|
| Contrato de dados | Define estrutura para comunicação produtor-importador |
| Formato intermediário | Facilita a preparação de dados para o CBAM |
| Especificação técnica | Permite validação automática de arquivos |
| Padrão aberto | Pode ser implementado por qualquer sistema |

---

## Responsabilidades

### Responsabilidade do Produtor

O produtor (operador) é responsável por:

1. **Veracidade dos dados** de produção e emissões
2. **Metodologia de cálculo** aplicada
3. **Documentação de suporte** para auditorias
4. **Atualização** de dados quando necessário

### Responsabilidade do Importador

O importador europeu é responsável por:

1. **Classificação aduaneira** correta (códigos CN/HS)
2. **Validação** dos dados recebidos
3. **Conversão** para o formato do CBAM Registry
4. **Submissão** do relatório trimestral
5. **Aquisição** de certificados CBAM

> **Importante:** A classificação de códigos CN/HS é de responsabilidade legal exclusiva do importador. O produtor fornece apenas uma sugestão informativa.

---

## Disclaimers

### Sobre Precisão dos Dados

```
Os dados contidos em um CBAM Producer Data Package são fornecidos 
pelo produtor com base em suas melhores informações disponíveis 
na data de geração. O importador deve realizar sua própria 
verificação antes de utilizar os dados para fins regulatórios.
```

### Sobre Metodologia de Cálculo

```
As emissões reportadas são calculadas de acordo com metodologias 
declaradas no pacote. Este formato não define nem endossa 
metodologias específicas de cálculo, que devem seguir as 
regulamentações aplicáveis (EU 2023/956 e regulamentos de 
implementação).
```

### Sobre Conformidade Regulatória

```
O uso deste formato não garante conformidade com o CBAM. A 
conformidade depende da precisão dos dados, adequação da 
metodologia e correta submissão ao CBAM Registry pelo importador.
```

---

## Texto de Disclaimer para Inclusão em Pacotes

Recomenda-se incluir o seguinte texto no campo `LegalDisclaimer` de cada pacote gerado:

### Em Inglês

```
IMPORTANT: This document is NOT a CBAM submission report (QReport) and 
cannot be submitted directly to the EU CBAM Registry. It is a CBAM 
Producer Data Package containing emission data for use by EU importers 
in completing their quarterly CBAM reports.

The importer is responsible for:
- Final verification of all data
- Commodity code classification (CN/HS codes)
- Submission to the CBAM Registry

This document does not constitute certification of emissions and is 
provided for informational purposes only.
```

### Em Português

```
IMPORTANTE: Este documento NÃO é um relatório de submissão CBAM 
(QReport) e não pode ser submetido diretamente ao CBAM Registry da 
União Europeia. É um CBAM Producer Data Package contendo dados de 
emissões para uso por importadores europeus.

O importador é responsável por:
- Verificação final de todos os dados
- Classificação de códigos aduaneiros (códigos CN/HS)
- Submissão ao CBAM Registry

Este documento não constitui certificação de emissões e é fornecido 
apenas para fins informativos.
```

---

## Proteção de Dados

### LGPD/GDPR

O formato foi projetado minimizando dados pessoais:

- **Não inclui** emails, telefones ou dados pessoais diretos
- **ContactDetails** contém apenas nome do departamento/função
- Dados de identificação empresarial (CNPJ, etc.) são públicos

### Dados Comerciais Sensíveis

O pacote pode conter informações comercialmente sensíveis:

- Volumes de produção
- Intensidade de emissões (pode indicar eficiência)
- Rotas de produção

**Recomendação:** Estabelecer acordos de confidencialidade (NDA) entre produtor e importador.

---

## Referências Regulatórias

| Regulamento | Descrição |
|-------------|-----------|
| EU 2023/956 | Regulamento CBAM principal |
| EU 2023/1773 | Regulamento de Implementação |
| Anexo I | Lista de produtos cobertos |
| Anexo III | Metodologias de cálculo |

---

## Isenção de Responsabilidade

```
OS MANTENEDORES DESTE FORMATO NÃO SE RESPONSABILIZAM POR:

1. Erros ou omissões nos dados fornecidos por produtores
2. Interpretações incorretas da regulamentação CBAM
3. Decisões de compliance baseadas neste formato
4. Penalidades resultantes de uso inadequado
5. Perdas financeiras de qualquer natureza

O uso deste formato é por conta e risco do usuário. Recomenda-se 
consultar especialistas em compliance CBAM e autoridades competentes 
para orientações específicas.
```

---

## Suporte e Contato

Para questões sobre:

- **Regulamentação CBAM:** Consultar [CBAM Registry](https://cbam.ec.europa.eu/) ou autoridades nacionais competentes
- **Este formato:** Abrir Issue no repositório
- **Implementação específica:** Consultar documentação do software utilizado

---

**Anterior:** [← Ciclo de Vida](lifecycle.md) | [Voltar ao Início](../README.md)

