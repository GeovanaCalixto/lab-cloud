Revisão de portas
Objetivo: estudar portas de rede e registrar um exemplo prático

O que é uma porta?
Uma porta é um número usado na comunicação de rede para identificar um serviço ou aplicação.
Por exemplo, HTTPS costuma usar a porta 443.

Testei HTTP na porta 80 com curl e recebi a resposta HTTP/1.1 200 OK

Comando utilizado
Usei o curl no WSL para fazer solicitações ao domínio example.com. 
A opção -I, com I maiúsculo, pede os cabeçalhos da resposta usando o método HTTP HEAD, sem baixar o corpo da página.

Nas URLs, :443 e :80 indicam as portas de destino. 
Essas são as portas padrão de HTTPS e HTTP, respectivamente, embora os serviços possam usar outras.

Teste 1: HTTPS na porta 443
Executei curl -I https://example.com:443. 
Recebi HTTP/2 200, indicando que minha solicitação foi atendida com sucesso. 
O HTTPS usa TLS () para proteger a comunicação em trânsito.

Teste 2: HTTP na porta 80
Executei curl -I http://example.com:80. 
Recebi HTTP/1.1 200 OK, indicando que a solicitação também foi atendida. 
Nessa conexão HTTP, os dados não são criptografados por TLS.

O que observei nas respostas
* 200 OK: status de sucesso da solicitação.
* HTTP/2 e HTTP/1.1: versões do protocolo usadas nas respostas; não são exclusivas das portas 443 e 80.
* date: data e hora da resposta, em GMT.
* content-type: text/html: informa o tipo de conteúdo do recurso; charset=utf-8 indica sua codificação.
* server: cloudflare: serviço identificado na resposta, sem confirmar, por si só, qual é o servidor de origem.
* cf-cache-status: HIT: a Cloudflare informou que a resposta veio do cache.

Meu aprendizado
Comparei duas conexões ao mesmo domínio: uma via HTTP e outra via HTTPS. 
As duas responderam com sucesso, mas apenas a conexão HTTPS usou TLS. 
Guardei os prints de cada teste na pasta Imagens.

