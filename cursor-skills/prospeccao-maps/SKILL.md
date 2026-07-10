---
name: prospeccao-maps
description: >-
  Prospecta clientes no Google Maps — busca negócios bem avaliados com sites
  ruins, qualifica leads e monta planilha. Use quando o usuário disser
  "prospectar", "buscar clientes", "achar leads", "clientes com site ruim"
  ou rodar o workflow prospectar do prospector de sites.
---

# Prospecção no Google Maps

Encontrar negócios com boa reputação mas presença digital fraca. O contraste entre nota alta e site ruim É o argumento de venda.

## Ferramentas (Cursor)

Use o MCP **cursor-ide-browser**:

- `browser_navigate` — abrir Maps e sites
- `browser_snapshot` — ler painéis e resultados
- `browser_click` — selecionar estabelecimentos
- `browser_scroll` — percorrer resultados e lazy-load
- `browser_cdp` → `Runtime.evaluate` — extrair e-mails via regex no HTML
- `browser_take_screenshot` — capturas de referência

## O perfil do lead ideal

- Nota **≥ 4.7** com **≥ 40 avaliações**
- **Site próprio ATIVO, mas ruim** — requisito eliminatório
- **E-mail público** — requisito eliminatório
- Nichos: profissionais liberais (nutricionistas, psicólogos, advogados, psiquiatras, dentistas, fisioterapeutas)

## Os 3 filtros eliminatórios (nesta ordem)

1. **Sem site próprio → PULA.** Não conta: Instagram/Facebook, WhatsApp, Doctoralia, iFood, Linktree, site fora do ar.
2. **Site BOM → PULA.** Moderno, responsivo, bem estruturado.
3. **Sem e-mail público → PULA.** Busque no perfil Maps, site (contato, rodapé) e via JavaScript.

## Fluxo de execução

1. `browser_navigate` → `https://www.google.com/maps/search/[nicho]+em+[cidade]`
2. Percorrer resultados, abrindo painel de cada estabelecimento
3. Anotar nota e avaliações; corte ≥ 4.7 / ≥ 40
4. Verificar site no perfil; Filtro 1
5. Abrir site em nova aba; avaliar qualidade; Filtro 2
6. Caçar e-mail; Filtro 3
7. Coletar: nome, nota, avaliações, telefone/WhatsApp, e-mail, URL, motivo do site ruim, 2-3 trechos de avaliações reais
8. Repetir até meta de leads ou 25 estabelecimentos

## Como avaliar qualidade do site

Site RUIM apresenta 2+ destes sinais:

- Não responsivo
- Design datado
- Sem hierarquia visual
- Sem CTA claro na primeira dobra
- Lento/pesado
- Conteúdo abandonado (copyright antigo, links quebrados)
- Template genérico mal preenchido

Registrar motivo específico e verificável — vira argumento do e-mail.

## Saída

1. **`leads.md`** na pasta de trabalho: todos avaliados, ranqueados por potencial. Colunas: #, Nome, Nota, Avaliações, E-mail, Telefone, Site atual, Motivo, Situação, Status, URL nova.
2. **`leads.csv`**: mesmos dados para importação no Google Sheets.

## Boas práticas

- Nunca reavaliar estabelecimento já em `leads.md`
- Rodadas novas somam na mesma lista, nunca duplicar
- Não coletar dados além do necessário para a proposta
- Fechar abas após cada análise
- Se poucos resultados, sugerir nicho alternativo ou cidade vizinha
