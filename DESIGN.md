---
version: alpha
name: Felipe Reis — Portfólio
description: Single-page pessoal em dark mode para um Solutions Engineer, com verde único de interação sobre fundo quase preto, tipografia condensada em peso extremo (300/700) e um plano de fundo radial em parallax que simula profundidade sem sombra.

colors:
  primary: "#0F0D13"
  secondary: "#E6E1E5"
  tertiary: "#1A915A"
  tertiary-container: "#10633D"
  neutral: "#FFFFFF"

typography:
  h1:
    fontFamily: "Helvetica Now Text"
    fontSize: 104px
  h2:
    fontFamily: "Helvetica Now Text"
    fontSize: 64px
  label-caps:
    fontFamily: "Helvetica Now Text"
    fontSize: 15px
  body-lg:
    fontFamily: "Helvetica Now Text"
    fontSize: 32px
  body-md:
    fontFamily: "Helvetica Now Text"
    fontSize: 16px
  mono:
    fontFamily: "Roboto Mono"
    fontSize: 12px

rounded:
  sm: 6px
  md: 20px
  lg: 50px
  full: 9999px

spacing:
  sm: 8px
  md: 24px
  lg: 48px

components:
  button-primary:
    backgroundColor: "linear-gradient(45deg, {colors.tertiary-container}, {colors.tertiary})"
    textColor: "{colors.neutral}"
    rounded: "{rounded.lg}"
    padding: "16px 36px"
  button-secondary:
    backgroundColor: "{colors.tertiary}"
    textColor: "{colors.neutral}"
    rounded: "{rounded.full}"
    padding: "8px 22px"
  button-glass:
    backgroundColor: "rgba(118, 118, 118, 0.3)"
    textColor: "{colors.neutral}"
    rounded: "{rounded.full}"
    padding: "11px 26px"
  badge:
    backgroundColor: "rgba(26, 145, 90, 0.15)"
    textColor: "{colors.tertiary}"
    rounded: "{rounded.sm}"
    padding: "4px 12px"
---

## Overview

O portfólio de Felipe Reis é uma single page de rolagem longa que troca qualquer chrome de UI tradicional (cards com sombra, grids visíveis, paleta colorida) por um fundo quase preto (`#0F0D13`) e uma única cor viva — o verde `#1A915A` — reservada para tudo que é interativo: links de navegação em hover, rótulos de seção, CTAs e badges de tecnologia. A tipografia salta entre dois extremos de peso (300 no corpo, 700 em títulos e rótulos), sem pesos intermediários, o que cria hierarquia por contraste em vez de por cor. A profundidade da página não vem de `box-shadow`: vem de um plano de fundo fixo com três gradientes radiais verdes sutis (`app.component.css`, `.bg-parallax-layer`) que se desloca discretamente com o scroll via `ParallaxDirective`, e de vidro translúcido (`backdrop-filter: blur`) na navbar e nos botões sociais do hero. Esses tokens de cor e forma não nasceram deste projeto — são o mesmo verde/gradiente/pílula que uma versão anterior deste `DESIGN.md` documentou a partir da landing do Rolex Submariner, usada como referência de estilo para o redesign do dark mode; este arquivo agora documenta o resultado real aplicado ao portfólio, não mais a referência.

## Colors

- **Primary `#0F0D13`** — fundo dominante de toda a página; é a superfície sobre a qual tudo (texto, cards, gradiente de fundo) é desenhado. Variações mais claras do mesmo fundo (`--color-bg-raised: #1C1B1F`) aparecem só no hover de cards de projeto.
- **Secondary `#E6E1E5`** — cor de leitura principal (nome no hero, headings, texto de projeto). Um branco levemente acinzentado, não branco puro, para reduzir o contraste agressivo sobre o fundo escuro.
- **Tertiary `#1A915A`** — o único acento cromático do site. Aparece em rótulos de seção ("Sobre", "Stack", "Projetos"), linhas decorativas, hover de links/pills/cards, badges de tag e como ponta clara do gradiente dos botões. Se algo no site "chama atenção" por cor, é sempre este verde.
- **Tertiary-container `#10633D`** — tom mais escuro do mesmo verde, usado exclusivamente como ponta inicial dos gradientes diagonais de CTA (nunca sozinho).
- **Neutral `#FFFFFF`** — branco puro, usado como cor de texto sempre que o fundo do elemento já é o verde sólido ou o vidro translúcido (botões, badges de CTA) — nunca como cor de fundo de seção.

## Typography

Família declarada: **Helvetica Now Text** (`--font-family-base`, fallback `Helvetica, Arial, sans-serif`) para todo o texto corrido, e **Roboto Mono** (`--font-family-mono`, carregada via Google Fonts em `index.html`) para elementos que remetem a dado/código: itens do ticker de stack, tags de projeto e copyright do rodapé.

- **h1** (`104px` no desktop, weight 700, letter-spacing `-3px`) — o nome "Felipe Reis" no hero, tratado como wordmark de página inteira. No CSS real é `clamp(56px, 9vw, 104px)`; o token registra o teto, mas o tamanho encolhe fluidamente até 56px em telas estreitas.
- **h2** (`64px` no desktop, weight 700, letter-spacing `-1px`) — chamada da seção Blog ("Ideias, projetos e experimentos"). CSS real: `clamp(36px, 5.5vw, 64px)`.
- **label-caps** (`15px`, weight 700, uppercase, letter-spacing `4px`, cor `{colors.tertiary}`) — rótulo curto que abre cada seção, sempre acompanhado de uma linha de 32px na mesma cor.
- **body-lg** (`32px` no desktop, weight 300) — o parágrafo de abertura da seção Sobre, mais leve e maior que o corpo comum. CSS real: `clamp(22px, 3.2vw, 32px)`.
- **body-md** (`14–20px`, weight 300) — descrições de projeto, texto do blog e corpo geral; o peso 300 mantém o texto discreto diante dos títulos em 700.
- **mono** (`10–14px`, weight 300/700) — usada só onde o conteúdo "parece dado": stack no ticker, tags de tecnologia nos cards, copyright do rodapé.

