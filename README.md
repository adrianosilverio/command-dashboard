# Crédito VR · Command Dashboard

Dashboard executivo pessoal. Roda 100% no browser, hospedado no GitHub Pages.

---

## Arquivos

```
/
├── index.html      ← dashboard principal (não edite manualmente)
├── config.json     ← sua fonte de verdade: OKRs, riscos, decisões, energia
└── README.md       ← este arquivo
```

---

## Como subir no GitHub Pages (passo a passo)

### 1. Criar o repositório

1. Acesse https://github.com/new
2. Nome sugerido: `command-dashboard` (pode ser privado ✓)
3. **Não** inicialize com README (você já tem os arquivos)
4. Clique em **Create repository**

### 2. Fazer upload dos arquivos

**Opção A — pelo browser (mais fácil):**
1. Na página do repositório recém-criado, clique em **uploading an existing file**
2. Arraste os 3 arquivos: `index.html`, `config.json`, `README.md`
3. Clique em **Commit changes**

**Opção B — pelo terminal (se tiver Git instalado):**
```bash
cd pasta-com-os-arquivos
git init
git add .
git commit -m "primeiro deploy"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/command-dashboard.git
git push -u origin main
```

### 3. Ativar o GitHub Pages

1. No repositório, clique em **Settings** (aba superior)
2. No menu esquerdo, clique em **Pages**
3. Em **Source**, selecione **Deploy from a branch**
4. Branch: `main` · Folder: `/ (root)`
5. Clique em **Save**
6. Aguarde ~2 minutos. A URL aparecerá no topo da página:
   `https://SEU_USUARIO.github.io/command-dashboard/`

### 4. (Opcional) Deixar o repositório privado mas o Pages público

GitHub Pages funciona com repositórios privados apenas no plano Pro/Team.
Se você tiver conta gratuita, o repositório precisa ser **público** para o Pages funcionar.
Alternativa gratuita: use **Netlify** (arraste a pasta no site, funciona em segundos).

---

## Como atualizar o dashboard

### Atualizar dados manuais (OKRs, riscos, decisões, energia)

Edite o `config.json` diretamente no GitHub:
1. Abra o arquivo `config.json` no repositório
2. Clique no ícone de lápis ✏️ (Edit this file)
3. Faça as alterações
4. Clique em **Commit changes**
5. O dashboard atualiza em ~1 minuto

### O que o `config.json` controla

| Campo | O que faz |
|---|---|
| `energia.nivel` | Define o indicador de energia e a sugestão do tipo de trabalho |
| `decisoes` | Lista de decisões pendentes com prazo e urgência |
| `riscos` | Radar de riscos com nível crítico/atenção/controle |
| `okrs` | OKRs com valor atual e esperado (gera o desvio automático) |
| `aguardando` | Lista de follow-ups pendentes com terceiros |
| `proxima_reuniao` | Banner da próxima reunião no header |
| `timeline` | Blocos na linha do tempo (também editáveis diretamente no dash) |
| `semana.dias` | Carga e eventos especiais de cada dia |

---

## Conectar com ClickUp e Linear (fase 2)

O dashboard atual usa dados do `config.json`. Para buscar tarefas reais das ferramentas:

### O que você vai precisar

- **ClickUp API Key**: Settings → Apps → API Token
- **Linear API Key**: Settings → API → Personal API keys

### Como conectar (sem backend, 100% frontend)

O dashboard pode fazer fetch direto das APIs no browser.
Adicione ao `config.json`:

```json
"_integracao": {
  "clickup_list_id": "123456789",
  "linear_team_id": "766c0e4e-8458-4146-98d8-8a50a17f32f5"
}
```

**As API keys NÃO ficam no config.json.**
Elas ficam salvas no `localStorage` do browser, digitadas uma única vez:

```
Primeira abertura → aparece um modal pedindo as keys
Keys ficam salvas localmente → nunca sobem para o GitHub
```

Posso implementar essa camada quando quiser. É 1 sessão de trabalho.

### Sync automático a cada 5 minutos

Já está implementado no código. O botão `sync` no header força um refresh manual.
O próximo passo é fazer o sync buscar dados reais das APIs ao invés do `config.json`.

---

## Modo privado

Clique no botão **👁 tudo visível** no header para ciclar entre:
- 👁 **tudo visível** — padrão
- 💼 **só trabalho** — esconde tudo pessoal (anel, Carla, flores, etc.)
- ❤ **só pessoal** — esconde tudo profissional (time, riscos, decisões, etc.)

O estado **não é salvo** entre sessões por segurança. Cada abertura começa com tudo visível.

---

## Problemas comuns

| Problema | Solução |
|---|---|
| Página não atualiza após editar config.json | Aguarde 1-2min ou force Ctrl+Shift+R no browser |
| GitHub Pages mostra 404 | Verifique se o arquivo se chama exatamente `index.html` |
| Icons não aparecem | Verifique conexão com internet (Tabler Icons carrega via CDN) |
| Layout quebrado no celular | Dashboard foi feito para desktop, tela mínima ~1200px |

