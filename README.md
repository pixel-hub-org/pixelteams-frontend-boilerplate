# Como criar uma nova Landing Page (LP)

Este repositório é um boilerplate para construir Landing Pages com Astro. Ele já contém uma estrutura mínima, componentes reutilizáveis e guias rápidos para começar para facilitar o uso da nossa bela equipe.

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

Execute os comandos a partir da raiz do projeto, em um terminal:

- `npm install` — instala dependências.
- `npm run dev` — inicia o servidor de desenvolvimento.
- `npm run build` — gera a build de produção.
- `npm run preview` — serve a build para preview.

## Guia de uso detalhado

1. Clonar o repositório e instalar dependências

```bash
git clone git@github.com:pixel-hub-org/pixelteams-frontend-boilerplate.git
cd pixelteams-frontend-boilerplate
npm install
```

2. Rodar em desenvolvimento

```bash
npm run dev
```

- Abra o endereço mostrado no terminal (padrão: http://localhost:4321).

3. Criar uma nova Landing Page

- Crie a pasta `src/pages/<nome-da-lp>/`.
- Crie `src/pages/<nome-da-lp>/index.astro` com algo como:

```astro
---
import BaseLayout from "../../layouts/BaseLayout.astro";
import Hero from "../../components/Hero.astro";
import CTA from "../../components/CTA.astro";
---
<BaseLayout>
	<Hero title="Título da LP" subtitle="Descrição curta">
		<CTA slot="cta" href="#" label="Experimentar" />
	</Hero>

	<section class="max-w-4xl mx-auto px-6 py-12">
		<h2 class="text-2xl font-semibold mb-4">Recursos</h2>
		<p class="text-slate-600">Descreva por que seu produto é legal.</p>
	</section>
</BaseLayout>
```

4. Assets e dados

- Coloque imagens específicas da LP em `src/assets/<nome-da-lp>/` ou em `public/` quando quiser servir diretamente.
- Dados estáticos (JSON/TS) em `src/data/<nome-da-lp>.ts` e importe na sua página.

5. Estilos

- Use Tailwind (já configurado via `src/styles/global.css`) com classes utilitárias.
- Tokens de design (variáveis) em `src/styles/tokens/variables.css`.

6. Lint, formatação e build

```bash
npm run lint
npm run prettier
npm run build
npm run preview
```

7. Deploy rápido

- Vercel ou Netlify: conecte o repositório, configure o build command como `npm run build` e o publish directory como `dist/`.
- Se usar CI, garanta que a pipeline execute `npm ci` e `npm run build`.

8. Boas práticas

- Trabalhe em branches por feature/LP e abra PRs para revisão.
- Use `CODEOWNERS` + branch protection para exigir revisões em áreas críticas.
- Teste responsividade e acessibilidade (alt, foco, contraste).

## Recursos

- Documentação Astro: https://docs.astro.build
- Mini guia Astro: [ASTRO_MINI_GUIDE.md](ASTRO_MINI_GUIDE.md)
