# Takahashi Logs

Blog pessoal minimalista em preto e branco com foco em conteúdo escrito em **Markdown (`.md`)**.

---

## 🌟 Características

- **Estética Minimalista Preto e Branco**: Design editorial limpo, elegante e de alto contraste, com suporte nativo aos modos **Claro** e **Escuro** (sem flash de tema ao recarregar).
- **Imagens em Destaque**: Todo o texto, botões e bordas seguem o padrão monocromático, permitindo que as imagens e diagramas adicionados aos posts se destaquem com 100% de suas cores naturais.
- **Conteúdo 100% em Markdown**: Crie e gerencie seus artigos diretamente como arquivos `.md` na pasta `src/content/blog/`.
- **Ultra Rápido (Astro)**: Geração de páginas HTML estáticas, zero JavaScript desnecessário no cliente e nota máxima em performance/SEO.
- **Destaque de Código**: Syntax highlighting automático integrado para blocos de código com Shiki (adaptando-se aos temas claro e escuro).
- **Organização por Tópicos / Tags**: Sistema automático de tags e filtros.
- **Feed RSS & Sitemap**: Endpoints automáticos em `/rss.xml` e `/sitemap-index.xml`.

---

## 🌿 Estrutura de Branches (Fluxo de Publicação)

O repositório é organizado com um fluxo simples e seguro para separação de rascunhos e produção:

- **`main`**: Branch principal e de produção. Contém apenas os artigos finalizados e publicados. Seu serviço de hospedagem (Vercel, Cloudflare, etc.) deve apontar para esta branch.
- **`drafts`**: Branch de produção de conteúdo. É onde novos artigos são iniciados, rascunhados e desenvolvidos sem risco de irem ao ar prematuramente.

### Como trabalhar no dia a dia:

1. **Escrever uma nova matéria**:
   ```bash
   git checkout drafts
   ```
   Crie ou edite seu arquivo `.md` em `src/content/blog/`, visualize localmente com `npm run dev` e comite:
   ```bash
   git add src/content/blog/meu-novo-artigo.md
   git commit -m "feat(content): rascunho do artigo sobre X"
   git push origin drafts
   ```

2. **Publicar a matéria finalizada**:
   Quando o artigo estiver concluído e pronto para ir ao ar no blog:
   ```bash
   git checkout main
   git merge drafts
   git push origin main
   ```
   *(Ou abra um Pull Request de `drafts` para `main` diretamente no GitHub).*

---

## 🚀 Como Executar Localmente

### 1. Iniciar servidor de desenvolvimento local
```bash
npm run dev
```
Acesse no seu navegador: `http://localhost:4321`

### 2. Gerar versão de produção
```bash
npm run build
```
Os arquivos estáticos otimizados serão gerados na pasta `dist/`.

### 3. Visualizar a versão de produção localmente
```bash
npm run preview
```

---

## ✍️ Como Criar uma Nova Matéria

Para publicar um novo artigo, basta criar um novo arquivo `.md` em `src/content/blog/`, por exemplo: `src/content/blog/minha-nova-materia.md`.

No topo do arquivo, adicione o cabeçalho (*frontmatter*):

```yaml
---
title: "Título da Sua Matéria"
description: "Uma breve descrição resumindo o artigo."
pubDate: 2026-10-19
heroImage: "/images/minha-imagem.png" # opcional
tags: ["tecnologia", "desenvolvimento"]
draft: false # mude para true se ainda estiver rascunhando
---

Escreva seu texto aqui normalmente usando Markdown!

## Um subtítulo

- Listas
- Links [como este](https://exemplo.com)
- **Negrito** e *itálico*

```python
def ola_mundo():
    print("Suporte automático para blocos de código!")
```
```

### Adicionando Imagens às Matérias

1. Coloque seus arquivos de imagem (`.png`, `.jpg`, `.webp`, `.svg`, etc.) dentro da pasta `public/images/`.
2. No seu arquivo `.md`, referencie a imagem assim:

```markdown
![Texto alternativo da imagem](/images/minha-imagem.png)
```

As imagens manterão suas cores originais, destacando-se de forma limpa sobre o design preto e branco.

---

## 📁 Estrutura de Arquivos

```
.
├── public/
│   ├── favicon.svg             # Favicon monocromático
│   └── images/                 # Imagens dos artigos
├── src/
│   ├── components/
│   │   ├── Footer.astro        # Rodapé
│   │   ├── FormattedDate.astro # Formatador de data
│   │   ├── Header.astro        # Cabeçalho e navegação
│   │   ├── PostCard.astro      # Card de resumo do post
│   │   └── ThemeToggle.astro   # Alternador Claro / Escuro
│   ├── content/
│   │   └── blog/               # 📝 SEUS ARTIGOS .MD FICAM AQUI
│   │       ├── bem-vindo-ao-takahashi-logs.md
│   │       └── arquitetura-limpa-tipos-programação.md (em drafts)
│   ├── layouts/
│   │   ├── BaseLayout.astro    # Shell principal com meta tags
│   │   └── BlogPostLayout.astro# Layout de leitura das matérias
│   ├── pages/
│   │   ├── index.astro         # Página inicial com lista de posts
│   │   ├── about.astro         # Página Sobre
│   │   ├── 404.astro           # Página 404
│   │   ├── rss.xml.ts          # Gerador do feed RSS
│   │   ├── posts/[...slug].astro # Rota dinâmica dos posts
│   │   └── tags/[tag].astro    # Rota dinâmica dos tópicos
│   ├── styles/
│   └── utils/
├── astro.config.mjs
├── package.json
└── tsconfig.json
```

---

## ☁️ Deploy

Como o projeto gera HTML estático puro, ele pode ser hospedado gratuitamente e com deploy automático via Git em qualquer serviço:

- **Vercel**: Importe o repositório Git, o framework `Astro` é detectado automaticamente.
- **Cloudflare Pages**: Conecte ao Git, comando `npm run build` e diretório de saída `dist`.
- **GitHub Pages**: Configure a GitHub Action oficial do Astro (`withastro/action`).
- **Netlify**: Detecção automática de build Astro.
