# Missão Numberblocks — Deploy no Netlify

## Estrutura do projeto

```
numberblocks/
├── index.html                  ← App principal
├── netlify.toml                ← Configuração do Netlify
└── netlify/
    └── functions/
        └── claude.js           ← Proxy seguro para a API
```

---

## Como fazer o deploy (Netlify CLI)

### 1. Instala o Netlify CLI (uma única vez)
```bash
npm install -g netlify-cli
```

### 2. Faz login no Netlify
```bash
netlify login
```
(Abre o browser para autenticares)

### 3. Dentro da pasta do projeto, inicializa
```bash
cd numberblocks
netlify init
```
Escolhe: **"Create & configure a new site"**

### 4. Adiciona a tua chave API como variável de ambiente segura
```bash
netlify env:set ANTHROPIC_API_KEY sk-ant-SUACHAVEAQUI
```

### 5. Faz o deploy!
```bash
netlify deploy --prod
```

✅ O teu site fica online em segundos com URL tipo `https://nome-do-site.netlify.app`

---

## Como atualizar o site no futuro

Sempre que modificares os ficheiros, basta correr:
```bash
netlify deploy --prod
```

---

## Como a segurança funciona

```
Browser do utilizador
        │
        │  POST /api/claude  (sem chave!)
        ▼
Netlify Function (claude.js)
        │
        │  Injeta ANTHROPIC_API_KEY (variável de ambiente segura)
        ▼
API da Anthropic (Claude)
```

A chave **nunca aparece no código HTML** nem é visível para os utilizadores.
