# Mini guia: Como usar Astro neste boilerplate

Este documento rápido explica os conceitos principais do Astro e como trabalhar neste boilerplate para criar Landing Pages (LPs). É pensado para desenvolvedores que nunca usaram Astro antes.

## O que é o Astro?

- Astro é um framework para construir sites estáticos ou híbridos. Ele permite usar componentes em formato `.astro` e também componentes de frameworks (React, Svelte, Vue, etc.), mas por padrão encoraja HTML estático renderizado no build para performance.

## Estrutura mínima do projeto

- `src/pages/` — Rotas do site. Cada arquivo `.astro` ou `.md` vira uma rota. Ex: `src/pages/index.astro` => `/`
- `src/components/` — Componentes reutilizáveis (.astro, .jsx, .tsx, etc.).
- `src/layouts/` — Layouts que envolvem páginas (ex.: `BaseLayout.astro`).
- `src/styles/` — CSS global e tokens (aqui usamos Tailwind + tokens CSS).
- `src/assets/` — Imagens e arquivos estáticos usados nas LPs.
- `src/data/` — Dados estáticos exportados (JSON/TS) para preencher páginas.
- `src/lib/` — Helpers/funções reutilizáveis.

## Como uma página `.astro` funciona (exemplo básico)

Um arquivo `.astro` combina frontmatter (script) com markup:

---

import MeuComponente from "../components/MeuComponente.astro";
const title = "Minha LP";

---

<MeuLayout>
  <section>
    <h1>{title}</h1>
    <MeuComponente prop1="valor" />
  </section>
</MeuLayout>

- A seção entre `---` é o frontmatter: você pode usar imports, lógica JS/TS, carregar dados.
- Depois vem o HTML/JSX-like que é a saída da página.

## Componentes `.astro` — Props e slots

- Props: exporte variáveis no topo do componente.
  Exemplo em `Hero.astro`:

  ***

  export let title = "";
  export let subtitle = "";

  ***

  <h1>{title}</h1>
  <p>{subtitle}</p>

- Slots: permitem passar markup para dentro do componente.
  Exemplo:
  <Hero title="Oi" subtitle="Sub">
  <button slot="cta">Quero</button>
  </Hero>
  No componente `Hero.astro` usar `<slot name="cta" />` ou simplesmente `<slot />`.

### Sobre slots (breve)

- O que é: `<slot />` é o ponto onde o conteúdo passado por quem usa o componente (ou layout) será renderizado. Em layouts, é a forma padrão de injetar o conteúdo da página.
- Exemplo prático (seu `BaseLayout.astro`):

```astro
<body>
  <Header />
  <main class="min-h-[70vh]">
    <slot />
  </main>
  <Footer />
</body>
```

Tudo que você colocar dentro de `<BaseLayout>...</BaseLayout>` aparece onde está `<slot />`.

- Slot nomeado: use `<slot name="cta" />` no componente e passe `slot="cta"` no filho para posicionar conteúdo em áreas específicas (útil para botões/CTAs dentro de um Hero, por exemplo).

- Fallback: você pode fornecer conteúdo padrão dentro do slot — será mostrado apenas se nada for passado:

```astro
<slot>Conteúdo padrão se nada for passado</slot>
```

- Observações: slots funcionam durante a renderização (SSR/build). Eles não são 'funções' — o pai fornece o markup; o filho define onde exibir. Use slots para tornar layouts e componentes mais flexíveis.

## Importando componentes

- Use caminhos relativos a partir do arquivo que importa.
- Import comum:
  import Header from "../components/Header.astro";
- Dica: prefira paths curtos e consistentes. Para evitar muitos `../../`, mantenha páginas em `src/pages/<nome>/index.astro` e importe `../../components/...` ou configure aliases (avançado).

## Estilos e Tailwind

- Este boilerplate inclui Tailwind na configuração (veja `src/styles/global.css` que importa o Tailwind).
- Use classes utilitárias (ex.: `class="max-w-4xl mx-auto p-6"`) ou crie classes utilitárias/extras em `src/styles/`.
- Tokens CSS: coloque variáveis em `src/styles/tokens/variables.css` e importe/consuma quando precisar.

## Assets (imagens, ícones)

- Coloque arquivos estáticos em `src/assets/<nome-da-lp>/` ou em `public/` para servir direto.
- Referencie imagens com paths a partir da raiz: `/assets/...` ou use import quando precisar do bundler (ex.: `import logo from '../assets/logo.svg'`).

## Scripts úteis (no package.json deste projeto)

- `npm run dev` — Inicia o servidor de desenvolvimento (hot reload).
- `npm run build` — Gera a build de produção na pasta `dist/`.
- `npm run preview` — Serve a build gerada para testar localmente.
- `npm run lint` / `npm run prettier` — Checagens e formatação (configuradas no projeto).

## Boas práticas para LPs

- Mobile-first: teste a página em dispositivos pequenos primeiro.
- Componentização: crie componentes pequenos (Hero, CTA, Features, Pricing, Footer).
- Dados: se a LP precisa de conteúdo repetido, coloque em `src/data/` e importe para a página.
- Acessibilidade: sempre use textos alternativos (`alt`) em imagens, contraste de cores e elementos focáveis.
- Performance: mantenha imagens otimizadas e scripts mínimos.

## Exemplo: criar uma nova LP (passo-a-passo)

1. Criar pasta: `src/pages/minha-lp/`
2. Criar `index.astro` com conteúdo:

---

import BaseLayout from "../../layouts/BaseLayout.astro";
import Hero from "../../components/Hero.astro";
import CTA from "../../components/CTA.astro";

---

<BaseLayout>
  <Hero title="Produto X" subtitle="Descrição curta">
    <CTA slot="cta" href="#" label="Experimentar" />
  </Hero>
  <!-- outras seções: features, depoimentos, rodapé -->
</BaseLayout>

3. Adicionar imagens em `src/assets/minha-lp/`.
4. Se precisar de dados estáticos, crie `src/data/minha-lp.ts` e importe na página.

## Debug/Problemas comuns

- "Import not found": verifique caminhos relativos e se o arquivo existe.
- CSS não aplicando: confirme que `global.css` está importado na página/layout e o Tailwind está configurado.
- Build falha: leia o erro no terminal; muitas vezes falta instalar dependências (`npm install`).

## Recursos para aprender mais

- Documentação oficial: https://docs.astro.build
- Exemplos e templates: https://github.com/withastro/astro/tree/main/examples
