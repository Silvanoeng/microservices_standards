## Distributed Tracing

É o uso de ID de transação global e do ID de transação da solicitação, nas requisições HTTP eles são enviados através dos cabeçalhos. Sua função é permitir a rastrabilidade de uma mesma solicitação na aplicação, pelos diferentes processos dos microsserviçõs.  
Para seguir esse padrão é necessario garantir que todas as solicitações e mensagens relacionadas sejam marcadas com um ID de correlação comum e que o ID faça parte de todos os eventos de log. Pois em um eventual problema, podemos usar o serviço de log centralizado para encontrar todos os eventos de log relacionados.
