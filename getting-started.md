---
layout: docs
title: "Começando com o CBAM Producer Data Package"
page_title: "Começando"
breadcrumb: "Começar"
description: "Guia rápido para começar a usar o CBAM Producer Data Package em poucos minutos."
prev_page:
  url: /
  title: "Início"
next_page:
  url: /docs/concept
  title: "Conceito"
---

## Visão Geral

Este guia vai ajudá-lo a começar com o **CBAM Producer Data Package** em poucos minutos. Ao final, você terá:

1. ✅ Baixado o Schema XSD
2. ✅ Criado seu primeiro arquivo XML
3. ✅ Validado o arquivo contra o schema

---

## Passo 1: Baixar o Schema XSD

O schema XSD é o arquivo que define a estrutura válida do pacote de dados. Você precisa dele para validar seus arquivos XML.

### Download direto

<a href="{{ '/schema/cbam-producer-data-package-v2.xsd' | relative_url }}" class="btn btn-primary" style="margin: 1rem 0;">
  <i class="fas fa-download"></i> Download Schema XSD v2.0
</a>

### Via linha de comando

```bash
# Linux/Mac
curl -O https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd

# Windows (PowerShell)
Invoke-WebRequest -Uri "https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd" -OutFile "cbam-producer-data-package-v2.xsd"
```

---

## Passo 2: Estrutura Básica do XML

Todo arquivo CBAM Producer Data Package segue esta estrutura básica:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CBAMProducerDataPackage 
    xmlns="https://rgtmaia.github.io/cbam-spec/schema/package/v2"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://rgtmaia.github.io/cbam-spec/schema/package/v2 
                        https://rgtmaia.github.io/cbam-spec/schema/cbam-producer-data-package-v2.xsd"
    version="2.0"
    schemaVersion="2.0.0">

  <!-- Metadados do Pacote -->
  <PackageMetadata>
    <PackageId>PKG-2024-001</PackageId>
    <GenerationTimestamp>2024-01-15T10:30:00Z</GenerationTimestamp>
    <Status>draft</Status>
  </PackageMetadata>

  <!-- Informações do Operador (Produtor) -->
  <Operator>
    <OperatorId>OP-BR-001</OperatorId>
    <LegalName>Empresa Exemplo LTDA</LegalName>
    <Country>BR</Country>
  </Operator>

  <!-- Instalações -->
  <Installations>
    <Installation>
      <!-- dados da instalação -->
    </Installation>
  </Installations>

  <!-- Produtos -->
  <Products>
    <Product>
      <!-- dados do produto -->
    </Product>
  </Products>

</CBAMProducerDataPackage>
```

---

## Passo 3: Usar um Exemplo Pronto

A maneira mais fácil de começar é usar um dos nossos exemplos como base:

<div class="cards-grid" style="margin: 1.5rem 0;">
  <a href="{{ '/examples/example-v2-minimal.xml' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon" style="background: linear-gradient(135deg, var(--color-info) 0%, #1d4ed8 100%);">
      <i class="fas fa-file-alt"></i>
    </div>
    <h3>Exemplo Mínimo</h3>
    <p>Estrutura básica com 1 instalação e 1 produto. Ideal para entender o formato.</p>
  </a>
  
  <a href="{{ '/examples/example-v2-complete.xml' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon" style="background: linear-gradient(135deg, var(--color-success) 0%, #15803d 100%);">
      <i class="fas fa-file-code"></i>
    </div>
    <h3>Exemplo Completo</h3>
    <p>2 instalações, 3 produtos, emissões de precursores. Demonstra todas as funcionalidades.</p>
  </a>
</div>

### Baixar exemplos via terminal

```bash
# Exemplo Mínimo
curl -O https://rgtmaia.github.io/cbam-spec/examples/example-v2-minimal.xml

