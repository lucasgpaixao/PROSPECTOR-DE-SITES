# Workflow: Publicar

Publique páginas na HostGator seguindo a skill `deploy-hostgator`.

## Passos

1. Leia `prospector-config.json`. Se dados da HostGator incompletos, colete usuário/domínio/servidor e oriente preencher senha no config — não prossiga sem eles.
2. Determine o que publicar: um cliente, "todos", ou liste páginas com status `redesenhado` em `leads.md` e pergunte.
3. Para cada página: envie `sites/[slug]/[slug].html` para `public_html/[pastaBase]/[slug]/index.html` via FTP (skill `deploy-hostgator`). Fallback: browser no cPanel File Manager.
4. Verifique cada URL pública (`https://[dominio]/[pastaBase]/[slug]/`) com `browser_navigate` ou `curl`.
5. Atualize `leads.md`: status `publicado` + URL pública. Regenere `leads.csv` se existir.

## Saída

Liste as URLs públicas. Sugira enviar propostas por e-mail.
