# Workflow: Prospectar

Prospecte leads qualificados seguindo a skill `prospeccao-maps`.

## Preparação

1. Leia `prospector-config.json` na pasta de trabalho (`prospector-data/`). Se não existir, oriente a rodar `setup` primeiro.
2. Determine nicho e cidade: use os argumentos `argumentos do usuário` se informados; senão, pergunte ao usuário qual dos nichos padrão do config usar (e confirme a cidade). O usuário SEMPRE pode trocar nicho e cidade na hora — nunca trave nos padrões.
3. Leia `leads.md` na pasta de trabalho (`prospector-data/`) (se existir) para saber quais profissionais já foram avaliados — estes devem ser EXCLUÍDOS da nova busca.

## Execução

Use as ferramentas do MCP `cursor-ide-browser` (carregue via ToolSearch se necessário) para abrir o Google Maps e executar o fluxo completo descrito na skill `prospeccao-maps`:

- Buscar "[nicho] em [cidade]"
- Avaliar até 25 estabelecimentos ou até atingir o número de leads qualificados do config (padrão 10), o que vier primeiro
- Critério ouro: nota alta (≥ 4.7) + muitas avaliações (≥ 40) + e-mail público. A partir daí o lead se divide em dois tipos, nenhum é descarte:
  - **`tipo: redesign`** — site próprio ATIVO porém ruim (segue os critérios de "site ruim" da skill).
  - **`tipo: criacao`** — sem site, site fora do ar ou só diretório de terceiros/rede social. Não descartar — é candidato a `criar-site`.
  - Único eliminatório de verdade: nota/avaliações abaixo do critério, ou site próprio já bom. Sem e-mail → pula (registrar descartado com o motivo) e seguir buscando até bater a meta
- Para cada candidato `tipo: redesign`, abrir o site em nova aba e avaliar a qualidade seguindo os critérios da skill. Para `tipo: criacao`, coletar do perfil do Maps: categoria, endereço, horários, fotos (aba "Fotos", rolar até o fim) e avaliações em destaque — ver skill.
- Coletar: nome, nota, nº de avaliações, telefone, **WhatsApp em formato 55DDDnúmero** (link wa.me no site ou celular do perfil do Maps — ver skill), e-mail, `tipo`, URL do site (se houver) e o motivo objetivo (site ruim, ou "sem site próprio")

## Saída — Google Sheets + dashboard + cópia local

1. **Google Sheets**: salve os leads numa PLANILHA DO GOOGLE via `leads.csv` local (importar no Sheets manualmente) — `create_file` com `contentMimeType: text/csv` e o CSV como `textContent` (a conversão automática cria uma planilha nativa do Sheets). Título: `Leads Prospector — [nicho] [cidade]`. Colunas: #, Nome, Nota, Avaliações, E-mail, Telefone, Tipo (redesign/criacao), Site atual, Motivo, Situação (Qualificado/Descartado + motivo), Status, URL nova. Inclua TODOS os avaliados (qualificados E descartados), ranqueados por potencial (melhor nota + pior site, ou sem site, primeiro). Retorne o link da planilha ao usuário.
2. **Cópia local**: mantenha `leads.md` na pasta de trabalho (`prospector-data/`) como cópia de trabalho (o conector do Drive não edita células — os status `novo → redesenhado → publicado → proposta enviada` são atualizados no leads.md local, e a planilha do Google é regenerada com os dados acumulados ao fim de cada comando que muda status). Em rodadas novas, some os leads novos aos antigos numa planilha só, nunca duplique cliente já avaliado.
3. **Dashboard**: crie/atualize `dashboard.html` na raiz da pasta de trabalho (`prospector-data/`) seguindo a skill `dashboard-leads` (template + merge do JSON embutido) — leads novos entram com `status: novo` e o `tipo` coletado (`redesign` ou `criacao`), descartados com `status: descartado`.

A entrega final DEVE incluir a confirmação explícita "Dashboard atualizado: [N] leads" (criando o dashboard pela skill `dashboard-leads` se a pasta não tiver um — obrigatório, nunca pule). Mostre a tabela ao usuário com o link da planilha e do `dashboard.html`, separando os dois grupos, e sugira o próximo passo: `redesenhar` para os 5+ melhores leads com site, `criar-site` para os leads sem site.
