# Product Bridge: CBAM Producer Data Package → SaaS

## 1. Arquitetura do Product Bridge

### 1.1 Estrutura de Captura

```
Documentação Técnica (GitHub Pages)
    ↓
[Ponto de Interesse] → [Formulário Qualificado] → [Confirmação + Tracking]
    ↓
[Email Sequence] → [Nurturing] → [Beta Access]
```

### 1.2 Componentes

1. **CTA Contextual** (não intrusivo, baseado em engajamento)
2. **Formulário de Interesse Qualificado** (Google Forms / Typeform)
3. **Email de Confirmação** (Mailchimp / SendGrid)
4. **Dashboard de Métricas** (Google Analytics + Sheets)

---

## 2. Posicionamento dos CTAs

### 2.1 Locais Estratégicos

#### **A. Hero Section (Homepage)**
- **Posição**: Após o botão "View on GitHub"
- **Visibilidade**: Sempre visível, mas discreto
- **Copy**: "Interested in automated validation? Join the waitlist"

#### **B. Getting Started Page**
- **Posição**: Após "Passo 4: Validar seu Arquivo"
- **Contexto**: Usuário acabou de aprender validação manual
- **Copy**: "Automate validation and compliance workflows"

#### **C. Structure Documentation**
- **Posição**: Após tabela de "Field Classification"
- **Contexto**: Usuário entendeu complexidade técnica
- **Copy**: "Need help implementing? Get early access"

#### **D. Examples Page**
- **Posição**: Após visualização do XML completo
- **Contexto**: Usuário viu complexidade real
- **Copy**: "Generate compliant packages automatically"

### 2.2 Design do CTA

**Estilo**: Botão secundário, não primário
- Cor: `var(--color-secondary)` (azul, não verde)
- Ícone: `fa-bell` ou `fa-envelope`
- Texto: Curto, ação clara
- Hover: Tooltip explicativo

**Exemplo Visual**:
```
┌─────────────────────────────────────┐
│  [Download Schema XSD] [View GitHub]│
│  [🔔 Get Early Access]              │
└─────────────────────────────────────┘
```

---

## 3. Copy dos CTAs (Regulatório, Profissional)

### 3.1 CTA Principal (Hero)

**Versão EN:**
```
"Interested in automated CBAM compliance workflows?"
[Get Early Access]
```

**Versão PT-BR:**
```
"Interessado em automação de compliance CBAM?"
[Receber Acesso Antecipado]
```

### 3.2 CTA Contextual (Getting Started)

**Versão EN:**
```
"Automate XML validation and CBAM report generation"
[Request Beta Access]
```

**Versão PT-BR:**
```
"Automatize validação XML e geração de relatórios CBAM"
[Solicitar Acesso Beta]
```

### 3.3 CTA Técnico (Structure)

**Versão EN:**
```
"Need implementation support for your organization?"
[Contact Us]
```

**Versão PT-BR:**
```
"Precisa de suporte para implementação na sua organização?"
[Entre em Contato]
```

### 3.4 Princípios do Copy

✅ **Fazer:**
- Foco em valor técnico (automação, validação, compliance)
- Linguagem institucional (organização, implementação)
- Benefício claro (economia de tempo, redução de erros)
- Call-to-action específica (não genérica)

❌ **Evitar:**
- "Transforme seu negócio"
- "Revolucione sua operação"
- "Join 10,000+ companies"
- Emojis excessivos
- Urgência artificial

---

## 4. Formulário de Interesse Qualificado

### 4.1 Campos Essenciais

#### **Identificação**
- Nome completo
- Email corporativo (validação de domínio)
- Cargo / Função
- Empresa / Organização

