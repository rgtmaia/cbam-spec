# Template: Formulário Google Forms

## Estrutura do Formulário

### Seção 1: Informações de Contato

**Título**: "Informações de Contato"

1. **Nome Completo**
   - Tipo: Resposta curta
   - Obrigatório: ✅
   - Validação: Texto

2. **Email Corporativo**
   - Tipo: Resposta curta
   - Obrigatório: ✅
   - Validação: Email
   - Dica: "Por favor, use seu email corporativo"

3. **Cargo / Função**
   - Tipo: Resposta curta
   - Obrigatório: ✅
   - Dica: "Ex: Gerente de ESG, Analista de Compliance, Diretor de Exportação"

4. **Empresa / Organização**
   - Tipo: Resposta curta
   - Obrigatório: ✅

---

### Seção 2: Perfil da Organização

**Título**: "Sobre sua Organização"

5. **Setor de Atuação**
   - Tipo: Múltipla escolha
   - Obrigatório: ✅
   - Opções:
     - Siderurgia (Ferro e Aço)
     - Alumínio
     - Cimento
     - Fertilizantes
     - Hidrogênio
     - Eletricidade
     - Consultoria / Serviços
     - Software / Tecnologia
     - Outro (especifique)

6. **Tamanho da Organização**
   - Tipo: Múltipla escolha
   - Obrigatório: ✅
   - Opções:
     - Menos de 50 funcionários
     - 50 - 250 funcionários
     - 250 - 1.000 funcionários
     - Mais de 1.000 funcionários

7. **País de Operação Principal**
   - Tipo: Múltipla escolha
   - Obrigatório: ✅
   - Opções: Lista de países (priorizar: Brasil, EU, Índia, China, Turquia)

---

### Seção 3: Papel no CBAM

**Título**: "Seu Papel no CBAM"

8. **Qual é seu papel em relação ao CBAM?**
   - Tipo: Múltipla escolha (permitir múltiplas seleções)
   - Obrigatório: ✅
   - Opções:
     - Produtor (empresa que exporta produtos CBAM)
     - Importador (empresa que importa produtos CBAM na UE)
     - Consultor (assessoria em compliance CBAM)
     - Desenvolvedor (integração de sistemas)
     - Outro (especifique)

9. **Volume Estimado de Transações CBAM/Ano**
   - Tipo: Múltipla escolha
   - Obrigatório: ✅
   - Opções:
     - Ainda não iniciado
     - Menos de 10 transações
     - 10 - 50 transações
     - 50 - 200 transações
     - Mais de 200 transações
     - Não se aplica

---

### Seção 4: Interesse e Necessidades

**Título**: "Sobre seu Interesse"

10. **Caso de Uso Principal**
    - Tipo: Parágrafo
    - Obrigatório: ✅
    - Limite de caracteres: 200
    - Dica: "Descreva brevemente como você pretende usar ferramentas de automação CBAM"

11. **Timeline de Implementação**
    - Tipo: Múltipla escolha
    - Obrigatório: ✅
    - Opções:
      - Menos de 3 meses
      - 3 - 6 meses
      - 6 - 12 meses
      - Mais de 12 meses
      - Apenas explorando opções

12. **Preferência de Contato**
    - Tipo: Múltipla escolha (permitir múltiplas seleções)
    - Obrigatório: ✅
    - Opções:
      - Email
      - Telefone
      - LinkedIn
      - WhatsApp (Brasil)

---

### Seção 5: Opcional (Qualificação Avançada)

**Título**: "Informações Adicionais (Opcional)"

13. **Como você conheceu a especificação CBAM Producer Data Package?**
    - Tipo: Múltipla escolha
    - Obrigatório: ❌
    - Opções:
      - Busca no Google
      - Recomendação de colega
      - Evento / Conferência
      - LinkedIn / Redes sociais
      - Artigo técnico
      - Outro

14. **Idioma Preferido**
    - Tipo: Múltipla escolha
    - Obrigatório: ❌
    - Opções:
      - English
      - Português (BR)

15. **Comentários Adicionais**
    - Tipo: Parágrafo
    - Obrigatório: ❌
    - Dica: "Alguma informação adicional que gostaria de compartilhar?"

---

## Configurações do Formulário

### Geral
- ✅ Coletar endereços de email
- ✅ Limitar a 1 resposta por pessoa
- ✅ Mostrar barra de progresso
- ✅ Enviar cópia da resposta por email

### Apresentação
- Tema: Profissional (azul/verde)
- Imagem de cabeçalho: Logo CBAM (opcional)
- Mensagem de confirmação personalizada

### Mensagem de Confirmação

**Título**: "Obrigado pelo seu interesse!"

