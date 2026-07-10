# Workflow: Respostas

Verifique respostas às propostas enviadas e atualize o pipeline.

## Passos

1. Leia o banco `prospector.db` (ou `leads.md` como fallback): selecione os leads com status `proposta` (ou o cliente de `argumentos do usuário`).
2. Para cada lead, busque no Gmail via conector (`search_threads`) por conversas com o e-mail do lead a partir da `dataProposta` — query típica: `from:[email do lead] after:[dataProposta]` e também a thread da proposta original (`to:[email] [primeiras palavras do assunto]`).
3. Classifique:
   - **Respondeu**: existe mensagem DO lead na thread → atualize o banco (`status='respondeu'`, resumo curto da resposta em `obs`, ex.: "Respondeu 09/07: gostou, pediu valores").
   - **Sem resposta**: mantenha `proposta` (o dashboard cuida do alerta de follow-up).
4. Atualize conforme a skill `dashboard-leads` (upsert no banco + regenerar o snapshot do `dashboard.html`) e regenere a planilha do Google se houver mudanças.
5. Resuma para o usuário: quem respondeu (com a essência de cada resposta), quem segue sem resposta e há quantos dias, e sugira as ações (responder o cliente, follow-up dos parados).

## Automação (sugerir na primeira execução)

Ofereça deixar isso automático com uma tarefa agendada do Cursor: "quer que eu verifique as respostas todo dia de manhã e deixe o dashboard atualizado?" — se aceitar, crie a tarefa agendada diária que executa este comando.

## Regras

- NUNCA marque `fechado` sozinho — fechamento envolve preço/acordo; apenas o usuário confirma (aí registre `valor`).
- Não responda e-mails automaticamente: leitura e classificação apenas. Se o usuário quiser, ofereça rascunho de resposta.
