---
title: Como fazer redirecionamento de portas no Windows usando o netsh 
date: 2023-05-04 11:18:50
tags:
- Windows
- Rede
---
O redirecionamento de portas no Windows é uma técnica útil para permitir que o tráfego de rede seja encaminhado de um endereço IP e porta para outro. O comando `netsh` é uma ferramenta poderosa que pode ser usada para fazer o redirecionamento de portas no Windows.

## Passo a passo

1. Abra o prompt de comando como administrador.
2. Digite o seguinte comando para ver a lista de interfaces de rede disponíveis:
    
    ```
    netsh interface portproxy show all
    ```
    
3. Anote o número de índice da interface de rede que você deseja usar para o redirecionamento de portas.
4. Digite o seguinte comando para adicionar uma regra de redirecionamento de porta:
    
    ```
    netsh interface portproxy add v4tov4 listenaddress={endereço IP de origem} listenport={porta de origem} connectaddress={endereço IP de destino} connectport={porta de destino} protocol={tcp|udp}
    ```
    
    Substitua os valores entre chaves pelos valores apropriados para sua situação. Por exemplo, se você quiser redirecionar o tráfego da porta 80 do seu computador para a porta 8080 em outro computador, você pode usar o seguinte comando:
    
    ```
    netsh interface portproxy add v4tov4 listenaddress=127.0.0.1 listenport=80 connectaddress=192.168.1.2 connectport=8080 protocol=tcp
    ```
    
5. Digite o seguinte comando para ver a lista de regras de redirecionamento de porta:
    
    ```
    netsh interface portproxy show v4tov4
    ```
    
    Isso exibirá todas as regras de redirecionamento de porta atuais.
    
6. Para remover uma regra de redirecionamento de porta, digite o seguinte comando:
    
    ```
    netsh interface portproxy delete v4tov4 listenaddress={endereço IP de origem} listenport={porta de origem}
    ```
    
    Novamente, substitua os valores entre chaves pelos valores apropriados para sua situação.
    

## Conclusão

O redirecionamento de portas usando o `netsh` é uma técnica poderosa que pode ser usada para encaminhar o tráfego de rede de uma porta para outra. Siga as etapas acima para adicionar, visualizar e remover regras de redirecionamento de porta no Windows.