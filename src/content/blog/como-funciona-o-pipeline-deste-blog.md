---
title: "Como funciona a arquitetura deste blog com Astro e Markdown"
description: "Entenda como cada arquivo .md se transforma em uma página estática veloz, validada por schemas e sem dependências pesadas."
pubDate: 2026-10-15
heroImage: "/images/architecture.svg"
tags: ["astro", "engenharia", "markdown"]
draft: false
---

Um blog para desenvolvedores não precisa de um banco de dados relacional, painel WordPress ou camadas complexas de infraestrutura. 

A arquitetura do **Takahashi Logs** é baseada em três pilares:

1. **Arquivos Markdown locais**: cada artigo é versionado com `git`, podendo ser escrito no seu editor favorito (VS Code, Neovim, Obsidian).
2. **Astro Content Layer**: validação rigorosa de metadados em tempo de compilação via Zod.
3. **HTML e CSS puros**: saída estática que pode ser hospedada gratuitamente em qualquer CDN global (Cloudflare Pages, Vercel, GitHub Pages).

---

## O Fluxo de Construção

Abaixo está o pipeline que processa cada arquivo `.md`:

![Pipeline de compilação do Astro](/images/architecture.svg)
*Figura: Da criação do arquivo Markdown à entrega das páginas estáticas.*

---

## Como criar uma nova matéria

Para publicar um novo artigo no Takahashi Logs, o processo leva menos de um minuto:

1. Crie um arquivo em `src/content/blog/meu-novo-artigo.md`.
2. Adicione os metadados no topo:

```yaml
---
title: "Seu Título Aqui"
description: "Breve resumo do conteúdo."
pubDate: 2026-10-17
tags: ["tecnologia", "notas"]
draft: false
---
```

3. Escreva seu conteúdo normalmente em Markdown.
4. Para adicionar imagens, salve o arquivo em `public/images/` e insira no texto com:

```markdown
![Descrição da imagem](/images/minha-foto.png)
```

5. Rode `npm run build` ou comite no Git — o deploy é imediato!

---

## Conclusão

Essa arquitetura garante que o blog carregue instantaneamente, tenha nota 100 no Google Lighthouse e seja um prazer de manter a longo prazo.
