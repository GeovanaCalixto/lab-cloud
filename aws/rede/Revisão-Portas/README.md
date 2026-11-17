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
O HTTPS usa TLS (TLS significa Transport Layer Security ou Segurança da Camada de Transporte. 
É um protocolo que protege os dados durante a comunicação: 
criptografa as informações, ajuda a detectar alterações e usa certificados para verificar a identidade do servidor.)

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

TCP e UDP
Aprendi que TCP e UDP são protocolos de transporte e usam números de porta para direcionar a comunicação

* TCP estabelece uma conexão e busca entregar os dados completos e em ordem, retransmitindo quando necessário.
* UDP envia datagramas sem estabelecer uma conexão e não garante entrega ou ordem. Pode ser útil quando a rapidez importa, como em algumas chamadas de voz.

Nos meus testes, HTTP/1.1 e HTTP/2 usaram TCP. 
O número da porta deve ser entendido junto com o protocolo: TCP 443 e UDP 443 são diferentes.

Portas e grupos de segurança na AWS
Um grupo de segurança controla o tráfego permitido para um recurso, como uma instância EC2. 
Suas regras indicam protocolo, porta e origem para entrada ou destino para saída.

Por exemplo, uma regra de entrada pode permitir TCP na porta 443 a partir de uma origem definida, para acessar uma aplicação HTTPS. 
Isso não garante, por si só, que o acesso funcione: a aplicação também precisa estar disponível e a rede configurada.

Grupos de segurança são stateful: as respostas ao tráfego permitido são aceitas automaticamente, sem uma regra separada para o retorno.
