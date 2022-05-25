## Central configuration

Esse padrão tem como objetivo centralizar todas as configurações dos microsserviços, como variáveis de ambiente. Para isso é criado um componente onde todas as instâncias de microsserviços em execução podem consumir essas informações. Ele também facilita caso essas configurações tenham que ser alteradas, pois dessa forma tal alteração deve ser feita apenas em um lugar. 
Pode ser guardadas as configurações dos diferentes ambiente (desenvolvimento, testing, QA, produção, etc).


## Cliente config
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


Outra abordagem seria colocando apenas a dependencia:

```xml
<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```
E no application.yml colocar a seguinte conteúdo:

```yml
server:
  port: 8071
spring:
  config:
    import: optional:configserver:http://localhost:8888
  application:
    name: 'cliente'
    profiles:
      active: defaulf

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
```
Onde as seguinte linhas
```yml
spring:
  config:
    import: optional:configserver:http://localhost:8888
```
São as responsaveis por definir onde o Spring deve buscar a configuração.

Ainda existe a possibilidade de registrar o Server Config no Eureka e quando o cliente for buscar as confugurações ele consulta o Eureka e então com a respota se conecta ao Server Config.
