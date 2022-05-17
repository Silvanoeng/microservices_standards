## Central configuration

Esse padrão tem como objetivo centralizar todas as configurações dos microsserviços, como variáveis de ambiente. Para isso é criado um componente onde todas as instâncias de microsserviços em execução podem consumir essas informações. Ele também facilita caso essas configurações tenham que ser alteradas, pois dessa forma tal alteração deve ser feita apenas em um lugar. 
Pode ser guardadas as configurações dos diferentes ambiente (desenvolvimento, testing, QA, produção, etc).
