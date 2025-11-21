# Como criar uma nova Landing Page (LP)

Este repositório é um boilerplate para construir Landing Pages com Astro. Ele já contém uma estrutura mínima, componentes reutilizáveis e guias rápidos para começar.

## Passo a passo rápido

1. Crie uma pasta em `src/pages/` com o nome da LP (ex: `src/pages/my-product/`).
2. Dentro dela crie `index.astro` e use o `BaseLayout` e os componentes existentes:

```astro
---
import BaseLayout from "../../layouts/BaseLayout.astro";
import Hero from "../../components/Hero.astro";
import CTA from "../../components/CTA.astro";
---
<BaseLayout>
	<Hero title="Título da LP" subtitle="Descrição curta">
		<CTA slot="cta" href="#signup" label="Começar grátis" />
	</Hero>
	<!-- restante da página -->
</BaseLayout>
```

3. Adicione imagens/ícones em `src/assets/<nome-da-lp>/`.
4. Dados estáticos podem ficar em `src/data/<nome-da-lp>.ts`.
5. Se precisar de hooks, use `src/hooks/`.

## Comandos úteis

All commands are run from the root of the project, from a terminal:

- `npm install` — instala dependências.
- `npm run dev` — inicia o servidor de desenvolvimento.
- `npm run build` — gera a build de produção.
- `npm run preview` — serve a build para preview.

## Recursos

- Documentação Astro: https://docs.astro.build
- Mini guia Astro: [ASTRO_MINI_GUIDE.md](ASTRO_MINI_GUIDE.md)
