---
name: prospector-de-sites
description: >-
  Prospecção semi-automática de clientes com sites ruins ou sem site: acha
  negócios no Google Maps, redesenha páginas premium ou cria sites do zero,
  publica na Hostinger, envia proposta anti-spam por e-mail e WhatsApp,
  acompanha respostas, follow-up e contrato. Use quando o usuário disser
  "prospector", "prospectar", "redesenhar", "criar site", "publicar",
  "proposta", "whatsapp", "respostas", "followup", "contrato", "dashboard" ou
  o ciclo achou → refez → publicou → ofertou.
---

# Prospector de Sites (Cursor) v0.15.0

Ciclo completo de prospecção e venda de sites:

**Achou → Refez (ou criou do zero) → Publicou → Ofertou** (+ respostas, follow-up, contrato)

## Como invocar

| Etapa | Exemplo de prompt |
|-------|-------------------|
| Setup (1x) | "Rode o setup do prospector de sites" |
| Prospectar | "Prospectar nutricionistas em Campinas" |
| Redesenhar | "Redesenhar os 5 melhores leads" |
| Criar site | "Criar o site dos leads sem site" |
| Editor | "Abrir editor do cliente jessica-nutri" |
| Publicar | "Publicar todos os sites na Hostinger" |
| Proposta | "Enviar proposta para os publicados" |
| Respostas | "Verificar respostas das propostas" |
| Follow-up | "Gerar follow-up dos que não responderam" |
| Contrato | "Gerar contrato do cliente fechado" |

Leia o workflow em [workflows/](workflows/) e a skill de domínio indicada.

## Pasta de trabalho

`prospector-data/` na raiz do workspace:

```
prospector-data/
├── prospector-config.json
├── prospector.db              # CRM SQLite (fonte da verdade)
├── dashboard.html
├── dashboard-server.py
├── iniciar-dashboard.bat
├── manual.html
├── comparar.html
├── fila-publicacao.txt        # Publicador automático
├── leads.md                   # Cópia de trabalho
├── leads.csv
└── sites/[slug]/
    ├── [slug].html
    ├── [slug]-editor.html
    ├── proposta.html          # Página-capa (único link do e-mail)
    └── contrato-[slug].docx
```

## Skills

| Skill | Função |
|-------|--------|
| `prospeccao-maps` | Busca no Google Maps (site fraco ou sem site) |
| `redesign-premium` | Redesign de site existente + editor + comparador |
| `criacao-premium` | Site do zero (leads sem site) + editor + comparador |
| `deploy-hostinger` | Publicação FTP/hPanel/publicador |
| `proposta-email` | E-mail e WhatsApp anti-spam com capa |
| `dashboard-leads` | CRM local (kanban, financeiro, contratos) |
| `contrato-servico` | Contrato HTML + DOCX |

## Workflows

1. [setup](workflows/setup.md) → `dashboard-leads` + `deploy-hostinger`
2. [prospectar](workflows/prospectar.md) → `prospeccao-maps` + `dashboard-leads`
3. [redesenhar](workflows/redesenhar.md) → `redesign-premium` (leads com site)
3b. [criar-site](workflows/criar-site.md) → `criacao-premium` (leads sem site)
4. [editor](workflows/editor.md) → `redesign-premium`
5. [publicar](workflows/publicar.md) → `deploy-hostinger` + `proposta-email`
6. [proposta](workflows/proposta.md) → `proposta-email` (e-mail + WhatsApp)
7. [respostas](workflows/respostas.md) → `dashboard-leads`
8. [followup](workflows/followup.md) → `proposta-email`
9. [contrato](workflows/contrato.md) → `contrato-servico`

## Ferramentas Cursor

| Claude | Cursor |
|--------|--------|
| Claude in Chrome | MCP `cursor-ide-browser` |
| Conector Gmail | Gmail via browser |
| WhatsApp Web | MCP `cursor-ide-browser` (mensagem pronta, você clica em enviar) |
| Google Sheets | `leads.csv` + import manual |
| Pasta Cowork | `prospector-data/` |

## Requisitos

- MCP **cursor-ide-browser**
- **Hostinger** com hPanel/FTP
- **Gmail** para rascunhos
- **Python** (dashboard + contrato DOCX)
- **Windows** (publicador automático `.bat`/`.ps1`)

## Segurança

Senha FTP só em `prospector-config.json` — nunca no chat. Preencher no dashboard (aba Configurações) ou no arquivo local.

## Manual

Após o setup, abra [manual.html](manual.html) — responde 90% das dúvidas do usuário.
