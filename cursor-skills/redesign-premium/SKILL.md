---
name: redesign-premium
description: >-
  Redesenha o site de um cliente prospectado — versão premium e de alta conversão
  mantendo conteúdo, logo e paleta reais. Use quando o usuário disser "redesenhar
  site", "melhorar página", "refazer o site do cliente" ou rodar redesenhar/editor
  do prospector de sites.
---

# Redesign premium de páginas

Criar uma NOVA VERSÃO da página do cliente — não uma página nova. O cliente precisa reconhecer o próprio negócio.

## Extração de conteúdo (Cursor)

Abra o site original via MCP **cursor-ide-browser** (fetch direto costuma falhar). Use `browser_cdp` → `Runtime.evaluate`:

```javascript
// Coletar imagens (role a página antes se lazy-load)
[...document.querySelectorAll('img')].map(i => i.currentSrc).filter(Boolean)

// Coletar textos principais
document.body.innerText
```

## Regras invioláveis

1. **Nenhum fato inventado — texto APRIMORADO.** Serviços, credenciais, contatos vêm do original. Reescreva com copy melhor.
2. **Fotos e logo originais OBRIGATÓRIOS.** URLs via `img.currentSrc` no browser.
3. **Identidade preservada.** Logo, paleta, fotos. Refinar tons se fracos — nunca trocar família de cores.
4. **Mais completo que o original.** Seções relevantes com informação real: prova social Google, como funciona, localização, horários, FAQ respondível.
5. **Arquivo único.** `sites/[slug]/[slug].html` autocontido: CSS inline, sem build.
6. **Mobile-first.** Testar mentalmente em 375px.
7. **Editor sempre.** Gere `[slug]-editor.html` com camada de `references/editor-visual.md`.
8. **Comparador sempre.** Atualize `comparar.html` via `references/comparador-template.html`.

## Estrutura da página

1. **Hero**: nome + especialidade, promessa, CTA WhatsApp, foto
2. **Prova social**: nota Google real + 2-3 trechos de avaliações
3. **Serviços**: cards com âncoras ou WhatsApp pré-preenchido
4. **Sobre**: formação e credenciais reais
5. **Oferta estruturada** (se fizer sentido): opções sem preços → WhatsApp
6. **Localização**: endereço, mapa iframe, horários, telefone
7. **Rodapé**: registro de classe se existir

## Copywriting

- Headline = benefício, não rótulo
- PAS suave ao longo da página
- Escaneabilidade: blocos curtos, bullets, subtítulos narrativos
- 1 CTA por dobra, orientado à ação
- Proibido: clichês vazios, superlativos inventados

## Padrão estético

- Tipografia: serif elegante (Playfair, Fraunces, Lora) + sans limpa (Inter, Sora, DM Sans)
- Espaçamento generoso: 80-120px entre seções
- Paleta: cor da marca + neutros + destaque CTA. Contraste AA
- Botão WhatsApp flutuante fixo
- Sem carrosséis, sem JS além do essencial

## Checklist final

- [ ] Zero placeholder / lorem ipsum
- [ ] CTAs para contato REAL
- [ ] WhatsApp formato wa.me correto (55 + DDD + número)
- [ ] Responsivo 375px e 1440px
- [ ] Title e meta description preenchidos
- [ ] Logo e fotos originais presentes
- [ ] Editor e comparador gerados

## Referências

- Camada de edição: [references/editor-visual.md](references/editor-visual.md)
- Comparador antes/depois: [references/comparador-template.html](references/comparador-template.html)
