# Config Service

Spring Cloud Config Server para gerenciamento centralizado de configurações.

## Tecnologias

- Java 17
- Spring Boot 3.2.2
- Spring Cloud Config Server
- Spring Boot Actuator
- Maven

## Dependências Principais

- **spring-cloud-config-server**: Servidor de configuração centralizada
- **spring-boot-starter-actuator**: Monitoramento e métricas da aplicação

## Configuração

O serviço está configurado para rodar na porta **8888** por padrão.

### Repositório de Configuração

Por padrão, o Config Server está configurado para usar um repositório Git local em:
```
file://${user.home}/config-repo
```

Para usar um repositório Git remoto, descomente e configure as propriedades no `application.yml`:
```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/your-org/config-repo
          default-label: main
          username: ${GIT_USERNAME}
          password: ${GIT_PASSWORD}
```

## Como Executar

```bash
mvn spring-boot:run
```

Ou compile e execute o JAR:
```bash
mvn clean package
java -jar target/config-service-0.0.1-SNAPSHOT.jar
```

## Endpoints

- Config Server: `http://localhost:8888/{application}/{profile}[/{label}]`
- Health: `http://localhost:8888/actuator/health`
- Metrics: `http://localhost:8888/actuator/metrics`

## Exemplo de Uso

Para acessar configurações de uma aplicação chamada "my-service" no profile "dev":
```
http://localhost:8888/my-service/dev
```
