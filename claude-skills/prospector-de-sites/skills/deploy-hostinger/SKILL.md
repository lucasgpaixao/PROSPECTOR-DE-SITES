---
name: deploy-hostinger
description: Esta skill deve ser usada ao publicar páginas na hospedagem Hostinger — upload via FTP/hPanel, criação de pastas por cliente, verificação da URL pública e fallback pelo navegador. Acione quando o usuário disser "publicar", "subir o site", "colocar no ar", "deploy", "hostinger" ou rodar /publicar ou o teste de conexão do /setup.
---

# Deploy na Hostinger

Publicar cada página do cliente em `public_html/[pastaBase]/[slug]/index.html`, acessível em `https://[dominio]/[pastaBase]/[slug]/`.

Credenciais: ler de `prospector-config.json` → `"hostinger"` (usuário, domínio, servidor, senha FTP/hPanel). Dados no hPanel: **Sites** → **Gerenciar** → **Arquivos** → **Contas FTP**. Se faltarem usuário/domínio/servidor, pedir ao usuário. Se faltar a senha, NUNCA pedir no chat: instruir o usuário a preenchê-la diretamente no campo `"senha"` do `prospector-config.json`. Ao usar a senha em comandos, leia-a do arquivo dentro do próprio comando — nunca exibi-la em saídas ou logs.

## Método 1 — FTP programático (tentar primeiro)

O host FTP normalmente é `ftp.[dominio]` ou o hostname do hPanel. Via bash:

```bash
curl -sS --ftp-create-dirs -T index.html \
  "ftp://ftp.DOMINIO/public_html/clientes/SLUG/index.html" \
  --user "USUARIO:SENHA"
```

- Testar também com o valor de `servidor` do config como host se `ftp.[dominio]` falhar.
- `--ftp-create-dirs` cria as pastas automaticamente.
- Se houver imagens locais ou preview, enviar da mesma forma.
- IMPORTANTE: não expor a senha em mensagens ao usuário; nos logs, mascarar.

## Método 2 — fallback pelo navegador (se o FTP falhar)

Usar o Claude in Chrome:

1. Navegar para `https://hpanel.hostinger.com` — se pedir login, pedir para o usuário logar (não digitar a senha dele no navegador sem autorização explícita).
2. Abrir **Gerenciador de arquivos** → `public_html/[pastaBase]/` → criar pasta `[slug]` → Upload do `index.html`.
3. Como o arquivo está na pasta conectada do usuário, o upload via navegador usa o arquivo real do computador dele — indicar o caminho na janela de seleção.

## Verificação (sempre)

Após o upload, buscar `https://[dominio]/[pastaBase]/[slug]/` e confirmar HTTP 200 + conteúdo correto (título do cliente presente). Se 404, checar: propagação, caminho da pasta, permissões (644 para arquivos, 755 para pastas).

## Organização

- 1 pasta por cliente, slug em kebab-case sem acentos (ex.: `jessica-nutri`).
- Nunca sobrescrever a pasta de outro cliente.
- Página de teste do setup: `public_html/[pastaBase]/teste/index.html` com um "Funcionou!" simples.
