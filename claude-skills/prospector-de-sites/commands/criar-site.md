---
description: Cria sites do zero (estética premium) para leads que não têm site próprio
argument-hint: "[nomes dos leads] — opcional, usa os leads tipo criacao mais bem ranqueados de leads.md"
---

Crie páginas novas do zero para leads sem site próprio seguindo a skill `criacao-premium`. Ela é obrigatória — leia a skill ANTES de escrever qualquer HTML. Este comando é o equivalente do `/redesenhar` para leads `tipo: criacao` (sem site) — mesma qualidade, mesma entrega, fonte de conteúdo diferente.

## Seleção dos clientes

1. Leia `prospector-config.json` e `leads.md` na pasta conectada.
2. Se `$ARGUMENTS` trouxer nomes, use-os (confirme que são `tipo: criacao`; se algum tiver site próprio, avise e sugira `/redesenhar` pra ele). Senão, selecione os leads `tipo: criacao` com status `novo` mais bem ranqueados — mínimo de 5 clientes por lote (se houver menos de 5, use todos e avise que rodar `/prospectar` de novo aumenta o lote).
3. Confirme a lista com o usuário antes de começar.

## Para cada cliente do lote

1. **Coleta (via Claude in Chrome, perfil do Google Maps — não há site pra extrair)**: abra o perfil do negócio no Google Maps. Colete categoria/especialidade, endereço completo, horários, telefone/WhatsApp, nota + nº de avaliações, 2-3 avaliações reais em destaque, e TODAS as fotos da aba "Fotos" (role até o fim, colete as URLs via `img.currentSrc`). Se o negócio tiver Instagram/Facebook público, abra também e colete fotos e conteúdo adicionais. Sem essa coleta completa, não prossiga.
2. **Criação**: aplique a skill `criacao-premium` na íntegra. Regra de ouro: NADA inventado — só o que veio do perfil do Maps ou da rede social real do negócio. Fotos genéricas de banco de imagens são PROIBIDAS. Sem logo → wordmark tipográfico, nunca símbolo inventado.
3. **Salvar** na pasta conectada, com o nome do cliente no arquivo:
   - `sites/[slug]/[slug].html` — a página final (arquivo único, autocontido, responsivo)
   - `sites/[slug]/[slug]-editor.html` — a MESMA página com a camada de edição visual injetada antes de `</body>` (script em `references/editor-visual.md` da skill `redesign-premium`, reutilizado pela `criacao-premium`). Gere SEMPRE, sem esperar o usuário pedir.
4. **Comparador (OBRIGATÓRIO — não é opcional)**: crie/atualize `comparar.html` na RAIZ da pasta conectada usando `references/comparador-template.html` da skill `redesign-premium`. Para este cliente, use `"old": null` e `"motivo": "Ainda não tinha site — esta é a primeira versão"` no array JSON — o template já mostra o cartão correto sozinho. Se `comparar.html` já existir, LEIA o array atual e acrescente os novos no topo — nunca perca os antigos.
5. **Atualizar** o status do lead em `leads.md` para `redesenhado` (mesmo funil dos leads com site — aqui significa "página pronta") e o `dashboard.html` (skill `dashboard-leads`), mantendo `tipo: criacao`.

## Checklist de saída (bloqueante)

Antes de apresentar qualquer resultado ao usuário, confirme que TODOS estes arquivos existem — se faltar algum, gere-o agora:

- [ ] `sites/[slug]/[slug].html` para CADA cliente do lote
- [ ] `sites/[slug]/[slug]-editor.html` para CADA cliente do lote
- [ ] `comparar.html` na raiz, com abas para TODOS os clientes do lote (com o card "sem site anterior" correto)

Um site sem o editor ou sem o comparador é entrega incompleta.

## Verificação do lote

Antes de encerrar, para cada página criada: renderize/revise o HTML procurando textos placeholder esquecidos, links quebrados, seções vazias, foto genérica (deve ser só foto real do perfil/rede social) e problemas de contraste. Todos os CTAs devem apontar para o WhatsApp ou contato REAL do cliente.

## Saída (TRAVADA — siga exatamente este formato)

A entrega final ao usuário DEVE conter, nesta ordem, sem exceção:

1. **Cards de arquivo apresentados no chat** (via ferramenta de apresentação de arquivos): o `comparar.html` PRIMEIRO, depois a página e o editor de cada cliente. Se você não apresentou o card do `comparar.html`, a entrega está errada — apresente antes de escrever qualquer resumo.
2. **Resumo de 1 linha por cliente** (o conceito/proposta visual usada, já que não há "antes" pra comparar).
3. **Confirmação do dashboard**: frase explícita "Dashboard atualizado: [N] leads com status redesenhado" após atualizar o banco/dashboard conforme a skill `dashboard-leads` (se a pasta ainda não tem dashboard, CRIE-o agora — pasta nova nunca é desculpa para pular).
4. Orientação curta: `comparar.html` = ver a primeira versão do site · `[slug]-editor.html` = editar textos/imagens · próximo passo `/publicar`.

É PROIBIDO encerrar a resposta sem os itens 1 e 3. Se qualquer arquivo do checklist não existir, gere-o antes de responder.
