## Padrão Service Registry

Esse padrão cria um mapeamento(IP, porta) dos nossos serviços, de forma a facilitar a localização destes.
Atravez dele criamos um servidor centralizado, onde os serviços devem se registrar no momento de iniciar.
Nesse registro consta o endereço IP, a porta e o identificador do serviço.
Outro dado muito importante que o Service Registry possui é a disponibilidade dos serviços e para que 
isso seja possivel, apos se registra, os serviços deve enviar um sinal de forma constante, esse sinal
é chamado de heartbeat("batimento"), quando não recebe o heartbeart, automaticamente marca o serviço
como fora de serviço e pode enviar uma notificação ao administrador.
