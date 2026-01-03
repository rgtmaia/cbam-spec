# Setup do Product Bridge - Instruções Rápidas

## ⚠️ Ação Necessária: Configurar URL do Formulário

Os CTAs foram implementados no site, mas você precisa substituir o placeholder `YOUR_FORM_ID_HERE` pela URL real do seu formulário Google Forms.

### Passo 1: Criar Formulário Google Forms

1. Acesse: https://forms.google.com
2. Crie novo formulário seguindo o template em `FORM_TEMPLATE.md`
3. Copie o link de compartilhamento (formato: `https://forms.gle/XXXXXXXXXX`)

### Passo 2: Substituir URLs nos Arquivos

Execute a busca e substituição em todos os arquivos:

**Buscar**: `https://forms.gle/YOUR_FORM_ID_HERE`
**Substituir**: `https://forms.gle/SEU_ID_AQUI`

**Arquivos a atualizar:**
- `_layouts/default.html` (linha ~1097)
- `getting-started.md` (linha ~187)
- `pt-br/getting-started.md` (linha ~188)
- `docs/structure.md` (linha ~327)
- `pt-br/docs/structure.md` (linha ~328)

### Passo 3: Verificar Google Analytics

Os eventos já estão configurados. Verifique no GA4:
- Admin → Events
- Evento: `cta_click`
- Parâmetros: `event_category`, `event_label`

---

## ✅ Checklist de Implementação

- [x] CTAs adicionados no Hero section
- [x] CTAs adicionados no Getting Started (EN + PT-BR)
- [x] CTAs adicionados no Structure (EN + PT-BR)
- [x] Estilos CSS implementados
- [x] Google Analytics events configurados
- [ ] **Formulário Google Forms criado**
- [ ] **URLs do formulário substituídas**
- [ ] Email de confirmação configurado (Mailchimp)
- [ ] Dashboard Google Sheets criado
- [ ] Fórmula de scoring implementada

---

## 📊 Próximos Passos

1. **Criar formulário** seguindo `FORM_TEMPLATE.md`
2. **Substituir URLs** nos arquivos
3. **Configurar email** de confirmação
4. **Criar dashboard** de métricas
5. **Testar fluxo** completo

---

**Status**: CTAs implementados ✅ | Formulário pendente ⏳

