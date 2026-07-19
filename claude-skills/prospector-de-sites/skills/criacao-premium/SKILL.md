---
name: criacao-premium
description: Esta skill deve ser usada ao criar um site do ZERO para um lead prospectado que NÃO tem site próprio — montar uma landing page premium e de alta conversão a partir do perfil do Google Maps (fotos, avaliações, categoria, endereço), sem site original pra extrair conteúdo. Acione quando o usuário disser "criar site", "gerar site do zero", "cliente não tem site", "fazer site novo" ou rodar /criar-site.
---

# Criação premium de páginas do zero

Criar o PRIMEIRO site do negócio — não existe "antes" pra preservar, só o negócio real por trás. A página precisa parecer que uma agência premium foi contratada pelo próprio cliente, usando só o material que ele realmente tem (fotos, avaliações, dados do perfil).

Esta skill é irmã da `redesign-premium`: mesma barra de qualidade estrutural, mesmo editor visual, mesmo comparador — a única diferença é a FONTE do conteúdo (perfil do Google Maps em vez de site existente) e que não há "antes" pra comparar.

## Regras invioláveis

1. **Nenhum FATO inventado.** Toda informação (serviços, especialidade, endereço, telefone, horários) vem do perfil do Google Maps do negócio (ou de redes sociais públicas, se houver) — nunca de suposição. Sem depoimento fabricado, sem serviço que o negócio não anuncia, sem prêmio ou credencial não verificável.
2. **Fotos reais são OBRIGATÓRIAS.** Toda foto usada é do perfil do Google Maps do negócio (aba "Fotos", coletada via `img.currentSrc` no navegador, rolando até o fim) ou de uma rede social pública do próprio negócio. PROIBIDO usar banco de imagens genérico (Unsplash, stock photo) para fachada, equipe ou ambiente — o cliente precisa se reconhecer. Exceção: ícones/ilustrações decorativas de apoio (não substituem foto real de prova social).
3. **Sem logo → composição tipográfica.** Se o negócio não tem logo, NUNCA inventar um símbolo/ícone como se fosse a marca — usar o nome do negócio em tipografia forte (wordmark) como identidade visual do cabeçalho.
4. **Profissional desde o dia 1.** Por não ter site anterior, este É o padrão de qualidade do negócio daqui pra frente — nenhuma seção pode parecer "provisória" ou "básica". Estrutura completa: hero, prova social, serviços, sobre, localização, contato — só com seções cujo conteúdo é sustentado por fato real coletado.
5. **Arquivo único.** `sites/[slug]/[slug].html` autocontido: CSS inline no `<head>`, sem build, sem dependências além de Google Fonts.
6. **Responsividade TOTAL (inegociável).** Perfeita em 360, 375, 768, 1024, 1280 e 1440px — sem rolagem horizontal, sem texto vazando, sem imagem esticada, sem seção quebrada em nenhum desses pontos.
7. **Editor sempre.** Todo site gera junto o `sites/[slug]/[slug]-editor.html` (camada de edição de `../redesign-premium/references/editor-visual.md` — reutilizada da skill `redesign-premium`) — nunca entregar página sem a versão editável.
8. **Comparador com aba própria.** Todo lote termina com `comparar.html` na raiz da pasta conectada, gerado a partir de `../redesign-premium/references/comparador-template.html`. O template já suporta cliente sem site antigo nativamente (`"old": null, "motivo": "..."`) — ver seção abaixo.

## Coleta obrigatória antes de escrever qualquer HTML

Fonte é o perfil do Google Maps do negócio (via Claude in Chrome), não um site:

- Nome exato do negócio, categoria/especialidade, nota e nº de avaliações.
- Endereço completo, bairro, horários de funcionamento.
- Telefone e WhatsApp (ver skill `prospeccao-maps` para como identificar o WhatsApp).
- Todas as fotos da aba "Fotos" do perfil (role até o fim antes de coletar as URLs — sem lazy-load pra vencer aqui, é scroll normal da aba).
- 2-3 avaliações reais em destaque (as mais específicas e elogiosas).
- Se existir uma rede social pública ativa (Instagram/Facebook) do negócio: nome de usuário, bio, mais fotos e eventuais serviços/produtos citados — usar como fonte adicional de conteúdo real, nunca como "site atual".

