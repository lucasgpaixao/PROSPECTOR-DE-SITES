---
description: Escreve e envia a proposta por e-mail (Gmail) e WhatsApp (WhatsApp Web)
argument-hint: "[nome do cliente ou todos]"
---

Envie propostas para os leads com página publicada, seguindo a skill `proposta-email`. Os dois canais são independentes: um lead pode receber só e-mail, só WhatsApp, ou os dois — conforme os dados que a prospecção capturou dele.

## Passos

1. Leia `prospector-config.json` (assinatura e modo de envio) e `leads.md`.
2. Determine os destinatários: `$ARGUMENTS`, ou todos os leads com status `publicado` que ainda não receberam proposta em NENHUM canal. Para cada um, verifique o que ele tem: e-mail confirmado → entra no lote de e-mail; WhatsApp capturado na prospecção → entra no lote de WhatsApp (a maioria entra nos dois lotes).
3. Se a página-capa ainda não foi publicada para algum cliente, gere e publique-a agora (template certo conforme o `tipo` do lead, na skill `proposta-email`; upload pela skill `deploy-hostinger`) antes de prosseguir — ela é o único link usado nos dois canais.
4. **E-mail** (para quem tem e-mail confirmado): escreva seguindo "E-mail — Estrutura" da skill `proposta-email`, usando os dados reais do lead (elogio das avaliações, defeito/oportunidade específico, link único da capa). NUNCA mencione preço. Rode a "E-mail — Checklist anti-spam" (bloqueante) antes de criar o rascunho. Envio conforme o modo do config: **rascunho** (padrão, via conector do Gmail) ou **enviar direto** (Claude in Chrome no Gmail web, se o conector não suportar).
5. **WhatsApp** (para quem tem WhatsApp capturado): escreva seguindo "WhatsApp — Mensagem" da skill `proposta-email` — versão curta e conversacional, NUNCA a mesma redação do e-mail colada. Rode o "WhatsApp — Checklist" (bloqueante). Envio seguindo "WhatsApp — Envio": abra `web.whatsapp.com/send?phone=...&text=...` via Claude in Chrome, confirme que a mensagem carregou no campo de texto e PARE — deixe pronta para o usuário revisar e clicar em enviar. Só clique em enviar você mesmo se o usuário pedir explicitamente e confirmar o lote antes.
6. Atualize `leads.md` e o banco do dashboard: status `proposta`, `dataProposta` (se e-mail enviado) e `whatsappProposta` (se mensagem de WhatsApp deixada pronta/enviada).

## Saída

Resuma por cliente: quais canais receberam proposta (e-mail criado/enviado, WhatsApp pronto para envio ou enviado) e o link da capa usado. Lembre o usuário: `/respostas` verifica quem respondeu por e-mail (dá pra agendar diário); respostas por WhatsApp ele confere direto e avisa você para atualizar o status. `/followup` cuida de quem está 3+ dias sem responder em nenhum canal.
