# Prospector de Sites — Claude Skills

Plugin para **Claude** (Cowork / Claude Code) que roda o ciclo completo de prospecção e venda de sites:

**Achou → Refez → Publicou → Ofertou.**

1. `/setup` — configura assinatura, nichos e Hostinger (roda uma vez)
2. `/prospectar` — varre o Google Maps atrás de negócios bem avaliados (nota ≥ 4.7) com site ruim e e-mail público
3. `/redesenhar` — recria as páginas com estética premium, editor visual e comparador antes/depois
4. `/editor` — edita textos e imagens no navegador e exporta a versão final
5. `/publicar` — sobe as páginas na Hostinger e devolve as URLs públicas
6. `/proposta` — escreve o e-mail de proposta (rapport real, sem preço) e cria rascunho no Gmail

## Como instalar

No Claude Code:

```
/plugin marketplace add lucasgpaixao/PROSPECTOR-DE-SITES
/plugin install prospector-de-sites@prospector-plugins
```

No Claude Cowork (desktop): Configurações → Plugins → Adicionar marketplace → cole a URL do repositório → instale o **prospector-de-sites**.

## Requisitos

- Claude Cowork (ou Claude Code) com extensão Claude in Chrome conectada
- Conector do Gmail e do Google Drive
- Uma pasta conectada no Cowork (config, leads e sites ficam nela)
- Hospedagem Hostinger com acesso ao hPanel/FTP

## Onde ficam os dados

Tudo na pasta conectada: `prospector-config.json`, `leads.md`, `sites/[slug]/` e `comparar.html`.

## Segurança

A senha FTP nunca é digitada no chat: preencha o campo `"senha"` em `prospector-config.json` localmente.

---

Lucas Paixão
