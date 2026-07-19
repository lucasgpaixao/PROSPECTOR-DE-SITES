---
name: proposta-email
description: Esta skill deve ser usada ao escrever e enviar a proposta comercial por e-mail E/OU WhatsApp para um lead prospectado — mensagem de apresentação da nova versão do site (leads com site) ou do site novo (leads sem site), com rapport e sem preço. Acione quando o usuário disser "enviar proposta", "e-mail para o cliente", "mandar o site para o cliente", "mandar no zap", "proposta por whatsapp" ou rodar /proposta ou /followup.
---

# Proposta por e-mail e WhatsApp

A proposta NÃO vende — ela desperta curiosidade e prova trabalho feito. O fechamento (preço, escopo, reunião) acontece na resposta. Uma mensagem que parece de vendedor morre no spam (e-mail) ou é ignorada (WhatsApp); uma mensagem que parece de uma pessoa que já trabalhou de graça pro destinatário é aberta e respondida.

Os dois canais são enviados para o mesmo lote de leads, sempre que o dado existir: **e-mail sempre que houver e-mail confirmado, WhatsApp sempre que houver WhatsApp capturado na prospecção** (a maioria dos leads tem os dois — mandar nos dois aumenta a chance de resposta, sem ser redundante porque cada canal tem seu próprio tom).

## Princípios (valem para e-mail E WhatsApp)

1. **Rapport primeiro.** Abrir com elogio ESPECÍFICO e verificável: a nota no Google, uma avaliação real citada, uma credencial do site. Nunca elogio genérico.
2. **A dor sem ofensa.** Apontar 1-2 defeitos objetivos do site atual como oportunidade ("notei que no celular o site fica difícil de ler"), nunca como crítica ao profissional.
3. **A prova antes do pedido.** O trabalho JÁ está feito e no ar. O link é a proposta.
4. **Zero preço.** Preço só na conversa que a resposta abre.
5. **Zero pressão.** Sem urgência falsa, sem "últimas vagas". Um único CTA: dar uma olhada e responder o que achou.
6. **Curto.** E-mail: 120-180 palavras. WhatsApp: 3-5 linhas — mensagem de zap longa não é lida, é ignorada.
7. **Canais independentes, mesma verdade.** Quem recebe os dois não pode sentir que levou a mesma mensagem colada duas vezes — o conteúdo factual é o mesmo, a redação e o tom são reescritos para cada canal (e-mail = mais formal/estruturado; WhatsApp = mais direto/conversacional, como uma mensagem que um conhecido mandaria).

## E-mail — Estrutura

A estrutura muda no parágrafo 2 e 3 conforme o `tipo` do lead (`redesign` ou `criacao`, ver `leads.md`/dashboard) — os demais parágrafos são iguais.

- **Assunto**: pergunta pessoal e específica, ≤ 60 caracteres, sem cara de marketing. Ex.: `Dra. [Nome], posso te mostrar uma coisa sobre seu site?` (redesign) ou `Preparei um site para a [Clínica X]` (criação).
- **Parágrafo 1**: quem encontrou + elogio específico (avaliações/credencial). Igual pros dois tipos.
- **Parágrafo 2**:
  - **`tipo: redesign`** — observação sobre o site atual (1-2 pontos objetivos, sem ofensa).
  - **`tipo: criacao`** — observação de oportunidade, nunca de falta: "reparei que a [empresa] ainda não tem um site próprio — quem busca no Google acaba não te achando, apesar da nota e do movimento que vocês já têm" (tom de quem viu uma oportunidade, não de quem aponta uma falha).
- **Parágrafo 3**:
  - **`tipo: redesign`** — "preparei uma nova versão, já no ar" + O ÚNICO LINK do e-mail: a página-capa (`.../proposta.html`), que mostra antes e depois lado a lado. Se a capa não existir, linkar a página nova direto.
  - **`tipo: criacao`** — "preparei um site pra vocês, já no ar, com fotos e avaliações reais do perfil de vocês no Google" + O ÚNICO LINK do e-mail: a página-capa (`.../proposta.html`), aqui em versão de apresentação única (sem toggle antes/depois, já que não havia site anterior).
