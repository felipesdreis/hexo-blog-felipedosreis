---
title: "Hyperframes: crie vídeos com HTML e Claude Code"
date: 2026-06-11 10:00:00
tags:
  - Claude Code
  - IA
  - Produtividade
  - Vídeo
categories:
  - Tutoriais
---

Estava procurando uma forma de criar vídeos para TikTok e Reels sem precisar abrir o CapCut ou o Premiere, sem esperar by API ou depender de IA generativa de vídeo. Queria algo programático, que coubesse na minha workflow de desenvolvedor — basicamente, descrever o vídeo, o Claude Code escrever o código, e eu renderizar. Descobri o **Hyperframes** testando ferramentas de criação de conteúdo e foi exatamente o que estava procurando. Agora estou usando para adicionar **motion graphics** nos meus vídeos — animações sincronizadas, transições shader, efeitos de texto — tudo que faltava para polir o conteúdo sem precisar sair do terminal.

---

## O que é o Hyperframes

**Hyperframes** é um framework open-source feito pela HeyGen que converte HTML em MP4 determinístico. O mantra é direto: "Write HTML. Render video. Built for agents."

Em vez de usar timeline editors ou formatos proprietários, você define vídeos da mesma forma que constrói páginas web — com HTML, CSS, JavaScript e animações GSAP. O framework captura cada frame usando a API `beginFrame` do Chrome (dando-lhe captura frame-perfeita e buscável) e codifica o resultado com FFmpeg.

O resultado? Um MP4 que você pode publicar no YouTube, TikTok, Reels, ou onde quiser.

---

## Por que é diferente

Hyperframes não é um editor de timeline visual. Não é um SaaS que gera vídeo por prompt (tipo Sora ou Runway). Não é um template maker.

É uma biblioteca que entende que **código é a linguagem natural de um desenvolvedor**. Se você sabe escrever HTML/CSS/JS, já sabe os conceitos principais:

- `data-start` e `data-duration` definem quando cada elemento aparece
- **GSAP timelines** controlam animações frame-a-frame
- **CSS** estiliza tudo — fontes, cores, layouts respondem como em qualquer site
- O engine captura a página renderizada no Chrome e converte em vídeo

É determinístico: mesmo HTML de entrada, sempre o mesmo vídeo de saída. Nenhuma randomicidade. Isso importa muito para CI/CD e pipelines automatizadas.

---

## A integração com Claude Code

O diferencial real está aqui: **Hyperframes é feito especificamente para AI coding agents**, e Claude Code é o alvo primário.

Você instala os skills do Hyperframes uma vez:

```bash
npx hyperframes skills --claude
```

Pronto. Claude Code ganha **3 slash commands nativos**:

- **`/hyperframes`** — escrever compositions HTML. Você descreve o vídeo em linguagem natural, o Claude escreve o HTML com timing certo.
- **`/hyperframes-cli`** — operar o CLI. Init de projetos, rodar preview, renderizar MP4.
- **`/hyperframes-media`** — assets e utilities. Transcrição via Whisper, TTS local com Kokoro (sem API key), remover fundo automático com IA local.

Os skills também podem ser instalados via:

```bash
npx skills add heygen-com/hyperframes
```

E isso funciona não só no Claude Code, mas em qualquer agente IA (Cursor, Gemini CLI, etc.).

---

## Na prática: criando um vídeo

O fluxo é simples:

**1. Descrever no Claude Code**

Você abre o Claude Code e usa o skill:

```
/hyperframes: crie um vídeo 9:16 de 15 segundos para TikTok. Título "Introdução ao Claude Code" que fade-in nos primeiros 2 segundos, depois uma legenda animada abaixo com bouncy effect, e voiceover narrando os conceitos de context management.
```

Claude escreve o HTML com `class="clip"`, `data-start`, `data-duration`, GSAP timelines — tudo que é necessário.

**2. Preview local**

```bash
npx hyperframes preview
```

Abre uma UI no navegador. Você vê o vídeo em tempo real, ajusta o timing, as cores. Se quiser mudar algo, volta pro Claude Code, pede para ajustar.

**3. Render**

```bash
npx hyperframes render --output video.mp4
```

Espera uns segundos. Seu MP4 está pronto.

---

## Economizando tempo com blocos prontos

Hyperframes vem com **50+ blocos reutilizáveis** — data charts, code terminals, shader transitions, social cards, device showcases, maps, text effects.

Instale o que precisa:

```bash
npx hyperframes add animated-title
npx hyperframes add bouncy-captions
npx hyperframes add shader-transition
```

Daí você combina esses blocos numa composition, ou pede pro Claude Code "use o bloco `bouncy-captions` no vídeo".

---

## Caso de uso: conteúdo para redes sociais

Aqui é onde Hyperframes brilha. Você quer criar vídeos 9:16 para TikTok/Reels rapidamente:

- **Títulos animados** com fade-in, scale, ou slide effects
- **Legendas sincronizadas** com narração (TTS local, sem API key — usa Kokoro)
- **Background removal** automático com IA local (u2net)
- **Social cards** com logos, cores da marca, texto
- **Code terminals** se for conteúdo sobre desenvolvimento

Exemplo de prompt real que você pode passar pro Claude Code:

*"Usando `/hyperframes`, crie um vídeo 9:16 de 20 segundos sobre 'Como o Claude Code economiza tempo de desenvolvimento'. Faça uma intro com o logo do Claude Code (fade-in), depois cuts rápidos de features (context window, MCP tools, agents) com transições shader, e encerre com call-to-action 'Teste agora'."*

O Claude Code escreve o HTML, você faz o preview, ajusta, renderiza.

---

## Opções de rendering

**Local** — Chrome + FFmpeg na sua máquina. Funciona bem, rápido.

**Cloud HeyGen** — servidor remoto renderiza. Você paga por créditos, útil se tiver muitos vídeos ou quiser economizar CPU local.

**AWS Lambda / Google Cloud Run** — rendering distribuído. Cada vídeo em uma função. Ideal para batch processing (render 100 vídeos personalizados em paralelo).

Para conteúdo de redes sociais, local já atende. FFmpeg renderiza um vídeo 9:16 de 15s em segundos.

---

## O passo a passo para começar

Se você quer testar agora:

1. Instale Hyperframes: `npm install -g hyperframes` (ou `npx hyperframes`)
2. Instale os skills: `npx hyperframes skills --claude`
3. Abra Claude Code
4. Use `/hyperframes` para descrever seu primeiro vídeo
5. Rode `npx hyperframes preview` para ver ao vivo
6. Rode `npx hyperframes render --output seu-video.mp4` para exportar

Documentação completa: [hyperframes.mintlify.app](https://hyperframes.mintlify.app/)

---

## Conclusão

Hyperframes é para quem quer tratar vídeo como código. Você descreve em linguagem natural, o Claude Code escreve HTML determinístico, o CLI renderiza. Não há UI visual obrigatória, não há drag-and-drop — apenas composições HTML + automação.

A integração com Claude Code via slash commands fecha o loop perfeitamente. É especialmente útil para criadores de conteúdo tech que já vivem no terminal e no código.

Se você está cansado de abrir editores pesados para cada vídeo de 20 segundos do TikTok, ou se quer versionar seus vídeos no Git (porque afinal, é HTML), o Hyperframes vale a exploração.
