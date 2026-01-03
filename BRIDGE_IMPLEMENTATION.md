# Guia de Implementação: Product Bridge

## Implementação Rápida (30 minutos)

### Passo 1: Criar Formulário Google Forms

1. Acesse: https://forms.google.com
2. Crie novo formulário: "CBAM Automation - Early Access"
3. Adicione campos conforme `PRODUCT_BRIDGE.md` seção 4.1
4. Configure:
   - Coletar endereço de email: ✅
   - Limitar a 1 resposta: ✅ (opcional)
   - Mostrar barra de progresso: ✅
5. Copie o link de compartilhamento

### Passo 2: Adicionar CTAs no Site

#### A. Hero Section (`_layouts/default.html`)

**Localização**: Após os botões "Download Schema XSD" e "View on GitHub"

```html
<!-- Adicionar após linha ~1089 -->
<div class="hero-buttons">
  <a href="{{ '/schema/cbam-producer-data-package-v2.xsd' | relative_url }}" class="btn btn-primary">
    <i class="fas fa-download"></i>
    Download Schema XSD
  </a>
  <a href="{{ site.github.repository_url }}" class="btn btn-secondary">
    <i class="fab fa-github"></i>
    View on GitHub
  </a>
  <!-- NOVO: CTA Bridge -->
  <a href="[SEU_FORM_URL]" 
     class="btn btn-secondary cta-bridge"
     target="_blank"
     onclick="gtag('event', 'cta_click', {'event_category': 'bridge', 'event_label': 'hero'});">
    <i class="fas fa-bell"></i>
    {% if page.lang == 'pt-BR' %}Receber Acesso Antecipado{% else %}Get Early Access{% endif %}
  </a>
</div>
```

#### B. Getting Started Page (`getting-started.md`)

**Localização**: Após "Passo 4: Validar seu Arquivo"

```markdown
---

## Automatize sua Validação

Interessado em automatizar a validação XML e geração de relatórios CBAM?

<div style="margin: 2rem 0;">
  <a href="[SEU_FORM_URL]" 
     class="btn btn-secondary"
     target="_blank"
     onclick="gtag('event', 'cta_click', {'event_category': 'bridge', 'event_label': 'getting-started'});">
    <i class="fas fa-rocket"></i>
    {% if page.lang == 'pt-BR' %}Solicitar Acesso Beta{% else %}Request Beta Access{% endif %}
  </a>
</div>
```

#### C. Structure Page (`docs/structure.md`)

**Localização**: Após tabela "Field Classification"

```markdown
---

## Precisa de Suporte para Implementação?

<div class="info-box">
  <div class="info-box-title">
    <i class="fas fa-info-circle"></i>
    Implementação Empresarial
  </div>
  <p>Estamos desenvolvendo ferramentas para automatizar a geração e validação de pacotes CBAM.</p>
  <a href="[SEU_FORM_URL]" 
     class="btn btn-primary"
     target="_blank"
     onclick="gtag('event', 'cta_click', {'event_category': 'bridge', 'event_label': 'structure'});">
    <i class="fas fa-envelope"></i>
    {% if page.lang == 'pt-BR' %}Entre em Contato{% else %}Contact Us{% endif %}
  </a>
</div>
```

### Passo 3: Estilizar CTA (CSS)

**Adicionar em `_layouts/default.html` e `_layouts/docs.html`**:

```css
/* CTA Bridge Styles */
.cta-bridge {
  position: relative;
  border: 1px solid var(--color-primary);
  background: rgba(16, 185, 129, 0.05);
}

.cta-bridge:hover {
  background: rgba(16, 185, 129, 0.1);
  border-color: var(--color-primary-light);
}

.cta-bridge::after {
  content: '🔔';
  position: absolute;
  top: -8px;
  right: -8px;
  font-size: 0.75rem;
  opacity: 0.8;
}
```

### Passo 4: Configurar Google Analytics Events

**Adicionar em `_layouts/default.html` (já existe, apenas verificar):**

```javascript
// Já configurado no onclick dos CTAs
gtag('event', 'cta_click', {
  'event_category': 'bridge',
  'event_label': 'hero' // ou 'getting-started', 'structure'
});
```

**Criar Goal no GA4:**
1. Admin → Events
2. Criar evento: `cta_click`
3. Parâmetros: `event_category`, `event_label`

### Passo 5: Configurar Email Automation

#### Opção A: Mailchimp (Gratuito até 500 contatos)

1. Criar lista: "CBAM Early Access"
2. Criar template de email de confirmação
3. Configurar automação:
   - Trigger: Novo contato adicionado
   - Ação: Enviar email de confirmação

#### Opção B: Zapier/Make.com (Automação)

1. Trigger: Nova resposta no Google Forms
2. Actions:
   - Calcular score (via Google Sheets formula)
   - Adicionar ao Mailchimp
   - Enviar email personalizado por tier

### Passo 6: Criar Dashboard de Métricas (Google Sheets)

**Estrutura da Planilha:**

| Coluna | Fórmula/Valor |
|--------|---------------|
| Timestamp | Automático (Google Forms) |
| Nome | Form |
| Email | Form |
| Cargo | Form |
| Empresa | Form |
| Setor | Form |
| Volume | Form |
| Timeline | Form |
| **Score** | `=IF(AND(ISNUMBER(SEARCH("@",E2)), LEN(E2)>5), 2, 0) + IF(OR(SEARCH("ESG",C2), SEARCH("Compliance",C2)), 2, 0) + ...` |
| **Tier** | `=IF(G2>=9, "Tier 1", IF(G2>=7, "Tier 2", IF(G2>=5, "Tier 3", "Tier 4")))` |
| Status | Manual (Hot/Warm/Cold) |
| Notes | Manual |