- **Parágrafo 4**: CTA — abrir no celular também, responder com a impressão.
- **Assinatura**: nome, apresentação e WhatsApp do config (assinatura completa humaniza e reduz suspeita).

## E-mail — Checklist anti-spam (BLOQUEANTE — rodar antes de criar o rascunho)

Revise o e-mail pronto contra CADA item; se falhar em qualquer um, reescreva antes de criar o rascunho:

- [ ] **1 link só** (a página-capa). Dois links no máximo se incluir o site antigo — nunca mais que isso.
- [ ] **Sem encurtador de URL** (bit.ly e afins = spam na certa). O link é o domínio real, com `https://`.
- [ ] **Link como âncora HTML com texto visível limpo.** O Gmail embrulha TODO link em um redirect próprio (`google.com/url?q=...`) ao salvar — não dá pra impedir, e em corpo de texto puro o embrulho fica VISÍVEL, o que parece golpe. Por isso o rascunho é criado com corpo HTML e o link como âncora: `<a href="https://[dominio]/[pastaBase]/[slug]/proposta.html">https://[dominio]/[pastaBase]/[slug]/proposta.html</a>` — texto visível = a URL limpa montada a partir do config (nunca copiada de outro e-mail). O redirect do Google fica só no href invisível, como em qualquer e-mail do Gmail. Depois de criar, confira o rascunho: o texto visível deve começar em `https://[dominio do config]`.
- [ ] **Domínio limpo e humano.** Se o domínio do config for um subdomínio técnico/temporário (cheio de números, tipo `nome1783367206076.1711244.meusitehostinger.com.br`), PARE antes de enviar qualquer proposta: link assim parece golpe e mata a confiança que a capa constrói. Oriente o usuário a ativar o domínio próprio (grátis no plano da Hostinger: hPanel → Domains, ou registro em registro.br) e atualizar o campo `dominio` nas Configurações do dashboard. Proposta só sai com domínio apresentável.
- [ ] **Sem palavras-gatilho**: grátis, promoção, imperdível, oferta, desconto, clique aqui, 100%, garantido, urgente.
- [ ] **Sem CAIXA ALTA no assunto, sem "!!", sem emoji** no assunto.
- [ ] **Texto simples** — corpo HTML minimalista (só parágrafos e a âncora do link; zero cores, botões, imagens ou anexos) (anexo de desconhecido aumenta score de spam E medo de abrir; a capa no link substitui o preview).
- [ ] **Assunto ≤ 60 caracteres**, formulado como pergunta ou frase pessoal com o nome do negócio.
- [ ] **Primeira linha 100% personalizada** (nome + fato real das avaliações) — filtros de spam e humanos reconhecem template genérico.
- [ ] **Remetente = conta Gmail pessoal ativa do usuário** (já tem SPF/DKIM do Google). Nunca sugerir disparo em massa: os envios são 1 a 1, poucos por dia — padrão humano.

## E-mail — Envio

- Modo **rascunho** (padrão): criar via conector do Gmail (`create_draft`) com destinatário, assunto e corpo prontos. Avisar o usuário para revisar antes de enviar.
- Modo **enviar direto**: se o conector não suportar envio, abrir o Gmail web via Claude in Chrome, ou criar o rascunho e avisar.
- Sem e-mail confirmado → pula o e-mail para esse lead (não impede o WhatsApp, se houver número).

## WhatsApp — Mensagem

Mesma verdade do e-mail (elogio real, defeito/oportunidade sem ofensa, link único, zero preço), reescrita curta e conversacional:

- **Abertura**: nome do negócio + elogio específico e verificável (nota/avaliação), em 1 frase — nunca "Olá, tudo bem?" genérico.
- **Corpo (1-2 frases)**:
  - **`tipo: redesign`** — observação leve sobre o site atual como oportunidade (mesmo espírito do parágrafo 2 do e-mail, mas 1 frase só).
  - **`tipo: criacao`** — "vi que vocês ainda não têm site, e imagino que perdem gente que busca no Google" (tom de oportunidade, nunca de crítica).