Sem essa coleta completa, não escrever a página — falta material real pra preencher com honestidade.

## Estrutura da página (adaptar à profissão)

1. **Hero**: nome do negócio (wordmark se sem logo) + especialidade, promessa clara em 1 linha, CTA primário (WhatsApp) visível sem rolar, melhor foto real do ambiente/equipe/produto.
2. **Prova social**: nota do Google em destaque ("5.0 ★ · 121 avaliações no Google") + 2-3 trechos reais de avaliação.
3. **Serviços/áreas de atuação**: cards clicáveis, cada um levando ao WhatsApp com mensagem pré-preenchida (`https://wa.me/55DDDNUMERO?text=Olá! Vi o [negócio] no Google e quero saber sobre [serviço]`). Só listar o que é deduzível da categoria/perfil/rede social real.
4. **Sobre**: história/proposta do negócio, só com o que é verificável (categoria, tempo de atuação se público, especialização).
5. **Localização e contato**: endereço, mapa (iframe do Google Maps), horários reais do perfil, telefone.
6. **Rodapé**: dados de contato consolidados.

Não criar seção que exigiria inventar fato (ex.: "nossa equipe" sem fotos/nomes reais de equipe) — pular a seção é sempre preferível a inventar.

## Copywriting (o mesmo rigor da redesign-premium)

- **Headline do hero = benefício, não rótulo.** Rótulo vira kicker/subtítulo.
- **Estrutura PAS suave**, tom do nicho, sem agressividade de lançamento.
- **Escaneabilidade**: blocos curtos, bullets com verbo, subtítulos que contam a história sozinhos.
- **1 CTA por dobra**, todos pro WhatsApp com mensagem pré-preenchida contextual.
- **Prova social costurada** perto do CTA e da seção correspondente.
- Proibido: clichês vazios, superlativos inventados, promessas que o negócio não faz.

## Barra de qualidade estrutural

Mesma régua da `redesign-premium`: grid consistente, alinhamento impecável, alternância de ritmo entre seções, imagens com tratamento coerente (mesmo raio de borda, mesma temperatura), tipografia com no máximo 2 famílias e escala harmônica, nenhuma seção órfã.

## Padrão estético

Idêntico à `redesign-premium`: serifada elegante pro título + sans limpa pro corpo, espaçamento generoso (80-120px entre seções desktop), paleta com 1 cor de destaque + neutros quentes (se o negócio não tiver identidade visual prévia, escolher uma paleta coerente com o nicho — clínica = tons quentes/confiáveis, estética = tons suaves, etc. — e documentar a escolha no resumo entregue ao usuário), botão de WhatsApp flutuante, micro-toques premium (bordas 12-16px, sombras suaves, transições 0.2s), zero JS além do essencial.

## Comparador para leads sem site anterior

No array JSON do `comparar.html`, este cliente entra com `"old": null` e `"motivo": "Ainda não tinha site — esta é a primeira versão"` (tom neutro, nunca constranger o cliente) — o template já renderiza automaticamente um cartão "Sem site para comparar" com esse texto no lugar do iframe do site antigo. Não é preciso alterar o template.

## Checklist final (obrigatório antes de entregar)

- [ ] Zero texto placeholder / lorem ipsum
- [ ] Todas as fotos são reais (perfil do Maps ou rede social do negócio) — nenhuma de banco de imagens
- [ ] Todos os links e CTAs apontam para contato REAL do cliente
- [ ] Número do WhatsApp no formato wa.me correto (55 + DDD + número)
- [ ] Responsivo verificado em 360, 375, 768, 1024, 1280 e 1440px — zero rolagem horizontal e zero quebra em TODAS
- [ ] Título e meta description preenchidos com nome + especialidade + cidade
- [ ] Nenhuma seção com fato inventado — cada afirmação rastreável até o perfil do Maps ou rede social coletada
- [ ] `[slug]-editor.html` gerado e `comparar.html` atualizado (com o card "sem site anterior" no lugar do antigo)

## Editor visual e comparador (reutilizados da redesign-premium)

A camada de edição visual está em `../redesign-premium/references/editor-visual.md` — injetar exatamente como documentado lá. O comparador está em `../redesign-premium/references/comparador-template.html` — mesmo processo de merge do array JSON, com o ajuste do card "sem site anterior" descrito acima.
