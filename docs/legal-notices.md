---
layout: docs
title: "Avisos Legais"
page_title: "Avisos Legais"
breadcrumb: "Avisos Legais"
description: "Informações sobre licenciamento, responsabilidades e compliance relacionados ao CBAM Producer Data Package."
prev_page:
  url: /docs/lifecycle
  title: "Ciclo de Vida"
---

Este documento contém informações legais e de compliance relacionadas ao CBAM Producer Data Package.

---

## Licenciamento

### Especificação e Schema

O CBAM Producer Data Package Specification e seus arquivos associados são disponibilizados sob a licença **Apache 2.0**.

```
Copyright 2024-2026 CBAM Spec Contributors

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

### Arquivos Cobertos

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Arquivo</th><th>Licença</th></tr>
  </thead>
  <tbody>
    <tr><td><code>cbam-producer-data-package-v2.xsd</code></td><td>Apache 2.0</td></tr>
    <tr><td>Documentação (Markdown)</td><td>Apache 2.0</td></tr>
    <tr><td>Exemplos (XML)</td><td>Apache 2.0</td></tr>
  </tbody>
</table>
</div>

---

## Disclaimer

### Propósito

Esta especificação foi desenvolvida com o objetivo de:

1. **Padronizar** a comunicação de dados de emissões entre produtores e importadores
2. **Facilitar** o cumprimento das obrigações CBAM durante o período transitório
3. **Promover** interoperabilidade entre sistemas de diferentes organizações

### Limitações

> **AVISO IMPORTANTE**
> 
> Esta especificação é uma iniciativa comunitária e **NÃO** é um documento oficial da União Europeia ou de qualquer autoridade reguladora.

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Aspecto</th><th>Status</th></tr>
  </thead>
  <tbody>
    <tr><td>Reconhecimento oficial pela UE</td><td>❌ Não</td></tr>
    <tr><td>Validação pela Comissão Europeia</td><td>❌ Não</td></tr>
    <tr><td>Substituição de formulários oficiais</td><td>❌ Não</td></tr>
    <tr><td>Uso como formato auxiliar</td><td>✅ Sim</td></tr>
  </tbody>
</table>
</div>

### Responsabilidade

- Os **usuários** são responsáveis por verificar a conformidade de seus dados com os requisitos regulatórios
- Os **importadores** devem utilizar os formulários e sistemas oficiais do CBAM Transitional Registry para submissões
- Os **desenvolvedores** desta especificação não garantem adequação para propósitos específicos

---

## Referências Regulatórias

### Base Legal

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Documento</th><th>Referência</th></tr>
  </thead>
  <tbody>
    <tr><td>Regulamento CBAM</td><td>EU 2023/956</td></tr>
    <tr><td>Regulamento de Implementação</td><td>EU 2023/1773</td></tr>
    <tr><td>Orientações da Comissão</td><td>C(2023) 5512</td></tr>
  </tbody>
</table>
</div>

### Links Oficiais

- [CBAM - Taxation and Customs Union](https://taxation-customs.ec.europa.eu/carbon-border-adjustment-mechanism_en)
- [CBAM Transitional Registry](https://cbam.ec.europa.eu/)
- [EU Climate Action](https://climate.ec.europa.eu/eu-action/carbon-border-adjustment-mechanism_en)

---

## Contribuição

### Como Contribuir

1. **Issues**: Reporte problemas ou sugestões via GitHub Issues
2. **Pull Requests**: Envie correções ou melhorias
3. **Discussões**: Participe das discussões no repositório

### Código de Conduta

Contribuidores devem seguir o [Contributor Covenant](https://www.contributor-covenant.org/) versão 2.1.

### Processo de Revisão

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Tipo</th><th>Aprovação</th><th>Prazo</th></tr>
  </thead>
  <tbody>
    <tr><td>Typo/Correção simples</td><td>1 maintainer</td><td>~3 dias</td></tr>
    <tr><td>Melhoria de documentação</td><td>1 maintainer</td><td>~7 dias</td></tr>
    <tr><td>Alteração no schema</td><td>2 maintainers</td><td>~14 dias</td></tr>
    <tr><td>Breaking change</td><td>Consenso + RFC</td><td>~30 dias</td></tr>
  </tbody>
</table>
</div>

---

## Versionamento do Schema

### Política de Versão

Esta especificação segue [Semantic Versioning 2.0.0](https://semver.org/):

- **MAJOR** (X.0.0): Mudanças incompatíveis
- **MINOR** (2.X.0): Adições retrocompatíveis
- **PATCH** (2.0.X): Correções retrocompatíveis

### Histórico de Versões

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Versão</th><th>Data</th><th>Descrição</th></tr>
  </thead>
  <tbody>
    <tr><td>2.0.0</td><td>Jan 2026</td><td>Versão atual com classificação de campos</td></tr>
    <tr><td>1.0.0</td><td>Out 2024</td><td>Versão inicial</td></tr>
  </tbody>
</table>
</div>

### Suporte a Versões

<div class="table-wrapper">
<table>
  <thead>
    <tr><th>Versão</th><th>Status</th><th>Suporte até</th></tr>
  </thead>
  <tbody>
    <tr><td>2.x</td><td>✅ Ativa</td><td>—</td></tr>
    <tr><td>1.x</td><td>⚠️ Legado</td><td>Dez 2026</td></tr>
  </tbody>
</table>
</div>

---

## Contato

### Maintainers

Para questões relacionadas à especificação:

- **GitHub**: [rgtmaia/cbam-spec](https://github.com/rgtmaia/cbam-spec)
- **Issues**: Utilize o sistema de Issues do GitHub

### Suporte Comercial

Esta especificação é mantida pela comunidade. Para suporte comercial ou implementação corporativa, entre em contato com os maintainers.

---

## Agradecimentos

Este projeto foi inspirado por:

- Iniciativas de padronização de dados ambientais
- Comunidade de compliance CBAM
- Contribuidores open source

Agradecemos a todos que contribuíram com feedback e melhorias.
