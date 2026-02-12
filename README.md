# Config Service

Spring Cloud Config Server para gerenciamento centralizado de configurações.

## Tecnologias

- Java 17
- Spring Boot 3.4.2
- Spring Cloud 2024.0.0
- Spring Cloud Config Server
- Spring Boot Actuator
- Maven
- Docker

## Dependências Principais

- **spring-cloud-config-server**: Servidor de configuração centralizada
- **spring-boot-starter-actuator**: Monitoramento e métricas da aplicação

## Configuração

O serviço está configurado para rodar na porta **8888** por padrão.

### Repositório de Configuração

O Config Server está configurado para usar o **profile native**, carregando os arquivos de configuração localmente de `classpath:/config/`.

#### Arquivos de Configuração Disponíveis

Os seguintes arquivos de configuração estão disponíveis em `src/main/resources/config/`:

- `api-gateway.yml` - Configurações do API Gateway
- `application.yml` - Configurações compartilhadas
- `check-health-service.yml` - Configurações do serviço de health check
- `config-service.yml` - Configurações deste próprio serviço
- `discovery-service.yml` - Configurações do Eureka Discovery Service

### Integração com Eureka

O serviço está configurado para se registrar no Eureka Discovery Service:

```yaml
eureka:
  client:
    service-url:
      defaultZone: http://discovery-service:8761/eureka/
    register-with-eureka: true
    fetch-registry: true
```

## Como Executar

### Com Maven

```bash
mvn spring-boot:run
```

### Com JAR

```bash
mvn clean package
java -jar target/config-service-0.0.1-SNAPSHOT.jar
```

### Com Docker

```bash
docker build -t config-service .
docker run -p 8888:8888 config-service
```

## Endpoints

- Config Server: `http://localhost:8888/{application}/{profile}[/{label}]`
- Health: `http://localhost:8888/actuator/health`
- Info: `http://localhost:8888/actuator/info`
- Metrics: `http://localhost:8888/actuator/metrics`

## Exemplo de Uso

Para acessar configurações de uma aplicação específica:

```
# Configurações do API Gateway
http://localhost:8888/api-gateway/default

# Configurações do Discovery Service
http://localhost:8888/discovery-service/default

# Configurações do Check Health Service
http://localhost:8888/check-health-service/default
```

## Estrutura do Projeto

```
config-service/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/fiap/tcc/configservice/
│   │   │       └── ConfigServiceApplication.java
│   │   └── resources/
│   │       ├── application.yml
│   │       ├── bootstrap.yml
│   │       └── config/
│   │           ├── api-gateway.yml
│   │           ├── application.yml
│   │           ├── check-health-service.yml
│   │           ├── config-service.yml
│   │           └── discovery-service.yml
│   └── test/
├── Dockerfile
└── pom.xml
```
