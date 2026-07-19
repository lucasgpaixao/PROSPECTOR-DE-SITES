---
description: Publica as páginas redesenhadas na Hostinger e retorna as URLs públicas
argument-hint: "[nome do cliente ou todos]"
---

Publique páginas na Hostinger seguindo a skill `deploy-hostinger`.

## Passos

1. Leia `prospector-config.json`. Se os dados da Hostinger não estiverem preenchidos, colete-os agora (usuário, domínio, servidor — e oriente o usuário a preencher a senha diretamente no config, nunca no chat) — não prossiga sem eles.
2. Determine o que publicar: `$ARGUMENTS` (um cliente ou "todos"), ou liste as páginas com status `redesenhado` em `leads.md` e pergunte.
3. **Gere a página-capa de cada cliente**: conforme o `tipo` do lead (`leads.md`/dashboard), preencha `references/capa-proposta-template.html` (tipo `redesign`, com toggle antes/depois) ou `references/capa-lancamento-template.html` (tipo `criacao`, sem toggle) — ambas na skill `proposta-email` — com os dados do lead + assinatura do config e salve como `sites/[slug]/proposta.html`. É ela que vai no e-mail de proposta.
4. **Publique seguindo a skill `deploy-hostinger`**, na ordem dela: Método 1 (Gerenciador de Arquivos via navegador, **sempre pedindo confirmação explícita antes de subir cada arquivo** — nunca faça upload silencioso, mesmo já tendo rodado `/publicar` antes) é o padrão, escopado sempre na subpasta exata `public_html/[pastaBase]/[slug]/`, nunca na raiz. Método 2 (FTP) só se o usuário preferir tentar e o diagnóstico da skill não indicar bloqueio de porta de dados — se travar depois do login (`230 User ... logged in`) mas antes da transferência, é bloqueio de rede e não adianta insistir; volte pro Método 1. **Nunca use ferramenta de deploy que publique substituindo o domínio inteiro** (ver seção "PROIBIDO" da skill) — ela apaga os outros clientes já publicados.
5. **Verificação HTTPS (bloqueante)**: abra cada URL com `https://` e confirme que carrega com cadeado válido. Se o HTTPS falhar, siga a seção "HTTPS obrigatório" da skill `deploy-hostinger` (AutoSSL no hPanel) antes de considerar publicado — link `http://` NUNCA vai para cliente.
6. Atualize `leads.md` e o banco do dashboard: status `publicado` + URL pública nova.

## Saída

Liste, por cliente: URL da página nova e URL da capa (`.../proposta.html`), ambas testadas em https. Sugira o próximo passo: `/proposta` para enviar os e-mails.
