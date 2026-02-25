# 🗺️ Guia: Configurar Google Maps API para Qmob

## ✅ Benefícios da API

Quando configurada, o app fará automaticamente:
- ✅ Detecta quadrante pelo endereço
- ✅ Preenche bairro automaticamente
- ✅ Busca supermercados, farmácias, restaurantes no raio
- ✅ Lista linhas de ônibus próximas
- ✅ Calcula walkability score

---

## 📋 Passo a Passo

### 1. Criar Conta Google Cloud (se não tiver)
- Acesse: https://console.cloud.google.com
- Faça login com sua conta Google
- **Bônus:** $300 de crédito grátis por 90 dias

### 2. Criar um Projeto
- No console, clique em "Select a project" (topo)
- Clique em "New Project"
- Nome: `Qmob` (ou o que quiser)
- Clique em "Create"

### 3. Ativar APIs Necessárias
- No menu lateral, vá em "APIs & Services" → "Library"
- Procure e ative:
  - ✅ **Geocoding API** (converte endereço em coordenadas)
  - ✅ **Places API (New)** (busca pontos de interesse)
  - ✅ **Maps JavaScript API** (opcional, para mapas visuais)

### 4. Criar API Key
- No menu lateral, vá em "APIs & Services" → "Credentials"
- Clique em "Create Credentials" → "API Key"
- **COPIE A KEY** (ex: `AIzaSyB...`)
- Guarde em local seguro!

### 5. Restringir a API Key (IMPORTANTE - segurança)
- Clique na key criada para editar
- Em "Application restrictions":
  - Escolha "HTTP referrers"
  - Adicione: `https://seuusername.github.io/*`
  - Adicione: `http://localhost/*` (para testes locais)
- Em "API restrictions":
  - Escolha "Restrict key"
  - Selecione apenas: Geocoding API, Places API
- Salve

### 6. Configurar Billing (necessário mesmo com crédito grátis)
- No menu lateral, vá em "Billing"
- Vincule um cartão de crédito
- **Não se preocupe:** Você tem $300 grátis e pode configurar alertas
- Configure alerta: $10/mês (será notificado se passar)

---

## 💰 Custos Estimados

| API | Custo | Uso Mensal Estimado | Total |
|-----|-------|---------------------|-------|
| Geocoding | $5 por 1000 chamadas | 100 auditorias | $0.50 |
| Places API | $17 por 1000 chamadas | 100 auditorias x 5 buscas | $8.50 |
| **TOTAL** | | 100 auditorias/mês | **~$9/mês** |

**Observação:** Primeiros 90 dias são grátis ($300 de crédito)

---

## 🔧 Adicionar no App

### Opção A: Direto no código (mais simples)
Edite o arquivo `qmob-app-v4.html`:

1. Procure por: `const geocodeUrl = \`https://maps.googleapis.com`
2. Substitua por:
```javascript
const geocodeUrl = `https://maps.googleapis.com/maps/api/geocode/json?address=${encodeURIComponent(enderecoCompleto)}&key=SUA_API_KEY_AQUI`;
```

### Opção B: Campo de configuração (mais seguro)
Adicionar um campo de configuração no app onde você cola a API Key.
Isso evita expor a key no código do GitHub.

---

## 🛡️ Segurança

**NUNCA:**
- ❌ Compartilhe sua API Key publicamente
- ❌ Comite a key no GitHub sem restrições
- ❌ Use a mesma key em projetos diferentes

**SEMPRE:**
- ✅ Restrinja a key por HTTP referrer
- ✅ Restrinja apenas às APIs necessárias
- ✅ Configure alertas de billing
- ✅ Revogue e recrie keys periodicamente

---

## 🧪 Testar

Depois de configurar:
1. Abra o app
2. Digite um endereço: "Rua Padre Chagas, 300"
3. Clique em "Buscar Dados"
4. Deve preencher: Quadrante Q1, Bairro: Moinhos de Vento

---

## ❓ Problemas Comuns

**"REQUEST_DENIED"**
→ API Key não configurada ou inválida

**"OVER_QUERY_LIMIT"**
→ Passou do limite gratuito, precisa billing

**"ZERO_RESULTS"**
→ Endereço não encontrado, verifique digitação

**"Quadrante não detectado"**
→ Endereço fora da área de atuação (polígono)

---

## 📞 Suporte

Dúvidas? Consulte:
- Documentação: https://developers.google.com/maps/documentation
- Pricing: https://developers.google.com/maps/billing-and-pricing/pricing
