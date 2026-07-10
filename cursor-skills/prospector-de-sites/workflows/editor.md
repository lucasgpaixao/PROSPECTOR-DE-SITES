# Workflow: Editor

Gere a versão editável de uma página redesenhada.

## Passos

1. Identifique o cliente pelo argumento do usuário ou liste as pastas em `sites/` e pergunte qual editar.
2. Leia `sites/[slug]/[slug].html`.
3. Crie (ou regenere) `sites/[slug]/[slug]-editor.html`: cópia da página com a camada de edição injetada antes de `</body>`. Script completo em `redesign-premium/references/editor-visual.md` — use exatamente como está.
4. Use `open_resource` (MCP cursor-app-control) ou informe o caminho absoluto para o usuário abrir no navegador. Explique em 3 linhas:
   - Clique em qualquer texto para editar direto na página.
   - Clique em qualquer imagem para trocá-la por arquivo do computador (embutida em base64).
   - Botão "Exportar página" baixa o HTML final limpo — substitua a página original por ele.
5. Se o usuário enviar o arquivo exportado, substitua `sites/[slug]/[slug].html` antes de publicar.
