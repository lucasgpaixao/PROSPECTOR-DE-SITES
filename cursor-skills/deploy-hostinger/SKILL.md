---
name: deploy-hostinger
description: Esta skill deve ser usada ao publicar páginas na hospedagem Hostinger — upload via script local automático, FTP ou hPanel, criação de pastas por cliente, verificação da URL pública e HTTPS. Acione quando o usuário disser "publicar", "subir o site", "colocar no ar", "deploy", "hostinger" ou rodar /publicar ou o teste de conexão do /setup.
---

# Deploy na Hostinger

Publicar páginas em `public_html/[pastaBase]/[slug]/` e garantir a URL pública `https://[dominio]/[pastaBase]/[slug]/` funcionando.

## Credenciais

Tudo vem de `prospector-config.json` (bloco `hostinger`): `usuario`, `dominio`, `servidor`, `senha`, `pastaBase` (padrão `clientes`). **A senha vive SÓ nesse arquivo, no computador do usuário — nunca é digitada no chat, nunca é exibida em nenhuma saída, log ou comando mostrado ao usuário.** Se a senha estiver vazia, oriente o usuário: dashboard → aba Configurações → Conexão Hostinger → colar a senha e salvar (ou editar o arquivo na mão). Nunca pelo chat.

## Método 1 — Publicador automático local (RECOMENDADO: instala uma vez, nunca mais clica)

A rede do sandbox do Cursor NÃO alcança FTP nem hPanel — isso vale para todo usuário. A publicação roda na máquina do usuário via um publicador instalado no agendador do Windows: a cada minuto ele verifica a fila e sobe o que houver, escondido, lendo as credenciais do config. O usuário instala UMA vez e o /publicar vira 100% automático.

1. **Garanta os 4 arquivos na pasta de trabalho (`prospector-data/`)** (copie de `references/` desta skill, sobrescrevendo versões antigas): `publicar-agora.ps1`, `publicar-agora.bat`, `publicador-oculto.vbs` e `instalar-publicador.bat`.
2. **Primeira vez**: peça UM duplo clique no `instalar-publicador.bat` (cria a tarefa "ProspectorPublicador" no Windows). Se der erro de permissão: botão direito → Executar como administrador. Isso acontece só uma vez na vida.
3. **Monte a fila**: escreva `fila-publicacao.txt` na raiz da pasta de trabalho (`prospector-data/`), uma linha por arquivo: `caminho/local/arquivo.html|public_html/[pastaBase]/[slug]/index.html`. Inclua página (`index.html`) e capa (`proposta.html`) de cada cliente. Em até 1 minuto o publicador sobe tudo sozinho e renomeia a fila para `fila-publicada-[data].txt` (o log fica em `publicador-log.txt`).
4. **Aguarde ~90s e verifique**: confira se a fila foi renomeada e teste as URLs (verificação abaixo). Sem tarefa instalada, o fallback manual é o duplo clique no `publicar-agora.bat`.

## Método 2 — FTP direto do sandbox (tentar primeiro, silencioso)

Antes de acionar o usuário, tente publicar você mesmo: `curl -sS --connect-timeout 15 -T [arquivo] "ftp://[servidor]/public_html/[pastaBase]/[slug]/index.html" --user "[usuario]:[senha do config]" --ftp-create-dirs` (senha lida do arquivo via script — jamais mostrada). Se funcionar, ótimo: zero ação do usuário. Se a rede do sandbox bloquear (timeout/refused), caia SEM DRAMA para o Método 1 — não insista em tentativas repetidas.

## Método 3 — Browser Cursor (último recurso)

Se os métodos 1 e 2 falharem (ex.: curl.exe ausente no Windows do usuário): hPanel Gerenciador de arquivos via MCP `cursor-ide-browser` — o USUÁRIO faz o login dele (nunca peça a senha no chat), você navega, cria as pastas e faz upload pela interface.

## Verificação (obrigatória, após qualquer método)

1. Abra `https://[dominio]/[pastaBase]/[slug]/` e a capa `.../proposta.html` — confirme que carregam com conteúdo certo.
2. **HTTPS obrigatório**: precisa carregar com cadeado válido. Se der erro de certificado: Hostinger tem SSL grátis — guie: hPanel → **SSL** → ativar para o domínio. Enquanto o HTTPS não valida, a publicação NÃO está concluída — link `http://` NUNCA vai para cliente.
3. Atualize `leads.md` + dashboard com status `publicado` e a URL.

## Teste de conexão do /setup

Publique `teste.html` simples ("Funcionou!") em `public_html/[pastaBase]/teste/index.html` pelo Método 2; se bloqueado, já deixe os scripts do Método 1 copiados na pasta, monte a fila com o teste e peça os 2 cliques — assim o usuário aprende o fluxo logo no setup.


## Método 4 — MCP Hostinger

Se o MCP **user-hostinger-hosting** estiver configurado, use `hosting_deployStaticWebsite` com zip da pasta do cliente (ver skill completa).
