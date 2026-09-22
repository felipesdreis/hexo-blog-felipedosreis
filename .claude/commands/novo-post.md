---
description: Escreve um novo post para o blog no estilo de Felipe — conversacional, baseado em experiência própria, com estrutura de tutorial ou review.
allowed-tools: Read, Write, Glob, Bash
---

Você vai escrever um novo post para o blog Hexo de Felipe em pt-br.

**Tema/assunto:** $ARGUMENTS

---

## Perfil de escrita de Felipe

**Tom e voz:**
- Primeira pessoa, conversacional mas profissional
- Ancora o post em experiência própria: conta como o problema apareceu na prática
- Se for tutorial: lista o que já tentou e não funcionou antes de dar a solução
- Honesto sobre limitações pessoais ("embora não me considere um especialista em X")
- Nunca exagera entusiasmo — recomendações vêm com contexto real
- Detalhes concretos: nome do produto, versão, preço em BRL quando relevante

**Estrutura por tipo:**

*Tutorial/How-to:*
1. Introdução com o problema pessoal (como aconteceu com Felipe)
2. Entendendo o problema (contexto técnico resumido)
3. O que não funcionou (tentativas frustradas — humaniza e poupa tempo do leitor)
4. A solução (passo a passo claro)
5. Medidas extras / aprofundamento (opcional)
6. Como verificar se funcionou (opcional, mas valorizado)
7. Conclusão curta e direta

*Review de produto:*
1. Introdução com contexto de uso (por que comprou/testou)
2. Seções por ângulo (design, conforto, som, etc.) — cada uma com H2
3. Conclusão com veredicto, preço pago e onde comprou

**Formatação obrigatória:**
- H2 (`##`) para seções principais, H3 (`###`) para subseções
- Separadores `---` entre seções
- Negrito nos termos-chave, nomes de ferramentas/produtos
- Itálico para exemplos de prompts ou comandos inline
- Listas para passos e dicas práticas
- Blocos de código para comandos técnicos
- Conclusão: no máximo 3 parágrafos, sem enrolação

---

## O que fazer

1. Identifique o tipo do post (tutorial, review, opinião) com base no assunto fornecido
2. Se necessário, pergunte ao Felipe **no máximo 3 coisas** que precisam ser específicas para o post ser autêntico (ex: qual produto testou, qual problema aconteceu, qual foi a solução encontrada)
3. Escreva o post completo com front matter Hexo correto:

```yaml
---
title: <título em português, descritivo e direto>
date: <data atual no formato YYYY-MM-DD HH:MM:SS>
tags:
  - <tag relevante>
  - <tag relevante>
categories:
  - <Tutoriais | Reviews | Opinião | etc>
---
```

4. Salve o arquivo em `source/_posts/<titulo-em-kebab-case-pt-br>.md`
5. Rode `npx hexo generate` para verificar que não há erros de build

**Não invente detalhes pessoais.** Se precisar de informação específica (qual microfone usou, qual foi o erro exato), pergunte antes de escrever.