**Ressalva real:** `Helvetica Now Text` é uma fonte comercial da Monotype e **não é carregada** em nenhum lugar do projeto (nem `@font-face`, nem Google Fonts — só Roboto Mono e Material Icons são baixados em `index.html`). Na prática, para praticamente todo visitante, o texto renderiza no fallback `Helvetica, Arial, sans-serif` do sistema, não na fonte nomeada. O efeito visual pretendido (pesos 300/700 bem contrastados) só é 100% fiel em sistemas Apple, onde "Helvetica" do SO já cobre bem esses pesos.

## Layout

Single page com seções empilhadas verticalmente (`#home`, `#sobre`, `#stack`, `#projetos`, `#blog`), cada uma limitada a `max-width: 900–960px` e centralizada, com padding horizontal consistente de `{spacing.lg}` (48px) no desktop caindo para `{spacing.md}` (24px) no breakpoint de 768px — a mesma dupla de valores se repete em nav, hero, todas as seções e rodapé, funcionando como a única escala de espaçamento horizontal do site. Cada seção interna começa com uma borda superior de 1px (`--color-border`) e `padding-top: 80px`, criando separação sem caixas fechadas. O grid de projetos é a única exceção ao empilhamento vertical: `repeat(auto-fit, minmax(380px, 1fr))` com gap de 1px preenchido pela cor de borda, simulando uma tabela de células dentro de um contêiner arredondado (`{rounded.md}`).

## Elevation & Depth

Não há `box-shadow` estático em nenhum componente — a única sombra do CSS é um anel de pulso (`pulse-ring`) disparado no hover do avatar do hero, e mesmo esse é uma animação, não uma elevação permanente. A profundidade vem de duas fontes: (1) o **plano de fundo fixo** (`.bg-parallax-layer`) com três `radial-gradient`s verdes semitransparentes sobre `{colors.primary}`, que se move com `ParallaxDirective` para sugerir profundidade ao rolar; (2) **vidro translúcido** (`backdrop-filter: blur`) na navbar (`blur(16px)`) e nos botões sociais do hero (`blur(5px)` sobre `rgba(118,118,118,0.3)`), mesma linguagem de "flutuar sobre o fundo" herdada da referência original.

## Shapes

- **`sm` (6px)** — badges pequenos de tecnologia dentro dos cards de projeto.
- **`md` (20px)** — cantos do contêiner do grid de projetos, a única forma "de caixa grande" do site.
- **`lg` (50px)** — o CTA principal do blog, uma pílula quase completa.
- **`full` (9999px)** — todos os outros botões e pills (nav, blog-btn, social-btn, stack-pill) — a forma padrão de qualquer elemento clicável pequeno.
- Círculos perfeitos (`border-radius: 50%`) aparecem à parte, em elementos não retangulares por natureza: avatar do hero e botão de link (↗) dos cards de projeto.

## Components

- **`button-primary`** (`.blog-cta`) — gradiente diagonal `{colors.tertiary-container} → {colors.tertiary}`, texto `{colors.neutral}` em bold, `{rounded.lg}`, padding generoso (`16px 36px`). É o CTA mais "pesado" da página, reservado para levar tráfego ao blog externo.
- **`button-secondary`** (`.blog-btn`, na navbar) — mesmo verde `{colors.tertiary}` só que sólido (sem gradiente) e em pílula completa (`{rounded.full}`), padding mais compacto. Variante de menor destaque do mesmo CTA de blog.
- **`button-glass`** (`.social-btn`) — fundo cinza translúcido com blur, borda semi-transparente na cor do acento, texto `{colors.neutral}`, `{rounded.full}`. Usado só sobre o fundo com gradiente do hero, nunca em contexto de card.
- **`badge`** (`.project-tag`) — fundo verde a 15% de opacidade, texto `{colors.tertiary}`, fonte mono, `{rounded.sm}`. Marca a stack técnica de cada projeto sem competir visualmente com o título do card.
- **card** (`.project-card`) — sem fundo próprio nem sombra; é uma célula dentro do grid de `1px` de borda compartilhada, que só ganha `{colors.bg-raised}` no hover — a "elevação" ao hover é uma troca de tom, não uma sombra.

## Do's and Don'ts

- **Faça** manter o verde (`{colors.tertiary}`) como a única cor de destaque da página inteira — nenhum outro matiz aparece fora dos neutros de fundo/texto e dos dois tons de verde.
- **Faça** usar peso 700 exclusivamente para títulos, rótulos e CTAs, e 300 para todo o resto do texto corrido — o contraste do site depende desse salto abrupto, sem pesos 400/500 no meio.
- **Não** adicione `box-shadow` estático a cards ou botões — a profundidade aqui vem de gradiente radial de fundo e de `backdrop-filter: blur`, nunca de sombra projetada.
- **Não** referencie `Helvetica Now Text` sem também carregá-la via `@font-face`/kit de fontes — hoje ela é só um nome no CSS; todo visitante já está vendo o fallback do sistema.
- **Atenção:** texto branco (`{colors.neutral}`) sobre `{colors.tertiary}` sólido (usado no `button-secondary`, ex. "Blog ↗" da navbar) mede 4.01:1 de contraste — abaixo do mínimo AA de 4.5:1 para texto normal. Passa como "large text" (≥14px bold), que é o caso aqui, mas está no limite; evitar reduzir o peso ou o tamanho desse botão sem revisar o contraste.
