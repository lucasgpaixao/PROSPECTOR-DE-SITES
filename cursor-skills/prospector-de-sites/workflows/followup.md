# Workflow: Followup

Gere follow-ups educados para propostas paradas, seguindo a skill `proposta-email`. Mesma lógica de canal duplo do `proposta`: e-mail pra quem tem e-mail, WhatsApp pra quem tem WhatsApp.

## Passos

1. **Verifique respostas ANTES**: rode a lógica do `respostas` (busca no Gmail via conector) para não fazer follow-up de quem já respondeu por e-mail — quem respondeu vira status `respondeu` e sai da lista. Para WhatsApp, pergunte ao usuário se algum lead já respondeu por lá (ele não é verificado automaticamente).
2. Selecione os elegíveis: leads com status `proposta`, proposta enviada (e-mail e/ou WhatsApp) há **3+ dias**, e SEM follow-up registrado (procure "Follow-up" no campo `obs` do banco/`leads.md`). Se `argumentos do usuário` indicar um cliente, restrinja a ele (mas respeite a regra de nunca repetir follow-up).
3. Para cada elegível, escreva o follow-up nos canais que ele recebeu a proposta original:
   - **E-mail**: máximo 4 linhas, tom de quem lembra com gentileza, nunca cobra. Referência leve ao primeiro e-mail ("te escrevi semana passada sobre o site") + pergunta única "conseguiu ver a página que preparei?" + o mesmo link da capa (único link). Sem preço, sem urgência. Passar pela "E-mail — Checklist anti-spam" da skill.
   - **WhatsApp**: 2-3 linhas só, ainda mais direto que o e-mail — "Oi! Só passando pra saber se você chegou a ver o [site/nova versão] que preparei: [link]" + nada mais. Passar pelo "WhatsApp — Checklist" da skill.
4. Envio: e-mail vira rascunho no Gmail (mesmo modo do config). WhatsApp segue "WhatsApp — Envio" da skill — mensagem pronta na conversa, usuário clica em enviar (nunca enviar sozinho sem pedido explícito). **1 follow-up por lead, para sempre** (nos canais que ele usar) — se não responder ao follow-up, o lead é marcado como frio manualmente pelo usuário no dashboard.
5. Registre em cada lead: `obs` += "Follow-up enviado em [data]" (indicando o(s) canal(is)) no banco via API do dashboard se estiver rodando, senão direto no SQLite/`leads.md`.

## Saída

Liste: follow-ups criados por canal, leads que responderam nesse meio-tempo (celebre!), e leads sem resposta que já receberam follow-up nos dois canais (sugerir marcar como frio). Ofereça agendar `respostas` + `followup` como verificação diária automática.
