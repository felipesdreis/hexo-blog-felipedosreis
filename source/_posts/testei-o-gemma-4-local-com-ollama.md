---
title: Testei o Gemma 4 local com Ollama — qual variante vale a pena?
date: 2026-09-22 10:00:00
tags:
  - IA
  - Ollama
  - LLM local
categories:
  - Tecnologia
---

O Google lançou o [Gemma 4](https://deepmind.google/models/gemma/gemma-4/) e, como já uso modelos locais no dia a dia via **Ollama**, resolvi baixar as principais variantes e rodar o mesmo teste em todas. Nada elaborado — três perguntas simples, sempre as mesmas, pra ver onde cada tamanho de modelo começa a errar e qual a velocidade real na minha máquina.

---

## O teste

Usei três perguntas que parecem triviais, mas pegam erros comuns de modelo pequeno:

1. **Correção de texto** — um parágrafo com erros de gramática, ortografia, pontuação e crase pra corrigir.
2. **Contagem de letras** — quantas vezes a letra "r" aparece em "paralelepípedo".
3. **Um puzzle de nomes** — o pai de Maria tem 5 filhas: Lala, Lele, Lili, Lolo e... qual o nome da quinta? (pegadinha: é "Maria", a própria pergunta já dá a resposta — não segue o padrão dos outros nomes).

Rodei as mesmas três perguntas em seis variantes do Gemma 4, todas via Ollama, e anotei a velocidade em tokens/segundo e quais tarefas cada uma acertou ou errou.

---

## Ambiente dos testes

Pra quem for comparar com a própria máquina, os testes rodaram em:

- **CPU:** AMD Ryzen 5 5600 (6 núcleos / 12 threads)
- **GPU:** NVIDIA RTX 4060, 8GB VRAM 
- **RAM:** 32GB
- **SO:** Windows 11 Pro 
- **Runtime:** Ollama

Isso importa porque a velocidade despenca quando o modelo não cabe inteiro na VRAM — dá pra ver isso acontecer no `12b-it-qat` mais abaixo.

---

## Resultado comparativo

| Modelo | Velocidade | Acertos | Observação |
|---|---|---|---|
| `gemma4:e2b-it-q8_0` | 77 tok/s | 2/3 (errou a do nome) | Usa "think" em todas, sem exagero |
| `gemma4:e4b` | 62 tok/s | 2/3 (errou a do nome) | Não usou "think" |
| `gemma4:e2b` | 109 tok/s | 2/3 (errou a contagem de letras) | A mais rápida do teste |
| `gemma4:e4b-it-qat` | 65 tok/s | 1/3 (errou letras e nome) | Nem usou "think" na primeira |
| `gemma4:12b-it-qat` | 10 tok/s | 3/3 | Não cabe na VRAM — processamento cai pra CPU/RAM |
| `gemma4:26b-a4b-it-qat` | 26 tok/s | 3/3 | É MoE, por isso mantém velocidade razoável mesmo maior |

O padrão que apareceu: os modelos **e2b/e4b** são rápidos mas erram a pergunta do "nome da quinta filha" — provavelmente porque ela exige ignorar o padrão óbvio (nomes terminados em -la/-lo) e prestar atenção ao que já foi dito no enunciado. Só os modelos a partir de **12b** pegaram essa pegadinha consistentemente.

O `26b-a4b-it-qat` chamou atenção por ser MoE (Mixture of Experts): tem mais parâmetros que o `12b-it-qat`, mas roda mais rápido porque só ativa parte da rede por token — e ainda assim acertou tudo.

---

## Minha conclusão

Pra tarefas simples do dia a dia — corrigir texto, resumir, bater papo — fico com o **`gemma4:e2b-it-q8_0`**: é rápido o suficiente e o único erro que teve foi numa pegadinha, não em algo que realmente atrapalha esse tipo de uso.

Já pra trabalhos com **agentes**, onde precisão e raciocínio em múltiplos passos pesam mais que velocidade bruta, vou de **`gemma4:26b-a4b-it-qat`**: acertou tudo e, por ser MoE, ainda mantém uma velocidade que não trava o fluxo — bem melhor que o `12b-it-qat`, que empaca ao estourar a VRAM.