#### **Qualificação**
- Setor (dropdown: Siderurgia, Alumínio, Cimento, Fertilizantes, Hidrogênio, Eletricidade, Outro)
- Tamanho da organização (dropdown: <50, 50-250, 250-1000, >1000)
- Papel no CBAM (checkbox: Produtor, Importador, Consultor, Desenvolvedor)
- Volume estimado de transações CBAM/ano (dropdown: <10, 10-50, 50-200, >200)

#### **Interesse**
- Caso de uso principal (textarea, 200 chars)
- Timeline de implementação (dropdown: <3 meses, 3-6 meses, 6-12 meses, Explorando)
- Preferência de contato (checkbox: Email, Telefone, LinkedIn)

#### **Opcional (para qualificação avançada)**
- País de operação
- Idioma preferido (EN/PT-BR)
- Como conheceu a especificação

### 4.2 Validação de Qualificação

**Lead Qualificado (Score ≥ 7):**
- Email corporativo (não gmail/hotmail genérico) = +2
- Cargo relevante (ESG, Compliance, Sustentabilidade, Exportação) = +2
- Setor CBAM coberto = +2
- Volume >10 transações/ano = +2
- Timeline <6 meses = +1
- Caso de uso específico = +1

**Lead Curioso (Score < 7):**
- Email genérico
- Cargo não relacionado
- Setor não CBAM
- Sem timeline definida

---

## 5. Métricas Pré-Produto

### 5.1 Métricas de Engajamento (Google Analytics)

#### **Comportamento na Documentação**
- Tempo na página (Getting Started, Structure)
- Scroll depth (75%, 100%)
- Downloads de schema XSD
- Visualizações de exemplos XML
- Taxa de rejeição por página

#### **Conversão**
- Clicks em CTAs (por localização)
- Taxa de conversão: CTA click → Form submission
- Abandono no formulário (em qual campo)

### 5.2 Métricas de Qualificação (Google Sheets)

#### **Volume**
- Total de submissões
- Leads qualificados vs. curiosos
- Taxa de qualificação (qualificados / total)

#### **Perfil**
- Distribuição por setor
- Distribuição por país
- Distribuição por papel (Produtor/Importador)
- Timeline de implementação

#### **Qualidade**
- Score médio de qualificação
- Casos de uso mais comuns
- Volume estimado agregado

### 5.3 Métricas de Nurturing (Email)

- Taxa de abertura (confirmação)
- Taxa de clique em links de recursos
- Respostas a emails de follow-up
- Unsubscribes (baixa expectativa)

---

## 6. Diferenciação: Curiosos vs. Leads Qualificados

### 6.1 Critérios de Qualificação

| Critério | Curioso | Qualificado |
|----------|---------|-------------|
| **Email** | Gmail/Hotmail pessoal | Corporativo (empresa.com) |
| **Cargo** | Genérico ou estudante | ESG, Compliance, Exportação |
| **Setor** | Não CBAM ou genérico | Siderurgia, Alumínio, etc. |
| **Volume** | Não informado ou <10 | >10 transações/ano |
| **Timeline** | Explorando ou >12 meses | <6 meses |
| **Caso de uso** | Vago ou genérico | Específico e detalhado |

### 6.2 Segmentação Automática

**Tier 1 - Hot Leads (Score 9-10)**
- Email corporativo + Cargo relevante + Setor CBAM + Volume alto + Timeline curta
- **Ação**: Email personalizado em 24h, oferta de call

**Tier 2 - Warm Leads (Score 7-8)**
- Email corporativo + Cargo relevante + Setor CBAM
- **Ação**: Email de confirmação + recursos adicionais

**Tier 3 - Cold Leads (Score 5-6)**
- Email corporativo mas outros critérios fracos
- **Ação**: Newsletter genérica, nurturing longo prazo

**Tier 4 - Curiosos (Score <5)**
- Email pessoal ou critérios não atendidos
- **Ação**: Apenas confirmação, sem follow-up ativo

### 6.3 Fluxo de Nurturing por Tier