# Exemplo Completo
curl -O https://rgtmaia.github.io/cbam-spec/examples/example-v2-complete.xml
```

---

## Passo 4: Validar seu Arquivo

Após criar ou modificar seu arquivo XML, você deve validá-lo contra o schema XSD.

### Linux/Mac (xmllint)

```bash
# Instalar xmllint (se não tiver)
# Ubuntu/Debian: sudo apt install libxml2-utils
# Mac: brew install libxml2

# Validar
xmllint --schema cbam-producer-data-package-v2.xsd seu-arquivo.xml --noout
```

### Windows (PowerShell)

```powershell
# Usando .NET (nativo do Windows)
$schema = [System.Xml.Schema.XmlSchema]::Read(
    [System.Xml.XmlReader]::Create("cbam-producer-data-package-v2.xsd"), 
    $null
)

$settings = New-Object System.Xml.XmlReaderSettings
$settings.Schemas.Add($schema)
$settings.ValidationType = [System.Xml.ValidationType]::Schema

$reader = [System.Xml.XmlReader]::Create("seu-arquivo.xml", $settings)
while ($reader.Read()) { }
$reader.Close()

Write-Host "Validação concluída com sucesso!"
```

### Python

```python
from lxml import etree

# Carregar schema
with open('cbam-producer-data-package-v2.xsd', 'rb') as f:
    schema_doc = etree.parse(f)
    schema = etree.XMLSchema(schema_doc)

# Carregar e validar XML
with open('seu-arquivo.xml', 'rb') as f:
    doc = etree.parse(f)

if schema.validate(doc):
    print("✅ XML válido!")
else:
    print("❌ Erros encontrados:")
    for error in schema.error_log:
        print(f"  Linha {error.line}: {error.message}")
```

---

## Passo 5: Entender os Campos Obrigatórios

Os campos são classificados em três categorias:

<div class="table-wrapper">
<table>
  <thead>
    <tr>
      <th>Categoria</th>
      <th>Badge</th>
      <th>O que significa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>REGULATORY</strong></td>
      <td><span class="badge badge-red">🔴 Regulatório</span></td>
      <td>Campos exigidos pelo regulamento EU 2023/956. Obrigatórios.</td>
    </tr>
    <tr>
      <td><strong>NON-REGULATORY</strong></td>
      <td><span class="badge badge-yellow">🟡 Não-Regulatório</span></td>
      <td>Campos para rastreabilidade e leitura humana. Recomendados.</td>
    </tr>
    <tr>
      <td><strong>INFORMATIVE</strong></td>
      <td><span class="badge badge-blue">🔵 Informativo</span></td>
      <td>Campos cuja responsabilidade é do importador. Opcionais.</td>
    </tr>
  </tbody>
</table>
</div>

<div class="info-box">
  <div class="info-box-title">
    <i class="fas fa-info-circle"></i> Dica
  </div>
  <p>Para uma implementação rápida, foque primeiro nos campos <strong>REGULATORY</strong>. Os demais podem ser adicionados posteriormente.</p>
</div>

---

## Próximos Passos

Agora que você criou e validou seu primeiro arquivo, explore a documentação completa:

<div class="cards-grid" style="margin: 1.5rem 0;">
  <a href="{{ '/docs/concept' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-lightbulb"></i>
    </div>
    <h3>Conceito</h3>
    <p>Entenda o contexto regulatório e o propósito do formato.</p>
  </a>
  
  <a href="{{ '/docs/structure' | relative_url }}" class="card" style="text-decoration: none;">
    <div class="card-icon">
      <i class="fas fa-sitemap"></i>
    </div>
    <h3>Estrutura XML</h3>
    <p>Referência completa de todos os elementos e atributos.</p>
  </a>
</div>

---

## Precisa de Ajuda?

- 📖 Leia a [documentação completa]({{ '/docs/concept' | relative_url }})
- 🐛 Reporte problemas no [GitHub Issues]({{ site.github.repository_url }}/issues)
- 💬 Dúvidas? Abra uma [Discussion]({{ site.github.repository_url }}/discussions)

