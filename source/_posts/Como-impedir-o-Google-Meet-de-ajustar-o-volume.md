---
title: Como Impedir o Google Meet e o Chrome de Ajustarem Automaticamente o Volume do Seu Microfone
date: 2025-08-12 10:07:37
tags:
  - Google Meet
  - Chrome
  - Microfone USB
  - Áudio
  - Produtividade
categories:
  - Tutoriais
---
## Introdução

Você já entrou em uma reunião online e, de repente, percebeu que sua voz estava mais baixa ou mais alta sem você ter mexido em nada?  
Pois é… isso aconteceu várias vezes comigo usando um **HyperX SoloCast** no Google Meet.

O problema não era o microfone em si, mas sim **o Google Meet (via Chrome)** ajustando automaticamente o ganho de entrada para “normalizar” o áudio.  
O resultado? Meu volume ficava inconsistente, e às vezes eu precisava parar no meio da reunião para corrigir.

Depois de alguns testes e bastante pesquisa, encontrei a solução definitiva para **manter o volume do microfone fixo**, e vou compartilhar todo o passo a passo aqui.

## Entendendo o problema

O Google Meet, assim como outros aplicativos de chamada, usa uma tecnologia chamada **WebRTC** para capturar o áudio.  
Por padrão, o WebRTC ativa algo chamado **AGC (Automatic Gain Control)** — um recurso que aumenta ou reduz o volume do microfone automaticamente.

Isso pode ser bom para quem usa microfones simples, mas para quem quer consistência (streamers, criadores de conteúdo, quem trabalha com áudio), pode ser um pesadelo.

## Tentativas iniciais que não funcionaram

- Ajustar o volume manualmente no **Painel de Controle do Windows** → sempre voltava a mudar.
- Procurar alguma configuração no **Google Meet** para desligar → não existe.
- Desconectar e reconectar o microfone → não resolveu.
- Testar outro navegador sem configurar nada → mesmo problema.

Foi aí que comecei a investigar mais a fundo como o Chrome lida com o áudio.


## A solução principal no Google Chrome/Edge

O truque está em desativar uma **flag experimental do navegador** que permite ao WebRTC controlar o volume de entrada.

### Passo a passo

1. Abra o Chrome e digite na barra de endereços: chrome://flags *(No Microsoft Edge, use `edge://flags`)*
2. Use a barra de busca da página e procure por: *Allow WebRTC to adjust the input volume*
3. Altere de **Default** para **Disabled**.
4. Clique no botão **Relaunch** para reiniciar o navegador e aplicar a mudança.

Pronto! Agora o Google Meet não vai mais alterar o ganho do seu microfone automaticamente.

## Medidas extras no Windows para blindar o microfone

Mesmo desativando a flag no Chrome, é bom configurar o Windows para impedir que outros aplicativos façam ajustes automáticos.

### 1. Desativar “Modo Exclusivo”
- Painel de Controle → **Som** → aba **Gravação**.
- Selecione o seu microfone → **Propriedades**.
- Aba **Avançado** → desmarque:
- “Permitir que aplicativos assumam o controle exclusivo deste dispositivo”.
- “Dar prioridade a aplicativos em modo exclusivo”.

### 2. Configurações de Comunicações
- Painel de Controle → **Som** → aba **Comunicações**.
- Marque **“Não fazer nada”**.

### 3. Desativar aprimoramentos
- Ainda nas **Propriedades do microfone**, procure pela aba **Aprimoramentos** (se existir).
- Marque **“Desativar todos os aprimoramentos”** ou desative cada um manualmente.

## Como testar se deu certo

1. Deixe aberta a janela **Níveis** do microfone no Painel de Controle.
2. Entre em uma reunião de teste no Google Meet.
3. Fale normalmente e veja se o **slider de volume** se mexe sozinho.
4. Se ele ficar estático no valor que você configurou, a missão foi cumprida!

## Resultado final

Depois de aplicar a mudança na flag do Chrome e as configurações extras no Windows, meu **HyperX SoloCast** parou de ter o volume alterado sozinho.  
Agora, tenho **áudio consistente** em todas as reuniões, gravações e transmissões.