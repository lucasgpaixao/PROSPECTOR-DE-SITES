---
name: deploy-hostinger
description: >-
  Publica páginas na hospedagem Hostinger — upload via FTP/hPanel, pastas por
  cliente e verificação de URL. Use quando o usuário disser "publicar", "subir
  site", "deploy", "hostinger" ou rodar publicar/setup do prospector de sites.
---

# Deploy na Hostinger

Publicar em `public_html/[pastaBase]/[slug]/index.html` → `https://[dominio]/[pastaBase]/[slug]/`.

Credenciais em `prospector-config.json` → `"hostinger"`. Senha NUNCA no chat — usuário preenche no arquivo. Ao usar em comandos, leia do arquivo sem exibir em saídas.

Dados no hPanel: **Sites** → **Gerenciar** → **Arquivos** → **Contas FTP** (usuário, host e porta).

## Método 1 — FTP programático (tentar primeiro)

Host FTP comum: `ftp.[dominio]` ou o hostname exibido no hPanel.

```bash
curl -sS --ftp-create-dirs -T index.html \
  "ftp://ftp.DOMINIO/public_html/clientes/SLUG/index.html" \
  --user "USUARIO:SENHA"
```

- Testar também com `servidor` do config se `ftp.[dominio]` falhar
- Porta padrão 21; se o hPanel indicar outra porta, use `--ftp-port`
- `--ftp-create-dirs` cria as pastas automaticamente
- Mascarar senha em logs

## Método 2 — MCP Hostinger (deploy de pasta zipada)

Se o MCP **user-hostinger-hosting** estiver configurado, empacote a pasta do cliente e publique:

```bash
cd prospector-data/sites/SLUG
zip -r ../SLUG_$(date +%Y%m%d_%H%M%S).zip .
```

Chame `hosting_deployStaticWebsite` com `domain` do config e `archivePath` do zip.

> Este método publica o conteúdo do zip na raiz do domínio. Para manter a estrutura `clientes/[slug]/`, prefira FTP (Método 1).

## Método 3 — fallback pelo browser (Cursor)

MCP **cursor-ide-browser**:

1. `browser_navigate` → `https://hpanel.hostinger.com` (hPanel)
2. Se pedir login, peça ao usuário logar (não digite senha sem autorização)
3. **Arquivos** → **Gerenciador de arquivos** → `public_html/[pastaBase]/` → criar pasta `[slug]` → Upload do `index.html`
4. O arquivo está no workspace — indicar caminho na janela de seleção

## Verificação (sempre)

Após upload: `browser_navigate` ou `curl` em `https://[dominio]/[pastaBase]/[slug]/`. Confirmar HTTP 200 e título do cliente. Se 404: checar caminho e permissões (644 arquivos, 755 pastas).

## Organização

- 1 pasta por cliente, slug kebab-case sem acentos
- Nunca sobrescrever pasta de outro cliente
- Teste do setup: `public_html/[pastaBase]/teste/index.html` com "Funcionou!"
