# Workflow: Setup

Configure o ambiente do Prospector de Sites. Siga esta ordem:

## 1. Pasta de trabalho

Crie ou confirme a pasta `prospector-data/` na raiz do workspace. Se o usuário preferir outro caminho, use `AskQuestion` e salve em `prospector-config.json` → `"pastaTrabalho"`.

## 2. Verificar config existente

Procure `prospector-config.json` na pasta de trabalho (`prospector-data/`). Se existir, mostre um resumo (sem exibir a senha) e pergunte o que o usuário quer atualizar. Se não existir, colete os dados abaixo.

## 3. Dados do usuário (perguntar via AskQuestion / formulário)

Colete:

- **Assinatura da proposta**: nome completo, como quer se apresentar (ex.: "Designer de páginas de alta conversão") e WhatsApp/telefone de contato.
- **Nichos padrão de prospecção**: sugira nutricionistas, psicólogos, advogados e psiquiatras como ponto de partida, mas deixe o usuário editar livremente.
- **Cidade/região padrão**.
- **Leads qualificados por busca**: padrão 10.
- **Modo de envio da proposta**: padrão "criar rascunho no Gmail para revisão" (recomendado). Alternativa: enviar direto.

## 4. Conexão com a Hostinger

Pergunte se o usuário já contratou a hospedagem Hostinger.

- **Se ainda não contratou**: explique brevemente que ele precisa de um plano que aceite múltiplos sites (plano Single ou superior), que ao contratar ganha domínio grátis, e que depois de ativar deve voltar e rodar `setup do prospector` de novo. Salve o config parcial e encerre.
- **Se já contratou**: NÃO colete nenhum dado da Hostinger pelo chat (nem usuário, nem servidor — e JAMAIS a senha). Tudo vai num lugar só, a aba Configurações do dashboard:
  1. Instrua: abra o dashboard (`iniciar-dashboard.bat` na pasta de trabalho (`prospector-data/`)) → aba **Configurações** → seção **Conexão Hostinger**.
  2. Lá ele preenche os 4 campos + senha: usuário FTP, domínio, servidor (hostname do hPanel → **Contas FTP**) e senha. Clica em "Salvar conexão" → tudo vai do navegador direto pro `prospector-config.json` no computador dele, sem passar pelo chat.
  3. Peça para ele avisar quando salvar ("salvei") — aí você LÊ o config (verificando que os campos estão preenchidos, sem nunca exibir a senha) e roda o teste de conexão.

  Nunca exiba, imprima ou registre a senha em nenhuma saída. Se ele preferir, editar o `prospector-config.json` na mão também vale.

## 5. Salvar e testar

Salve tudo em `prospector-config.json` na pasta de trabalho (`prospector-data/`), neste formato:

```json
{
  "assinatura": { "nome": "", "apresentacao": "", "whatsapp": "" },
  "prospeccao": { "nichos": ["nutricionistas", "psicologos", "advogados", "psiquiatras"], "cidade": "", "leadsPorBusca": 10 },
  "envio": { "modo": "rascunho" },
  "hostinger": { "usuario": "", "dominio": "", "servidor": "", "senha": "", "pastaBase": "clientes" }
}
```

Se os dados da Hostinger foram informados, teste a conexão seguindo a skill `deploy-hostinger`: publique uma página `teste.html` simples e informe a URL pública ao usuário. Se o teste falhar, diagnostique (credenciais, servidor, método de upload) antes de concluir.

## 6. Dashboard inicial

Siga a seção "Setup" da skill `dashboard-leads`: copie `dashboard-server.py` e `iniciar-dashboard.bat` para a raiz da pasta de trabalho (`prospector-data/`), crie o banco `prospector.db` (schema da skill) e gere o `dashboard.html` do template. Explique ao usuário: duplo clique em `iniciar-dashboard.bat` abre o painel completo em http://localhost:8765 com edição/exclusão salvando no banco (requer Python no Windows; sem ele, o dashboard.html abre no modo leitura).

## 7B. Entregar o manual e os scripts

Copie da pasta do plugin para a pasta de trabalho (`prospector-data/`) (sobrescrevendo versões antigas): `manual.html` (manual do usuário) e os 4 arquivos do publicador (skill `deploy-hostinger`, pasta references): `publicar-agora.ps1`, `publicar-agora.bat`, `publicador-oculto.vbs`, `instalar-publicador.bat`. Peça UM duplo clique no `instalar-publicador.bat` (registra o publicador automático no Windows — única vez na vida; o teste de conexão do item 5 pode usar esse fluxo). Apresente o `manual.html` ao usuário com a frase: "Esse é o seu manual — guarda ele que responde 90% das dúvidas."

## 7. Encerrar

Confirme o que foi salvo e explique o ciclo (guiando SEMPRE o próximo passo ao fim de cada comando): `prospectar` → `redesenhar` → `publicar` → `proposta`, com `editor` opcional para ajustes manuais e o `dashboard.html` como painel de controle de tudo.
