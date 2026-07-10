# Prospector de Sites

Prospecção semi-automática de clientes com sites ruins: acha, redesenha, publica e oferta.

Versões para **Cursor** e **Claude** do fluxo de prospecção e venda de sites.

## Estrutura

| Pasta | Plataforma | Documentação |
|-------|------------|--------------|
| [`cursor-skills/`](cursor-skills/) | Cursor | [README](cursor-skills/README.md) |
| [`claude-skills/`](claude-skills/) | Claude (Cowork / Claude Code) | [README](claude-skills/README.md) |

## Ciclo

**Achou → Refez → Publicou → Ofertou**

1. Setup — configuração inicial
2. Prospectar — busca leads no Google Maps
3. Redesenhar — páginas premium com editor e comparador
4. Publicar — deploy na Hostinger
5. Proposta — e-mail comercial (sem preço)

## Instalação rápida (Cursor)

```bash
git clone git@github.com:lucasgpaixao/PROSPECTOR-DE-SITES.git
cp -r cursor-skills/* ~/.cursor/skills/
```

## Instalação rápida (Claude)

```
/plugin marketplace add <seu-usuario>/PROSPECTOR-DE-SITES
/plugin install prospector-de-sites@arrecheneto-plugins
```

---

Lucas Paixão
