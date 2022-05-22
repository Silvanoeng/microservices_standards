## Circuit Breaker
Tem como função priorizar a resposta dos serviços mais críticos, para evitar que as aplicações fiquem aguardando um retorno. Para isso é feito um monitoramento das aplicações e caso seja verificado o erro, ele para de passar as requisições e retorna uma falha.
Esse processo apresenta três estados diferentes.

### Closed
A aplicação esta respondendo com sucesso. Os erros são monitorados, áte que atinja o valor que foi colocado como limite, quando esse for atingido o estado passa para Open.

### Open
A aplicação paro de responder, quando é enviada uma requisição o Circuit Breaker retorna a falha e para de requisitar a aplicação com problema. Apos um tempo passa para o estado Half Open.

### Half Open
Inicia um processo de teste, onde um número reduzido de requisições são enviadas para a aplicação, de forma a validar se o serviço esta ativo novamente. Se estas forem respondidas com sucesso o estado passa para Closed, mas casso não tenha sucesso passa para o estado Open.
