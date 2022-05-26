## Central configuration

Esse padrão tem como objetivo centralizar todas as configurações dos microsserviços, como variáveis de ambiente. Para isso é criado um componente onde todas as instâncias de microsserviços em execução podem consumir essas informações. Ele também facilita caso essas configurações tenham que ser alteradas, pois dessa forma tal alteração deve ser feita apenas em um lugar. 
Pode ser guardadas as configurações dos diferentes ambiente (desenvolvimento, testing, QA, produção, etc).


## Cliente config

Depois de pesquisar sobre o assunto, descobri que havia um tempo onde era necessario criar um arquivo bootstrap.yml, quando as configurações 
que desejamos importar tinham relação com o banco de dados que vamos conectar, esse arquivo seria processado antes do aplication.yml.
Porem isso já foi superado, por esse motivo vou descrever três maneiras de configuração, para poder ajudar pessoas quem possam encontrar 
configurações com o bootstrap.yml.


### Primeira forma (+ atual, kkk)

No pom.xml deve ser inserido essa dependencia.

```xml
<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```
No https://start.spring.io/ esta como Config Client.

E no application.yml colocar o seguinte conteúdo:

```yml
server:
  port: 8071
spring:
  application:
    name: cliente
  config:
    import: optional:configserver:http://localhost:8888
  cloud:
    config:
      profile: dev
```
Primeiro eu defino a porta da aplicação, no caso '8071', depois nomeio a aplicação como 'cliente', isso é usado para se 
registrar no Eureka e também define o nome do arquivo que vai ser buscado no config server.
Depois configuramos onde deve ser importado as configurações 'optional:configserver:http://localhost:8888', o 'optional' 
torna essa configuração opcional, caso não consiga realizar essa configuração a aplicação vai subir sem carregar essa informação. 
Por fim podemos definir o profile, no caso devinimos como 'dev', desta forma ele vai buscar um arquivo nomeado da seguinte 
forma 'cliente-dev.yml', se ele não encontrar esse profile, vai usar o default 'cliente.yml', o mesmo ocorre se não for 
definido essa propriedade.
Seguindo essa linha, se o Spring não achar um arquivo que corresponda ao name passado, vai 
buscar a configuração default, que no caso seria um arquico nomeado como 'application.yml'.


### Segunda forma (- atual, kkk)

No pom.xml deve ser inserido duas dependencias.
A primeira seria para definir que a aplicação deve iniciar pelo arquivo bootstrap.yml, 
inserindo essa dependencia se torna dispensavel criar o arquivo, caso seu server config 
esteja na server port padrão 8888.

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bootstrap</artifactId>
</dependency>
```

Porem se for necessario alterar a server port, deve ser criado o arquivo bootstrap.yml, 
com o seguinte conteúdo.

```yml
spring:
  application:
    name: 'cliente'
  profiles:
    active: defaulf
  cloud:
    config:
      uri: http://localhost:8889
```
Nesse caso a configuração esta vindo de um aquivo local "cliente.yml".

A segunda dependencia é do config client.

```xml
<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

### Terceira forma

Ainda existe a possibilidade de registrar o Server Config no Eureka e quando o cliente for buscar as confugurações ele consulta o Eureka e então com a respota se conecta ao Server Config.



[1] - https://docs.spring.io/spring-cloud-config/docs/current/reference/html/#config-first-bootstrap
