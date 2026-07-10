# Workflow: Redesenhar

Redesenhe as páginas dos leads seguindo a skill `redesign-premium`. Leia a skill ANTES de escrever qualquer HTML.

## Seleção dos clientes

1. Leia `prospector-config.json` e `leads.md` na pasta de trabalho.
2. Se o usuário informar URLs ou nomes, use-os. Senão, selecione leads com status `novo` mais bem ranqueados — **mínimo de 5 clientes por lote** (se houver menos, use todos e avise).
3. Confirme a lista com o usuário antes de começar.

## Para cada cliente do lote

1. **Extração**: abra o site original via MCP `cursor-ide-browser` (fetch direto costuma falhar em domínios de terceiros). Extraia TODO o conteúdo real. Use `browser_cdp` → `Runtime.evaluate` para coletar `img.currentSrc` de todas as imagens (role a página até o fim para lazy-load). `browser_take_screenshot` do site original.
2. **Redesign**: aplique a skill `redesign-premium` na íntegra. Regra de ouro: NADA inventado.
3. **Salvar** na pasta de trabalho:
   - `sites/[slug]/[slug].html` — página final autocontida
   - `sites/[slug]/[slug]-editor.html` — mesma página com camada de edição (script em `redesign-premium/references/editor-visual.md`)
4. **Comparador (OBRIGATÓRIO)**: crie/atualize `comparar.html` na raiz usando `redesign-premium/references/comparador-template.html`. Se já existir, leia o array atual e acrescente novos clientes no topo.
5. **Atualizar** status em `leads.md` para `redesenhado`.

## Checklist de saída (bloqueante)

- [ ] `sites/[slug]/[slug].html` para CADA cliente
- [ ] `sites/[slug]/[slug]-editor.html` para CADA cliente
- [ ] `comparar.html` na raiz com abas para TODOS os clientes do lote

## Verificação

Para cada página: textos placeholder, links quebrados, seções vazias, contraste. CTAs apontam para WhatsApp REAL do cliente.

## Saída

Resumo de 1 linha por cliente. Oriente: abrir `comparar.html` para antes/depois, `[slug]-editor.html` para editar. Sugira publicar na HostGator.
