# Workflow: Proposta

Envie propostas para leads com página publicada, seguindo a skill `proposta-email`.

## Passos

1. Leia `prospector-config.json` (assinatura e modo de envio) e `leads.md`.
2. Destinatários: argumento do usuário, ou todos com status `publicado` sem proposta. Somente leads com e-mail confirmado — demais: ofereça texto adaptado para WhatsApp.
3. Para cada cliente, escreva o e-mail seguindo a skill `proposta-email` com dados reais do lead. NUNCA mencione preço.
4. `browser_take_screenshot` da nova página (dobra inicial) → salve em `sites/[slug]/preview.png`. Oriente anexar ao e-mail.
5. Envio conforme modo do config:
   - **rascunho** (padrão): abra Gmail via `cursor-ide-browser`, crie rascunho com destinatário, assunto e corpo. Informe que está pronto para revisão.
   - **enviar direto**: Gmail web via browser, ou MCP Resend se o usuário tiver configurado.
6. Atualize `leads.md`: status `proposta enviada` + data. Regenere `leads.csv`.

## Saída

Resuma quantas propostas criadas/enviadas. Lembre follow-up educado após 3-4 dias úteis sem resposta.
