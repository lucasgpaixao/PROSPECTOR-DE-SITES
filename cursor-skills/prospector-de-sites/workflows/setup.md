# Workflow: Setup

Configure o ambiente do Prospector de Sites. Siga esta ordem:

## 1. Pasta de trabalho

Crie ou confirme a pasta `prospector-data/` na raiz do workspace. Se o usuário preferir outro caminho, use `AskQuestion` e salve em `prospector-config.json` → `"pastaTrabalho"`.

## 2. Verificar config existente

Procure `prospector-config.json` na pasta de trabalho. Se existir, mostre um resumo (sem exibir a senha) e pergunte o que atualizar. Se não existir, colete os dados abaixo.

## 3. Dados do usuário

Use `AskQuestion` ou perguntas no chat para coletar:

- **Assinatura da proposta**: nome completo, como quer se apresentar (ex.: "Designer de páginas de alta conversão") e WhatsApp/telefone de contato.
- **Nichos padrão de prospecção**: sugira nutricionistas, psicólogos, advogados e psiquiatras como ponto de partida, mas deixe o usuário editar livremente.
- **Cidade/região padrão**.
- **Leads qualificados por busca**: padrão 10.
- **Modo de envio da proposta**: padrão "criar rascunho no Gmail para revisão" (recomendado). Alternativa: enviar direto.

## 4. Conexão com a Hostinger

Pergunte se o usuário já contratou a hospedagem Hostinger.

- **Se ainda não contratou**: explique brevemente que ele precisa de um plano de hospedagem web (Single ou superior), que ao contratar pode vincular um domínio, e que depois de ativar deve voltar e rodar o setup de novo. Salve o config parcial e encerre.
- **Se já contratou**: peça 3 informações do hPanel (**Sites** → **Gerenciar** → **Arquivos** → **Contas FTP**):
  1. **Usuário** FTP
  2. **Domínio principal**
  3. **Servidor FTP** (hostname exibido no hPanel, ex.: `ftp.seudominio.com.br`)

  **A senha NUNCA deve ser digitada no chat.** Salve o config com `"senha": ""` e instrua o usuário a abrir `prospector-config.json` e preencher a senha ele mesmo. Só depois disso rode o teste de conexão.

## 5. Salvar e testar

Salve em `prospector-config.json`:

```json
{
  "pastaTrabalho": "prospector-data",
  "assinatura": { "nome": "", "apresentacao": "", "whatsapp": "" },
  "prospeccao": { "nichos": ["nutricionistas", "psicologos", "advogados", "psiquiatras"], "cidade": "", "leadsPorBusca": 10 },
  "envio": { "modo": "rascunho" },
  "hostinger": { "usuario": "", "dominio": "", "servidor": "", "senha": "", "pastaBase": "clientes" }
}
```

Se os dados da Hostinger foram informados, teste a conexão seguindo a skill `deploy-hostinger`: publique uma página `teste.html` simples e informe a URL pública. Se falhar, diagnostique antes de concluir.

## 6. Encerrar

Confirme o que foi salvo e explique o ciclo: prospectar → redesenhar → publicar → proposta, com editor opcional para ajustes manuais.
