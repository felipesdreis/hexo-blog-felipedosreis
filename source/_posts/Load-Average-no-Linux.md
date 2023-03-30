---
title: Tudo que você precisa saber sobre Load Average no Linux
date: 2023-03-30 12:33:43
tags: Linux
---
## Introdução

O Load Average, também conhecido como carga média do sistema, é um indicador importante para monitorar a quantidade de trabalho que o sistema está processando. É medido em três intervalos de tempo: 1 minuto, 5 minutos e 15 minutos. Quando o Load Average é superior a 1, significa que o sistema está sobrecarregado. Neste post, vamos explorar tudo o que você precisa saber sobre Load Average e como usá-lo para garantir que seu sistema esteja funcionando sem problemas.

## Como o Load Average é calculado?

O Load Average é uma média ponderada do número de processos em execução no sistema. Ele é calculado levando em consideração os processos em estado de execução e aqueles que estão aguardando para serem executados. Por exemplo, um Load Average de 1,5 no intervalo de 1 minuto indica que, em média, o sistema está executando 1,5 processos ao mesmo tempo.

## Por que monitorar o Load Average?

É importante monitorar o Load Average para garantir que o sistema não esteja excedendo sua capacidade de processamento. Se o Load Average estiver constantemente acima de 1, pode ser um sinal de que o sistema está sobrecarregado e pode começar a ficar lento ou travar. Além disso, o monitoramento do Load Average pode ajudar a identificar picos de atividade e a planejar a capacidade do sistema para atender às necessidades de processamento.

## Como visualizar o Load Average?

Existem algumas maneiras de visualizar o Load Average em um sistema Linux. Uma delas é usar o comando `uptime`, que exibe o Load Average nos últimos 1, 5 e 15 minutos. Outra opção é usar o comando `top` e pressionar a tecla `1` para exibir o Load Average de cada CPU. É importante lembrar que o Load Average é um indicador de carga do sistema e deve ser usado em conjunto com outras métricas para uma análise mais completa do desempenho do sistema.

### Exemplos 
*uptime:*
```bash
  14:33:43 up  1:00,  1 user,  load average: 0,00, 0,00, 0,00
```
*top:*
```bash
  top - 14:33:43 up  1:00,  1 user,  load average: 0,00, 0,00, 0,00
```

## Conclusão

O Load Average é um indicador importante para monitorar o desempenho do sistema e garantir que ele esteja funcionando sem problemas. É medido em três intervalos de tempo e indica a quantidade de trabalho que o sistema está processando. É importante monitorar o Load Average para garantir que o sistema não esteja sobrecarregado e para identificar picos de atividade. Use as ferramentas disponíveis, como `uptime` e `top`, para visualizar o Load Average e obter uma análise mais completa do desempenho do sistema.