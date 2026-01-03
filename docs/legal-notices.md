---
layout: docs
title: "Avisos Legais e Disclaimers"
page_title: "Avisos Legais"
breadcrumb: "Avisos Legais"
description: "Avisos legais, disclaimers e limitações de responsabilidade para uso do CBAM Producer Data Package."
prev_page:
  url: /docs/lifecycle
  title: "Ciclo de Vida"
---

Este documento contém avisos legais importantes sobre o uso e limitações do CBAM Producer Data Package.

---

## ⚠️ Aviso Principal

<div class="alert">
  <div class="alert-title">
    <i class="fas fa-exclamation-triangle"></i>
    Importante
  </div>
  <p><strong>O CBAM Producer Data Package NÃO é um relatório de submissão CBAM (QReport).</strong></p>
  <p>Este documento não pode ser submetido diretamente ao CBAM Registry da União Europeia.</p>
</div>

---

## Limitações do Formato

### O que este formato NÃO é

<div class="table-wrapper">

| ❌ NÃO é | Explicação |
|---------|------------|
| QReport oficial | Não substitui o formato oficial do CBAM Registry |
| Documento de compliance | Não comprova conformidade regulatória por si só |
| Certificado de emissões | Não é verificado por terceiros independentes |
| Schema oficial da UE | É um formato privado para troca de dados |

</div>

### O que este formato É

<div class="table-wrapper">

| ✅ É | Explicação |
|-----|------------|
| Contrato de dados | Define estrutura para comunicação produtor-importador |
| Formato intermediário | Facilita a preparação de dados para o CBAM |
| Especificação técnica | Permite validação automática de arquivos |
| Padrão aberto | Pode ser implementado por qualquer sistema |

</div>

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

<div class="warning-box">
  <div class="warning-box-title">
    <i class="fas fa-exclamation-triangle"></i> Importante
  </div>
  <p>A classificação de códigos CN/HS é de <strong>responsabilidade legal exclusiva do importador</strong>. O produtor fornece apenas uma sugestão informativa.</p>
</div>

---

## Disclaimers

### Sobre Precisão dos Dados

> Os dados contidos em um CBAM Producer Data Package são fornecidos pelo produtor com base em suas melhores informações disponíveis na data de geração. O importador deve realizar sua própria verificação antes de utilizar os dados para fins regulatórios.

### Sobre Metodologia de Cálculo

> As emissões reportadas são calculadas de acordo com metodologias declaradas no pacote. Este formato não define nem endossa metodologias específicas de cálculo, que devem seguir as regulamentações aplicáveis (EU 2023/956 e regulamentos de implementação).

### Sobre Conformidade Regulatória

> O uso deste formato não garante conformidade com o CBAM. A conformidade depende da precisão dos dados, adequação da metodologia e correta submissão ao CBAM Registry pelo importador.

---

## Texto de Disclaimer para Inclusão em Pacotes

Recomenda-se incluir o seguinte texto no campo `LegalDisclaimer` de cada pacote gerado:

### Em Inglês

```text
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

```text
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

<div class="info-box">
  <div class="info-box-title">
    <i class="fas fa-shield-alt"></i> Recomendação
  </div>
  <p>Estabelecer acordos de confidencialidade (NDA) entre produtor e importador.</p>
</div>

---

## Referências Regulatórias

<div class="table-wrapper">

| Regulamento | Descrição |
|-------------|-----------|
| EU 2023/956 | Regulamento CBAM principal |
| EU 2023/1773 | Regulamento de Implementação |
| Anexo I | Lista de produtos cobertos |
| Anexo III | Metodologias de cálculo |

</div>

---

## Isenção de Responsabilidade

<div class="alert">
  <div class="alert-title">
    <i class="fas fa-gavel"></i>
    Isenção de Responsabilidade
  </div>
  <p><strong>Os mantenedores deste formato NÃO se responsabilizam por:</strong></p>
  <ul>
    <li>Erros ou omissões nos dados fornecidos por produtores</li>
    <li>Interpretações incorretas da regulamentação CBAM</li>
    <li>Decisões de compliance baseadas neste formato</li>
    <li>Penalidades resultantes de uso inadequado</li>
    <li>Perdas financeiras de qualquer natureza</li>
  </ul>
  <p>O uso deste formato é por conta e risco do usuário. Recomenda-se consultar especialistas em compliance CBAM e autoridades competentes para orientações específicas.</p>
</div>

---

## Suporte e Contato

Para questões sobre:

- **Regulamentação CBAM:** Consultar [CBAM Registry](https://cbam.ec.europa.eu/) ou autoridades nacionais competentes
- **Este formato:** Abrir Issue no [repositório]({{ site.github.repository_url }}/issues)
- **Implementação específica:** Consultar documentação do software utilizado
