# Prospector de Sites

Prospecção semi-automática de clientes com sites ruins (ou sem site): acha, redesenha ou cria do zero, publica e oferta.

## O ciclo

1. `/setup` — roda uma vez: assinatura, nichos padrão, dados do hPanel da Hostinger (com teste de publicação).
2. `/prospectar [nicho] [cidade]` — busca no Google Maps negócios nota ≥ 4.7 com site fraco OU sem site e gera `leads.md` com e-mail, tipo (redesign/criação), motivo e ranking (padrão: 10 leads).
3. `/redesenhar` — recria as páginas dos 5+ melhores leads (que já têm site) com estética premium, mantendo o conteúdo, logo e paleta reais do cliente.
3b. `/criar-site` — gera do zero as páginas dos leads sem site próprio, usando fotos e avaliações reais do perfil do Google Maps (mesma qualidade e mesma entrega do `/redesenhar`).
4. `/editor [cliente]` — gera versão editável no navegador (textos e imagens) com exportação da página final.
5. `/publicar [cliente|todos]` — sobe na Hostinger em `dominio.com/clientes/[slug]/`, gera a página-capa de apresentação (antes/depois para redesign, ou lançamento para site novo — `proposta.html`) e só conclui com HTTPS validado.
6. `/proposta [cliente|todos]` — escreve a proposta (rapport, sem preço) e envia nos dois canais disponíveis: e-mail (rascunho no Gmail, passa pela checklist anti-spam) e WhatsApp (mensagem pronta no WhatsApp Web para você revisar e clicar em enviar) — mesma página-capa como único link nos dois.
7. `/respostas` — verifica no Gmail quem respondeu e atualiza o dashboard sozinho (dica: agende a verificação diária). Respostas por WhatsApp você confere direto e informa ao Claude.
8. `/followup [cliente]` — 3+ dias sem resposta em nenhum canal? Gera o follow-up gentil por e-mail e/ou WhatsApp (1 por lead, nunca repete) já checando quem respondeu antes.
9. `/contrato [cliente]` — cliente fechou? Gera a minuta do contrato (pronta pra PDF) com os dados do negócio e deixa o rascunho no Gmail.

## Manual e publicação automática

O pacote inclui `manual.html` — o manual completo do usuário, copiado pra pasta no `/setup` e **atualizado a cada versão do plugin**. A publicação na Hostinger é automática: senha preenchida uma vez no `prospector-config.json` + `publicar-agora.bat` (2 cliques) quando a rede do sandbox não alcança o FTP — sem login no hPanel.

## Dashboard local

O plugin mantém um painel de controle na sua pasta: `prospector.db` (banco SQLite) + `dashboard.html`. Duplo clique em `iniciar-dashboard.bat` (requer Python) abre o painel completo em http://localhost:8765 — kanban com drag & drop, edição, exclusão, funil, comparador antes/depois integrado, follow-ups, controle de contratos (pendente/enviado/assinado) e painel financeiro (recebido, a receber e MRR das manutenções), tudo salvo no banco.

## Requisitos

- Extensão Claude in Chrome conectada (prospecção no Maps, fallback de deploy e envio pelo WhatsApp Web — a primeira mensagem pede para você escanear o QR code)
- Conector do Gmail (rascunhos de proposta)
- Pasta conectada no Cowork (armazena config, leads e sites)
- Hospedagem Hostinger com acesso ao hPanel

## Onde ficam os dados

Tudo na pasta conectada: `prospector-config.json` (preferências e credenciais — a senha do hPanel fica em texto no seu computador), `leads.md` (pipeline) e `sites/[slug]/` (páginas criadas).
