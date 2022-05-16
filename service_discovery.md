## Padrão Service Discovery

Este padrão é complementar ao padrão Service Registry.
O Service Discovery é responsavel por monitorar os nossos serviços e atualizar o registro deles no nosso Service Registry.
Ele pode ocorrer de duas formas, pelo lado do cliente ou pelo lado do servidor.
Pelo lado do cliente, a aplicação se conecta ao Service Registry para consultar quais são os serviços disponíveis, com
essa informação(Ip:porta) a aplicação se conectar ao serviço.
Pelo lado do servidor, a aplicação se conecta a um servidor, este se conecta ao Service Registry para consultar quais são
os serviços disponíveis e faz o balanceamento de carga internamente, ocultando essa capacidade do cliente.
