# Prospector de Sites

Prospecção semi-automática de clientes com sites ruins ou sem site: acha, redesenha (ou cria do zero), publica e oferta.

Versão **0.15.0** — com CRM local, página-capa, proposta por e-mail e WhatsApp, follow-up, respostas e contrato.

## Estrutura

| Pasta | Plataforma | Documentação |
|-------|------------|--------------|
| [`cursor-skills/`](cursor-skills/) | Cursor | [README](cursor-skills/README.md) |
| [`claude-skills/`](claude-skills/) | Claude (Cowork / Claude Code) | [README](claude-skills/README.md) |

## Ciclo

**Achou → Refez (ou criou do zero) → Publicou → Ofertou**

1. Setup — configuração + dashboard + publicador
2. Prospectar — Google Maps (site fraco ou sem site)
3. Redesenhar — páginas premium (leads com site) / Criar site — do zero (leads sem site)
4. Publicar — Hostinger + capa de proposta
5. Proposta — e-mail e WhatsApp anti-spam
6. Respostas — monitora Gmail
7. Follow-up — após 3+ dias (e-mail e/ou WhatsApp)
8. Contrato — HTML + DOCX

## Instalação rápida (Cursor)

```bash
git clone git@github.com:lucasgpaixao/PROSPECTOR-DE-SITES.git
cp -r cursor-skills/* ~/.cursor/skills/
```

## Instalação rápida (Claude)

```
/plugin marketplace add lucasgpaixao/PROSPECTOR-DE-SITES
/plugin install prospector-de-sites@prospector-plugins
```

---

Lucas Paixão