```
Tier 1 (Hot) → Email personalizado → Call agendado → Beta exclusivo
Tier 2 (Warm) → Email recursos → Newsletter → Beta quando disponível
Tier 3 (Cold) → Newsletter → Conteúdo educativo → Re-qualificação
Tier 4 (Curioso) → Confirmação → Sem follow-up ativo
```

---

## 7. Evolução do Bridge (Pré → Pós-Produto)

### 7.1 Fase 1: Pré-Produto (Atual)

**Objetivo**: Validar demanda, construir lista qualificada

**Ferramentas**:
- Google Forms / Typeform (formulário)
- Mailchimp / SendGrid (email)
- Google Analytics (métricas)
- Google Sheets (CRM básico)

**Métricas-chave**:
- Taxa de conversão CTA → Form
- Taxa de qualificação
- Volume de leads Tier 1

### 7.2 Fase 2: Beta Fechado

**Objetivo**: Testar produto com usuários reais

**Mudanças**:
- CTA muda para "Request Beta Access"
- Formulário inclui: "Interesse em beta testing?"
- Email de confirmação inclui: "Beta disponível em [data]"
- Dashboard: Tracking de beta signups

**Métricas-chave**:
- Beta signups por tier
- Taxa de ativação beta
- Feedback qualitativo

### 7.3 Fase 3: Produto Público

**Objetivo**: Conversão de leads em clientes

**Mudanças**:
- CTA muda para "Start Free Trial" ou "Schedule Demo"
- Formulário simplificado (já temos dados)
- Integração com CRM (HubSpot, Salesforce)
- A/B testing de CTAs

**Métricas-chave**:
- Trial signups
- Trial → Paid conversion
- CAC (Customer Acquisition Cost)
- LTV (Lifetime Value)

---

## 8. Implementação Técnica (Solução Simples)

### 8.1 Stack Mínimo

**Formulário**: Google Forms (gratuito) ou Typeform (plano básico)
- Embed via iframe ou link direto
- Respostas em Google Sheets
- Webhook para email automation (Zapier/Make.com)

**Email**: Mailchimp Free (até 500 contatos) ou SendGrid (100 emails/dia grátis)
- Template profissional
- Automação básica (confirmação, follow-up)

**Analytics**: Google Analytics 4 (gratuito)
- Event tracking para CTA clicks
- Goal tracking para form submissions

**CRM Básico**: Google Sheets + Apps Script
- Scoring automático
- Segmentação por tier
- Dashboard de métricas

### 8.2 Código do CTA (HTML)

```html
<!-- CTA Button -->
<a href="[FORM_URL]" 
   class="btn btn-secondary cta-bridge"
   onclick="gtag('event', 'cta_click', {'event_category': 'bridge', 'event_label': 'hero'});">
  <i class="fas fa-bell"></i>
  Get Early Access
</a>

<!-- Tooltip (opcional) -->
<div class="cta-tooltip">
  Join our waitlist to be notified when automated validation tools are available
</div>
```

### 8.3 Automação (Zapier/Make.com)

**Trigger**: Nova resposta no Google Forms
**Actions**:
1. Calcular score de qualificação
2. Adicionar ao Google Sheets (CRM)
3. Enviar email de confirmação (Mailchimp)
4. Se Tier 1: Criar tarefa para follow-up manual

---

## 9. Critérios de Sucesso do Bridge

### 9.1 Métricas de Sucesso (3 meses)

#### **Volume**
- ✅ 50+ submissões de formulário
- ✅ 20+ leads qualificados (Tier 1 + Tier 2)
- ✅ 5+ leads Tier 1 (Hot)

#### **Qualidade**
- ✅ Taxa de qualificação ≥ 40%
- ✅ Score médio ≥ 6.5
- ✅ 3+ setores CBAM representados

#### **Engajamento**
- ✅ Taxa de conversão CTA → Form ≥ 5%
- ✅ Taxa de abertura email ≥ 30%
- ✅ Tempo médio na documentação ≥ 3 min

