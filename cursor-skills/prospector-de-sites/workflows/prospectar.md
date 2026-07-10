# Workflow: Prospectar

Prospecte leads qualificados seguindo a skill `prospeccao-maps`.

## Preparação

1. Leia `prospector-config.json` na pasta de trabalho. Se não existir, oriente a rodar o setup primeiro.
2. Determine nicho e cidade: use os argumentos do usuário se informados; senão, pergunte qual nicho padrão do config usar (e confirme a cidade). O usuário SEMPRE pode trocar nicho e cidade na hora.
3. Leia `leads.md` (se existir) para excluir profissionais já avaliados.

## Execução

Use o MCP **cursor-ide-browser** para abrir o Google Maps e executar o fluxo da skill `prospeccao-maps`:

1. `browser_navigate` → `https://www.google.com/maps/search/[nicho]+em+[cidade]`
2. `browser_snapshot` para ler resultados; `browser_click` para abrir cada estabelecimento
3. Para cada site, abra em nova aba e avalie qualidade
4. Use `browser_cdp` com `Runtime.evaluate` para extrair e-mails do HTML quando necessário
5. `browser_take_screenshot` para referência visual

Critérios: nota ≥ 4.7, ≥ 40 avaliações, site ativo porém ruim, e-mail público. Meta: leads qualificados do config (padrão 10) ou até 25 avaliados.

## Saída

1. **`leads.md`** (obrigatório): todos os avaliados — qualificados e descartados — ranqueados por potencial. Status inicial: `novo` para qualificados.
2. **`leads.csv`** (obrigatório): mesmas colunas para o usuário importar no Google Sheets se quiser (#, Nome, Nota, Avaliações, E-mail, Telefone, Site atual, Motivo, Situação, Status, URL nova).
3. Em rodadas novas, some os leads novos aos antigos — nunca duplique cliente já avaliado.

Mostre a tabela ao usuário e sugira redesenhar os 5+ melhores leads.