- **A prova**: "preparei uma [nova versão / um site] pra vocês, já no ar" + o link da página-capa (mesmo link do e-mail).
- **CTA único**: "dá uma olhada e me conta o que achou?" — sem preço, sem pressão, sem múltiplas perguntas.
- **Assinatura leve**: primeiro nome do usuário ao final (não precisa da assinatura completa do e-mail — no WhatsApp o contato já é 1:1 e pessoal).

Exemplo de tom (adaptar aos dados reais, nunca usar literalmente):
> Oi! Vi o [Nome do negócio] no Google, nota [4.8] com [63] avaliações, muito bom! Reparei que [oportunidade/defeito em 1 frase]. Preparei uma [nova versão do site / um site] pra vocês, já no ar: [link]. Dá uma olhada quando puder e me conta o que achou?
> — [Primeiro nome do usuário]

## WhatsApp — Checklist (BLOQUEANTE — rodar antes de abrir a conversa)

- [ ] 3-5 linhas no máximo — sem parágrafos longos.
- [ ] 1 link só (a mesma página-capa do e-mail), sem encurtador.
- [ ] Primeira frase 100% personalizada (nome do negócio + fato real).
- [ ] Zero preço, zero urgência, zero emoji em excesso (no máximo 1, se combinar com o tom).
- [ ] Mensagem diferente da versão de e-mail — mesma verdade, redação própria do canal.

## WhatsApp — Envio (via Claude in Chrome, WhatsApp Web)

**Padrão: deixar a mensagem pronta para o usuário revisar e clicar em enviar — nunca clicar em enviar sozinho, a menos que o usuário peça explicitamente e confirme o envio daquele lote no chat.**

1. Monte o link `https://web.whatsapp.com/send?phone=[whatsapp]&text=[mensagem URL-encoded]` (whatsapp no formato `55DDDNUMERO`, sem `+` nem espaços).
2. Abra o link no Claude in Chrome. Se for a primeira vez na sessão, o WhatsApp Web pode pedir para o usuário escanear o QR code — pause e avise o usuário para escanear com o celular dele; nunca tente contornar esse login.
3. Aguarde a conversa carregar com a mensagem já digitada no campo de texto (não enviada). Confirme visualmente (screenshot ou leitura da página) que o texto está correto e completo no campo.
4. **Pare aí.** Informe ao usuário: "mensagem pronta na conversa do WhatsApp com [Nome] — é só revisar e apertar enviar". Só clique no botão de enviar se o usuário tiver dito explicitamente que quer que você envie (ex.: "pode mandar direto") — nesse caso, confirme o lote antes de começar e ainda assim avise a cada envio.
5. Sem WhatsApp capturado → pula o WhatsApp para esse lead (não impede o e-mail, se houver endereço).

## Página-capa (o que o cliente vê ao clicar)

O link do e-mail leva à página-capa gerada no `/publicar`. Duas versões, conforme o `tipo` do lead:

- **`tipo: redesign`** — `references/capa-proposta-template.html`: nome do cliente no topo, toggle antes/depois lado a lado e a assinatura do usuário.
- **`tipo: criacao`** — `references/capa-lancamento-template.html`: nome do cliente no topo, só a página nova em destaque (sem toggle, já que não há site anterior) e a assinatura do usuário.

Ambas existem para dar credibilidade ao clique — o cliente vê o próprio negócio, não um link estranho. Exigências: servida em `https://`, personalizada com dados reais, sem pedido de dado pessoal nenhum.

## Depois do envio

Registrar no banco/`leads.md`: status `proposta` + `dataProposta` (data do e-mail, se enviado) + `whatsappProposta` (data/hora em que a mensagem de WhatsApp foi deixada pronta ou enviada, se aplicável) — e no dashboard (skill `dashboard-leads`). As respostas por e-mail são verificadas pelo comando `/respostas` (Gmail via conector) — sugira ao usuário agendar a verificação diária. Respostas por WhatsApp o usuário confere direto no celular/WhatsApp Web e informa ao Claude para atualizar o status manualmente. Follow-up pelo `/followup` após 3+ dias úteis sem resposta em NENHUM dos canais (1 único follow-up por lead, mas pode sair nos dois canais: curto, gentil, "conseguiu ver a página?").
