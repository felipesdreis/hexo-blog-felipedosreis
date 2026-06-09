---
title: Context Management no Claude Code — quando a memória fica cheia
date: 2026-06-09 14:30:00
tags:
  - Claude Code
  - Produtividade
  - IA
categories:
  - Tutoriais
---

Depois de algumas sessões longas no Claude Code, comecei a notar que a janela de contexto estava enchendo — e o Claude começava a sumarizar conversas antigas automaticamente. Aí entendi: **context management não é um detalhe**, é algo que afeta diretamente sua produtividade. E mais importante: qual modelo você escolhe em cada momento importa muito.

---

## O que é context window e por que importa

Pense no context window como a **memória de trabalho** do Claude. Cada arquivo que você lê, cada comando que roda, cada ferramenta que invoca — tudo consome espaço dessa memória. Quando você tem uma conversa longa, muitos arquivos grandes ou está usando muitas tools ao mesmo tempo, essa memória fica cheia.

Quando o limite é atingido, o Claude **compacta a conversa automaticamente**, sumarizando pontos antigos e removendo resultados de tool calls desnecessários. Funciona, mas pode perder detalhes — e você vai notar que as respostas ficam mais genéricas.

O tamanho do context window é o mesmo para todos os modelos (200k tokens), mas a **velocidade de consumo é diferente**. Um **Opus processa mais contexto por resposta**, enquanto um **Haiku consome muito menos** fazendo praticamente o mesmo trabalho para tarefas simples.

---

## Como descobri que estava desperdiçando contexto

Eu estava **reservando Opus só para as coisas complexas**, o que faz sentido. Mas continuava vendo `Compacting conversation...` aparecer com frequência demais. O problema não era só escolher o modelo certo — era **ficar muito tempo na mesma sessão**.

Uma investigação de bug que se estendia por 3–4 horas, uma refatoração longa — o contexto ia inchando, o Claude ia sumarizando, e no final eu acabava redigitando informações que já tinha passado porque a compactação tinha perdido os detalhes.

Aí tentei algumas coisas:
- **Usar `/compact` manualmente** — funcionava, mas interrompia o fluxo
- **Rodar `/clear` e recomeçar** — perdia histórico importante
- **Fechar e reabrir a aba** — temporário, problema voltava em poucas horas

Nenhuma dessas era a solução real. A resposta estava em **ser mais estratégico com ferramentas e modelos**.

---

## A descoberta: Haiku para exploração, economizar o contexto

Comecei a experimentar e descobri algo óbvio em retrospecto:

**Para exploração e descoberta de código**, um **Haiku resolve 90% das vezes**. Quando você está:
- Lendo arquivos para entender a estrutura
- Procurando por funções ou patterns específicos
- Analisando logs ou entendendo erros
- Criando planos de implementação

...Haiku é rápido, mantém contexto baixo e é suficiente. No meu caso, constatei que **gastava a mesma quantidade de tempo explorando com Haiku que com Opus**, mas consumia uma fração do contexto.

**Para tarefas pesadas** (refatorações complexas, design de arquitetura, debugging de lógica intrincada), aí sim Opus faz diferença. Mas isso representa uns 30% do meu tempo real.

---

## Desativar MCPs que você não está usando

Outra descoberta prática: **MCP servers carregam todas as suas tools na memória, mesmo que você não use**. Se você tem 5 MCPs configurados e tá usando só 1, está pagando o preço de contexto dos 4 que não tá tocando.

Meu fluxo agora é:
1. Quando vou **explorar código** → **Haiku** + desativo MCPs desnecessários
2. Quando vou **implementar** → **Sonnet** (suficiente) ou **Opus** (se realmente precisar)
3. Se deixar uma sessão aberta muito tempo → `/compact` quando a compactação automática começa a aparecer

---

## Commands práticos

**Verificar estado do context:**
```
/context
```
Mostra quanto espaço você tá usando, breakdown por categoria, gráfico visual.

**Compactar manualmente:**
```
/compact
```
Útil quando você tá numa sessão longa e quer liberar espaço *sem perder histórico importante*. Sumariza tudo até aquele ponto.

**Limpar e recomeçar:**
```
/clear
```
Zera tudo. Use quando começar uma feature/tarefa nova e não quer viés da conversa anterior.

---

## Dicas que fazem diferença

1. **Seja específico em prompts** — uma instrução vaga parece curta mas força o Claude a explorar mais código pra entender o contexto. No final, custa mais espaço.

2. **Pense em "baterias de sessão"** — em vez de uma sessão de 8 horas, faça 3 sessões de 2–3 horas com `/compact` ou `/clear` entre elas. Contexto fica mais limpo, respostas mais diretas.

3. **Guarde informação importante em CLAUDE.md** — coisas que você quer o Claude lembrar em próximas sessões, salva lá. Não precisa re-digitar.

4. **Escolha o modelo pela tarefa, não pela "qualidade geral"** — Haiku é suficiente pra exploração. Opus é pra quando você realmente precisa.

5. **Monitore a compactação automática** — quando começar a ver `Compacting...` com frequência, é sinal de que tá na hora de compactar manualmente ou limpar.

---

## Conclusão

Context management não é teórico. É a diferença entre **uma sessão de 2 horas produtiva** e **uma sessão de 2 horas onde você fica esperando o Claude reconstruir contexto que já passou**.

Minhas descobertas foram:
- Haiku é suficiente (e mais barato) pra exploração
- Desativar MCPs desnecessários libera contexto imediatamente
- Uma sessão bem compartimentada com `/compact` bate uma maratona contínua
- Escolher o modelo certo pra cada tarefa importa muito

Vale a pena investir uns 5 minutos aprendendo a usar `/context` e `/compact`. O resto vem naturalmente.