### 9.2 Sinais de Validação de Demanda

**Demanda Forte:**
- Volume crescente de leads qualificados
- Múltiplos setores representados
- Timeline de implementação <6 meses
- Casos de uso específicos e variados

**Demanda Fraca:**
- Maioria de curiosos (score baixo)
- Setores não CBAM
- Timeline >12 meses ou "explorando"
- Casos de uso genéricos

### 9.3 Decisões Baseadas em Métricas

**Se demanda forte (≥20 leads qualificados em 3 meses):**
- Acelerar desenvolvimento do produto
- Priorizar features mais solicitadas
- Iniciar beta com Tier 1

**Se demanda moderada (10-19 leads):**
- Continuar nurturing
- Expandir conteúdo educativo
- Re-avaliar em 6 meses

**Se demanda fraca (<10 leads):**
- Revisar copy e posicionamento
- Expandir canais de aquisição
- Considerar pivot ou nicho mais específico

---

## 10. Próximos Passos

### 10.1 Implementação Imediata

1. **Adicionar CTAs** nos locais estratégicos (Hero, Getting Started, Structure)
2. **Criar formulário** Google Forms com campos de qualificação
3. **Configurar email** de confirmação (Mailchimp)
4. **Implementar tracking** (Google Analytics events)
5. **Criar dashboard** Google Sheets para métricas

### 10.2 Semana 1-2

- Testar fluxo completo (CTA → Form → Email)
- Validar scoring de qualificação
- Ajustar copy baseado em feedback inicial

### 10.3 Mês 1-3

- Coletar métricas
- Analisar padrões de qualificação
- Ajustar segmentação e nurturing
- Decidir sobre aceleração ou pivot

---

## 11. Templates e Recursos

### 11.1 Email de Confirmação (Tier 1)

**Assunto**: "Thank you for your interest in CBAM automation"

**Corpo**:
```
Dear [Name],

Thank you for expressing interest in automated CBAM compliance workflows.

We're currently developing tools to help [Company] streamline CBAM Producer Data Package generation and validation.

Based on your profile, we believe our solution could help you:
- Automate XML validation against the CBAM schema
- Generate compliant packages from your existing data
- Reduce manual errors in quarterly reporting

We'll keep you updated on our progress and notify you when beta access becomes available.

In the meantime, feel free to explore our technical specification:
[Link to documentation]

Best regards,
[Your Name]
CBAM Spec Team
```

### 11.2 Email de Confirmação (Tier 2-4)

**Assunto**: "You're on the waitlist for CBAM automation tools"

**Corpo**:
```
Hi [Name],

Thanks for joining our waitlist! We're building tools to automate CBAM compliance workflows.

You'll receive updates as we progress, including:
- Beta access announcements
- New features and capabilities
- Best practices and case studies

Learn more about the CBAM Producer Data Package specification:
[Link to documentation]

Best,
CBAM Spec Team
```

---

## 12. Considerações Finais

### 12.1 Princípios

- **Transparência**: Seja claro sobre o status do produto (em desenvolvimento)
- **Valor primeiro**: Ofereça valor (documentação) antes de pedir algo
- **Qualidade > Quantidade**: Melhor 10 leads qualificados que 100 curiosos
- **Respeito**: Não seja invasivo, respeite o contexto técnico

### 12.2 Riscos e Mitigações

**Risco**: CTAs muito agressivos afastam público técnico
**Mitigação**: Posicionar como "early access" ou "beta", não "venda"

**Risco**: Formulário muito longo reduz conversão
**Mitigação**: Campos opcionais claramente marcados, progresso visível

**Risco**: Promessas não cumpridas (produto não sai)
**Mitigação**: Ser transparente sobre timeline, não prometer datas específicas

---

**Documento criado em**: Janeiro 2026
**Versão**: 1.0
**Status**: Proposta para implementação

