---
name: prospector-de-sites
description: >-
  Prospecção semi-automática de clientes com sites ruins: acha negócios no
  Google Maps, redesenha páginas premium, publica na Hostinger e envia proposta
  por e-mail. Use quando o usuário disser "prospector", "prospectar", "redesenhar
  site do cliente", "publicar na hostinger", "proposta de site", "setup prospector"
  ou mencionar o ciclo achou → refez → publicou → ofertou.
---

# Prospector de Sites (Cursor)

Ciclo completo de prospecção e venda de sites:

**Achou → Refez → Publicou → Ofertou.**

## Como invocar no Cursor

Não há slash commands como no Claude. Peça ao agente em linguagem natural:

| Etapa | Exemplo de prompt |
|-------|-------------------|
| Setup (1x) | "Rode o setup do prospector de sites" |
| Prospectar | "Prospectar nutricionistas em São Paulo" |
| Redesenhar | "Redesenhar os 5 melhores leads" |
| Editor | "Abrir editor do cliente jessica-nutri" |
| Publicar | "Publicar todos os sites na Hostinger" |
| Proposta | "Enviar proposta para todos os publicados" |

O agente deve ler o workflow correspondente em [workflows/](workflows/) e a skill de domínio indicada.

## Pasta de trabalho

Todos os dados ficam em **`prospector-data/`** na raiz do workspace (ou caminho definido no setup):

```
prospector-data/
├── prospector-config.json
├── leads.md
├── leads.csv
├── comparar.html
└── sites/[slug]/
    ├── [slug].html
    ├── [slug]-editor.html
    └── preview.png
```

Se o workspace não tiver pasta definida, pergunte ao usuário onde salvar e registre em `prospector-config.json` → `"pastaTrabalho"`.

## Ferramentas do Cursor (substituem Claude)

| Antes (Claude) | No Cursor |
|----------------|-----------|
| Claude in Chrome | MCP `cursor-ide-browser` (`browser_navigate`, `browser_snapshot`, `browser_click`, `browser_scroll`, `browser_take_screenshot`, `browser_cdp` com `Runtime.evaluate`) |
| AskUserQuestion | `AskQuestion` |
| Conector Google Drive / Sheets | `leads.md` + `leads.csv` local (exportar CSV para o usuário subir no Sheets se quiser) |
| Conector Gmail | Browser no Gmail web (rascunho) ou MCP Resend se configurado |
| Pasta conectada Cowork | `prospector-data/` no workspace |

## Workflows

1. **[setup](workflows/setup.md)** — configura assinatura, nichos e Hostinger (roda uma vez)
2. **[prospectar](workflows/prospectar.md)** — busca leads no Maps → skill `prospeccao-maps`
3. **[redesenhar](workflows/redesenhar.md)** — redesign premium → skill `redesign-premium`
4. **[editor](workflows/editor.md)** — gera versão editável no navegador
5. **[publicar](workflows/publicar.md)** — deploy Hostinger → skill `deploy-hostinger`
6. **[proposta](workflows/proposta.md)** — e-mail de proposta → skill `proposta-email`

## Requisitos

- MCP **cursor-ide-browser** habilitado (prospecção no Maps, extração de sites, fallback hPanel)
- Hospedagem **Hostinger** com acesso ao hPanel/FTP (ou preencher deploy manualmente)
- Conta **Gmail** para rascunhos de proposta (via browser)

## Segurança

A senha FTP **nunca** é digitada no chat. O usuário preenche `"senha"` em `prospector-config.json` localmente.
