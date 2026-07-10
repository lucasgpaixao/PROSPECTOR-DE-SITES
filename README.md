# Prospector de Sites

Prospecção semi-automática de clientes com sites ruins: acha, redesenha, publica e oferta.

Versão **0.13.5** — com CRM local, página-capa, follow-up, respostas e contrato.

## Estrutura

| Pasta | Plataforma | Documentação |
|-------|------------|--------------|
| [`cursor-skills/`](cursor-skills/) | Cursor | [README](cursor-skills/README.md) |
| [`claude-skills/`](claude-skills/) | Claude (Cowork / Claude Code) | [README](claude-skills/README.md) |

## Ciclo

**Achou → Refez → Publicou → Ofertou**

1. Setup — configuração + dashboard + publicador
2. Prospectar — Google Maps
3. Redesenhar — páginas premium
4. Publicar — Hostinger + capa de proposta
5. Proposta — e-mail anti-spam
6. Respostas — monitora Gmail
7. Follow-up — após 3+ dias
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
