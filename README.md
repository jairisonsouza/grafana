# Grafana com Autenticação via LDAP

Este repositório contém os arquivos necessários para implantação do Grafana utilizando autenticação via LDAP, integrado ao Traefik para gerenciamento de tráfego HTTPS.

## Tecnologias Utilizadas
- **Docker Swarm** para orquestração de containers
- **Grafana** para monitoramento e visualização de dados
- **PostgreSQL** como banco de dados do Grafana
- **LDAP** para autenticação dos usuários
- **Traefik** como proxy reverso e gerenciador de certificados SSL

## Estrutura dos Arquivos

### `docker-compose.yml`
Define os serviços:
- **grafana-db**: Banco de dados PostgreSQL para armazenar as configurações do Grafana
- **grafana**: Servidor Grafana configurado para utilizar PostgreSQL e autenticação LDAP
- Integração com o Traefik para exposição segura via HTTPS

### `grafana.ini`
- Configuração do Grafana, incluindo autenticação via LDAP
- Referencia o arquivo `ldap.toml` para obter os detalhes da conexão LDAP

### `ldap.toml`
- Define as configurações de conexão com o servidor LDAP
- Configura mapeamentos de grupos do AD para funções do Grafana

## Como Utilizar

### 1. Configurar Variáveis de Ambiente
Crie um arquivo `.env` no mesmo diretório do `docker-compose.yml` com as seguintes variáveis:
```
POSTGRES_DB_USER=seu_usuario
POSTGRES_PASSWORD=sua_senha
POSTGRES_DATABASE=grafana
```

### 2. Subir os Containers
Execute o seguinte comando:
```
docker stack deploy -c docker-compose.yml grafana
```
Isso iniciará os serviços no Docker Swarm.

### 3. Acessar o Grafana
Abra o navegador e acesse:
```
https://grafana.seudominio.com
```
Entre com suas credenciais do AD para autenticação.

## Personalização
- Modifique `ldap.toml` para ajustar grupos e permissões conforme sua estrutura de AD.
- Edite `grafana.ini` para alterar as configurações padrões do Grafana.

## Licença
Este projeto é distribuído sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.
