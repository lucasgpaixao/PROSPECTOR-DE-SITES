---
name: deploy-hostinger
description: Esta skill deve ser usada ao publicar páginas na hospedagem Hostinger — upload via script local automático, FTP ou hPanel, criação de pastas por cliente, verificação da URL pública e HTTPS. Acione quando o usuário disser "publicar", "subir o site", "colocar no ar", "deploy", "hostinger" ou rodar /publicar ou o teste de conexão do /setup.
---

# Deploy na Hostinger

Publicar páginas em `public_html/[pastaBase]/[slug]/` e garantir a URL pública `https://[dominio]/[pastaBase]/[slug]/` funcionando.

## Credenciais

Tudo vem de `prospector-config.json` (bloco `hostinger`): `usuario`, `dominio`, `servidor`, `senha`, `pastaBase` (padrão `clientes`). **A senha vive SÓ nesse arquivo, no computador do usuário — nunca é digitada no chat, nunca é exibida em nenhuma saída, log ou comando mostrado ao usuário.** Se a senha estiver vazia, oriente o usuário: dashboard → aba Configurações → Conexão Hostinger → colar a senha e salvar (ou editar o arquivo na mão). Nunca pelo chat.

## Método 1 — Navegador / hPanel Gerenciador de Arquivos (PADRÃO — sempre pedir confirmação antes de subir)

Este é o método confiável na maioria das redes: roda inteiramente por HTTPS (porta 443), que praticamente nunca é bloqueada — diferente do FTP (ver Método 2). Via MCP `cursor-ide-browser`, com o usuário já logado no hPanel (nunca peça a senha do hPanel no chat):

1. Navegue até `hpanel.hostinger.com` → Sites → `[dominio]` → Painel de controle → **Arquivos → Gerenciador de arquivos** → "Acessar arquivos de [dominio]" → `public_html/[pastaBase]/`.
2. Crie a pasta do cliente se não existir (`New folder` → `[slug]`) e entre nela — **nunca opere na raiz de `public_html`, sempre dentro da subpasta exata do cliente**.
3. **BLOQUEANTE — pergunte explicitamente ao usuário antes de subir qualquer arquivo**, mesmo que ele já tenha pedido `publicar` antes: confirme o(s) nome(s) do(s) arquivo(s) e o destino exato (ex.: "posso subir `[slug].html` como `index.html` e `proposta.html` em `public_html/[pastaBase]/[slug]/`?"). Nunca faça upload silencioso — o usuário decide o momento de cada envio.
4. Depois de confirmado: use a ferramenta de upload de arquivo do MCP `cursor-ide-browser` se os arquivos estiverem numa pasta compartilhada com a sessão; se a ferramenta rejeitar o caminho, ofereça duas saídas ao usuário — (a) ele mesmo arrasta os arquivos pra pasta aberta no Gerenciador, ou (b) você usa o editor de texto embutido do Gerenciador (`New file` + colar o conteúdo) para arquivos HTML — este último só funciona para texto, não para imagens.
5. Renomeie a página principal do cliente para `index.html` dentro da subpasta (o Gerenciador não aceita a URL sem arquivo-índice).

## Método 2 — FTP (só se o Método 1 não for viável; alta chance de falhar em modo passivo)

FTP tem uma pegadinha: a conexão de controle (porta 21) costuma abrir mesmo quando o **canal de dados** (modo passivo, porta alta aleatória que o servidor abre pra transferir o arquivo) está bloqueado pelo roteador/rede do usuário (roteadores sem "FTP ALG" fazem exatamente isso — autentica, mas trava ao transferir). Isso NÃO é específico do sandbox: já foi confirmado que acontece até rodando localmente fora do sandbox.

1. Confirme o host de FTP correto no hPanel → Arquivos → **Contas FTP** (o campo "IP do FTP (host)") — em contas compartilhadas o host de FTP costuma ser um IP dedicado, DIFERENTE do domínio configurado em `hostinger.servidor`. Se forem diferentes, atualize `prospector-config.json` com o IP correto antes de tentar.
2. Teste rápido e silencioso: `curl -sS --connect-timeout 15 -T [arquivo] "ftp://[servidor]/public_html/[pastaBase]/[slug]/index.html" --user "[usuario]:[senha do config]" --ftp-create-dirs` (senha lida do arquivo via script — jamais mostrada).
3. **Diagnóstico de falha — não insista em retentativas cegas.** Se o teste travar/der timeout, verifique ANTES de desistir do FTP: `curl -v` até a porta de controle isolada — se a autenticação ("230 User ... logged in") funciona mas trava depois do `EPSV`/`PASV`, é bloqueio de porta de dados (roteador/rede), não vai se resolver tentando de novo. Volte pro Método 1 imediatamente.
4. **Publicador automático local** (só vale a pena se o teste acima realmente funcionar ponta a ponta): copie de `references/` desta skill `publicar-agora.ps1`, `publicar-agora.bat`, `publicador-oculto.vbs` e `instalar-publicador.bat` pra pasta de trabalho (`prospector-data/`), peça UM duplo clique no `instalar-publicador.bat` (cria a tarefa "ProspectorPublicador" no Windows — se der erro de permissão, botão direito → Executar como administrador), depois escreva `fila-publicacao.txt` na raiz (`caminho/local/arquivo.html|public_html/[pastaBase]/[slug]/index.html`, uma linha por arquivo) e aguarde ~90s (a fila renomeia sozinha para `fila-publicada-[data].txt`, log em `publicador-log.txt`).

## PROIBIDO — ferramentas de "deploy" que substituem o site inteiro

Nunca use uma ferramenta de deploy de hospedagem (MCP da Hostinger — incluindo `hosting_deployStaticWebsite` ou qualquer API equivalente que receba um `.zip`/arquivo e publique num domínio) para subir a página de UM cliente. Essas ferramentas publicam substituindo TODO o conteúdo de `public_html` pelo pacote enviado — mesmo que o zip só contenha a subpasta do cliente novo, ela pode inclusive achatar (remover) o nível "clientes/" se for a única pasta no topo do zip, jogando os arquivos direto na raiz. Isso já apagou os outros clientes publicados numa sessão real. Só o Método 1 (Gerenciador de Arquivos, escopado na subpasta exata) ou o Método 2 (FTP, que naturalmente só escreve o arquivo indicado) tocam no site do cliente sem risco pros demais.

## Verificação (obrigatória, após qualquer método)

1. Abra `https://[dominio]/[pastaBase]/[slug]/` e a capa `.../proposta.html` — confirme que carregam com conteúdo certo.
2. **HTTPS obrigatório**: precisa carregar com cadeado válido. Se der erro de certificado: Hostinger tem SSL grátis — guie: hPanel → **SSL** → ativar para o domínio. Enquanto o HTTPS não valida, a publicação NÃO está concluída — link `http://` NUNCA vai para cliente.
3. Atualize `leads.md` + dashboard com status `publicado` e a URL.

## Teste de conexão do /setup

Tente publicar `teste.html` simples ("Funcionou!") em `public_html/[pastaBase]/teste/index.html` pelo Método 2 (FTP) — é um arquivo neutro, sem risco pra clientes, então esse teste único pode ser silencioso. Se travar no canal de dados (ver diagnóstico do Método 2), explique ao usuário que o FTP não é confiável nessa rede e que o comando `publicar` vai usar o Gerenciador de Arquivos (Método 1, sempre com confirmação) daqui pra frente.