**Fórmula de Score (exemplo):**

```excel
=IF(AND(ISNUMBER(SEARCH("@",E2)), NOT(OR(ISNUMBER(SEARCH("gmail",E2)), ISNUMBER(SEARCH("hotmail",E2))))), 2, 0)
+ IF(OR(ISNUMBER(SEARCH("ESG",C2)), ISNUMBER(SEARCH("Compliance",C2)), ISNUMBER(SEARCH("Sustentabilidade",C2))), 2, 0)
+ IF(OR(F2="Siderurgia", F2="Alumínio", F2="Cimento", F2="Fertilizantes"), 2, 0)
+ IF(OR(H2="10-50", H2="50-200", H2=">200"), 2, 0)
+ IF(OR(I2="<3 meses", I2="3-6 meses"), 1, 0)
+ IF(LEN(J2)>50, 1, 0)
```

### Passo 7: Testar Fluxo Completo

1. ✅ Clicar em CTA
2. ✅ Preencher formulário
3. ✅ Verificar resposta no Google Sheets
4. ✅ Verificar email de confirmação
5. ✅ Verificar evento no Google Analytics

---

## Templates de Email

### Email de Confirmação (Tier 1 - Hot Lead)

**Assunto**: "Thank you for your interest - CBAM Automation"

**Corpo (HTML)**:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body { font-family: Arial, sans-serif; line-height: 1.6; color: #333; }
    .container { max-width: 600px; margin: 0 auto; padding: 20px; }
    .header { background: #10b981; color: white; padding: 20px; text-align: center; }
    .content { padding: 20px; background: #f9f9f9; }
    .button { display: inline-block; padding: 12px 24px; background: #10b981; color: white; text-decoration: none; border-radius: 4px; margin: 20px 0; }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <h1>CBAM Producer Data Package</h1>
    </div>
    <div class="content">
      <p>Dear [Name],</p>
      
      <p>Thank you for expressing interest in automated CBAM compliance workflows.</p>
      
      <p>We're currently developing tools to help <strong>[Company]</strong> streamline CBAM Producer Data Package generation and validation.</p>
      
      <p>Based on your profile, we believe our solution could help you:</p>
      <ul>
        <li>Automate XML validation against the CBAM schema</li>
        <li>Generate compliant packages from your existing data</li>
        <li>Reduce manual errors in quarterly reporting</li>
      </ul>
      
      <p>We'll keep you updated on our progress and notify you when beta access becomes available.</p>
      
      <a href="[DOC_URL]" class="button">Explore Documentation</a>
      
      <p>Best regards,<br>
      CBAM Spec Team</p>
    </div>
  </div>
</body>
</html>
```

### Email de Confirmação (Tier 2-4)

**Assunto**: "You're on the waitlist - CBAM Automation"

**Corpo (simplificado)**:

```html
<p>Hi [Name],</p>

<p>Thanks for joining our waitlist! We're building tools to automate CBAM compliance workflows.</p>

<p>You'll receive updates as we progress, including:</p>
<ul>
  <li>Beta access announcements</li>
  <li>New features and capabilities</li>
  <li>Best practices and case studies</li>
</ul>

<p>Learn more: <a href="[DOC_URL]">CBAM Producer Data Package Specification</a></p>

<p>Best,<br>
CBAM Spec Team</p>
```

---

## Checklist de Implementação

### Semana 1
- [ ] Criar formulário Google Forms
- [ ] Adicionar CTAs no Hero (EN + PT-BR)
- [ ] Adicionar CTA no Getting Started
- [ ] Configurar Google Analytics events
- [ ] Testar fluxo completo

### Semana 2
- [ ] Configurar email de confirmação (Mailchimp)
- [ ] Criar dashboard Google Sheets
- [ ] Implementar fórmula de scoring
- [ ] Adicionar CTA no Structure page
- [ ] Documentar processo interno

### Semana 3
- [ ] Analisar primeiras métricas
- [ ] Ajustar copy baseado em feedback
- [ ] Otimizar formulário (campos opcionais)
- [ ] Configurar automação Zapier (opcional)

### Mês 2-3
- [ ] Revisar métricas mensais
- [ ] Ajustar segmentação
- [ ] Criar conteúdo de nurturing
- [ ] Decidir sobre aceleração/pivot

---

## Métricas a Monitorar (Dashboard)

### Google Analytics
- Eventos `cta_click` por localização
- Taxa de conversão: CTA → Form
- Tempo na página antes do click
- Scroll depth

### Google Sheets
- Total de submissões
- Taxa de qualificação (Tier 1+2 / Total)
- Distribuição por setor
- Score médio
- Timeline de implementação

### Email (Mailchimp)
- Taxa de abertura
- Taxa de clique
- Unsubscribes

---

## Próximos Passos Após Implementação

1. **Coletar dados por 2-3 meses**
2. **Analisar padrões de qualificação**
3. **Ajustar copy e posicionamento**
4. **Decidir sobre desenvolvimento do produto**
5. **Comunicar progresso aos leads qualificados**

---

**Última atualização**: Janeiro 2026

