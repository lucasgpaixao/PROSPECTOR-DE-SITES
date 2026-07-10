---
name: deploy-hostgator
description: >-
  Publica páginas na hospedagem HostGator — upload via FTP/cPanel, pastas por
  cliente e verificação de URL. Use quando o usuário disser "publicar", "subir
  site", "deploy", "hostgator" ou rodar publicar/setup do prospector de sites.
---

# Deploy na HostGator

Publicar em `public_html/[pastaBase]/[slug]/index.html` → `https://[dominio]/[pastaBase]/[slug]/`.

Credenciais em `prospector-config.json`. Senha NUNCA no chat — usuário preenche no arquivo. Ao usar em comandos, leia do arquivo sem exibir em saídas.

## Método 1 — FTP programático (tentar primeiro)

```bash
curl -sS --ftp-create-dirs -T index.html \
  "ftp://ftp.DOMINIO/public_html/clientes/SLUG/index.html" \
  --user "USUARIO:SENHA"
```

- Testar também com `servidor` do config se `ftp.[dominio]` falhar
- `--ftp-create-dirs` cria pastas automaticamente
- Mascarar senha em logs

## Método 2 — cPanel UAPI via HTTPS

```bash
curl -sS -u "USUARIO:SENHA" \
  "https://SERVIDOR:2083/execute/Fileman/upload_files" \
  -F "dir=/public_html/clientes/SLUG" -F "file-1=@index.html"
```

Criar pasta: `https://SERVIDOR:2083/execute/Fileman/mkdir?path=public_html/clientes&name=SLUG`

## Método 3 — fallback pelo browser (Cursor)

MCP **cursor-ide-browser**:

1. `browser_navigate` → `https://SERVIDOR:2083` (cPanel)
2. Se pedir login, peça ao usuário logar (não digite senha sem autorização)
3. Abrir **Gerenciador de Arquivos** → `public_html/[pastaBase]/` → criar pasta `[slug]` → Upload do `index.html`
4. O arquivo está no workspace — indicar caminho na janela de seleção

## Verificação (sempre)

Após upload: `browser_navigate` ou `curl` em `https://[dominio]/[pastaBase]/[slug]/`. Confirmar HTTP 200 e título do cliente. Se 404: checar caminho e permissões (644 arquivos, 755 pastas).

## Organização

- 1 pasta por cliente, slug kebab-case sem acentos
- Nunca sobrescrever pasta de outro cliente
- Teste do setup: `public_html/[pastaBase]/teste/index.html` com "Funcionou!"