**Mensagem**:
```
Obrigado por se inscrever! Recebemos sua solicitação de acesso antecipado.

Você receberá atualizações sobre:
- Desenvolvimento de ferramentas de automação CBAM
- Acesso beta quando disponível
- Melhores práticas e estudos de caso

Enquanto isso, explore nossa documentação técnica:
[Link para documentação]

Equipe CBAM Spec
```

---

## Fórmula de Scoring (Google Sheets)

Após receber respostas, adicionar colunas calculadas:

### Coluna "Score" (coluna H)

```excel
=IF(AND(ISNUMBER(SEARCH("@",B2)), NOT(OR(ISNUMBER(SEARCH("gmail",B2)), ISNUMBER(SEARCH("hotmail",B2)), ISNUMBER(SEARCH("yahoo",B2)), ISNUMBER(SEARCH("outlook",B2))))), 2, 0)
+ IF(OR(ISNUMBER(SEARCH("ESG",C2)), ISNUMBER(SEARCH("Compliance",C2)), ISNUMBER(SEARCH("Sustentabilidade",C2)), ISNUMBER(SEARCH("Exportação",C2)), ISNUMBER(SEARCH("Regulatory",C2))), 2, 0)
+ IF(OR(E2="Siderurgia (Ferro e Aço)", E2="Alumínio", E2="Cimento", E2="Fertilizantes", E2="Hidrogênio", E2="Eletricidade"), 2, 0)
+ IF(OR(I2="10 - 50 transações", I2="50 - 200 transações", I2="Mais de 200 transações"), 2, 0)
+ IF(OR(K2="Menos de 3 meses", K2="3 - 6 meses"), 1, 0)
+ IF(LEN(J2)>50, 1, 0)
```

### Coluna "Tier" (coluna I)

```excel
=IF(H2>=9, "Tier 1 - Hot", IF(H2>=7, "Tier 2 - Warm", IF(H2>=5, "Tier 3 - Cold", "Tier 4 - Curioso")))
```

### Coluna "Status" (coluna J)

```excel
=IF(I2="Tier 1 - Hot", "Follow-up em 24h", IF(I2="Tier 2 - Warm", "Email confirmação", IF(I2="Tier 3 - Cold", "Newsletter", "Apenas confirmação")))
```

---

## Exemplo de Resposta Qualificada (Tier 1)

| Campo | Resposta |
|-------|----------|
| Nome | João Silva |
| Email | joao.silva@siderurgicaexemplo.com.br |
| Cargo | Gerente de ESG e Sustentabilidade |
| Empresa | Siderúrgica Exemplo S.A. |
| Setor | Siderurgia (Ferro e Aço) |
| Tamanho | Mais de 1.000 funcionários |
| País | Brasil |
| Papel | Produtor |
| Volume | 50 - 200 transações |
| Caso de Uso | Precisamos automatizar a geração de pacotes CBAM para nossos clientes europeus. Atualmente fazemos manualmente e há risco de erros. |
| Timeline | 3 - 6 meses |
| Contato | Email, Telefone |

**Score Calculado**: 10 (Tier 1 - Hot)

---

## Exemplo de Resposta Curiosa (Tier 4)

| Campo | Resposta |
|-------|----------|
| Nome | Maria Santos |
| Email | maria.santos@gmail.com |
| Cargo | Estudante |
| Empresa | Universidade XYZ |
| Setor | Outro (Pesquisa acadêmica) |
| Tamanho | Menos de 50 funcionários |
| País | Brasil |
| Papel | Outro (Pesquisa) |
| Volume | Ainda não iniciado |
| Caso de Uso | Estou pesquisando sobre CBAM para minha tese. |
| Timeline | Apenas explorando opções |
| Contato | Email |

**Score Calculado**: 2 (Tier 4 - Curioso)

---

## Automação Sugerida (Zapier/Make.com)

### Trigger
- Nova resposta no Google Forms

### Actions
1. **Adicionar ao Google Sheets** (já automático)
2. **Calcular Score** (via fórmula no Sheets)
3. **Enviar Email por Tier**:
   - Tier 1: Email personalizado (Mailchimp)
   - Tier 2: Email de confirmação padrão
   - Tier 3-4: Email genérico

### Condições
```
IF Score >= 9:
  → Enviar email personalizado
  → Criar tarefa no Trello/Asana para follow-up
ELSE IF Score >= 7:
  → Enviar email de confirmação
  → Adicionar à lista "Warm Leads"
ELSE:
  → Enviar email genérico
  → Adicionar à lista "Newsletter"
```

---

## Métricas a Extrair

### Por Setor
- Quantidade de leads por setor CBAM
- Taxa de qualificação por setor

### Por País
- Distribuição geográfica
- Países com maior interesse

### Por Timeline
- Urgência de implementação
- Leads com timeline <6 meses

### Por Volume
- Potencial de receita estimado
- Leads com volume alto (>50 transações)

---

**Última atualização**: Janeiro 2026

