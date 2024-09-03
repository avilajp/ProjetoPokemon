# Projeto Fullstack para Processo Seletivo 4Linux

## Descrição
Este projeto consiste em uma aplicação web full stack desenvolvida como parte do processo seletivo para a 4Linux. Ele inclui funcionalidades de login, registro de usuários, autenticação via JWT, consumo da PokeAPI para exibir uma lista de Pokémons e está completamente conteinerizado usando Docker.

## Requisitos
- Docker
- Docker Compose

## Como Rodar o Projeto

### Passo 1: Clonar o Repositório
Clone este repositório para o seu ambiente local.


git clone https://github.com/avilajp/ProjetoPokemon

### Passo 2: Construir e Iniciar os Containers
Use o Docker Compose para construir as imagens e iniciar os containers.

docker-compose up --build

### Passo 3: Acessar a Aplicação
O backend estará rodando em http://localhost:8000.
O frontend estará disponível em http://localhost:8080.

Estrutura do Projeto
backend/: Contém a lógica do servidor em Python com FastAPI.
frontend/: Contém o código do cliente em Vue.js.
venv/: Ambiente virtual Python.
docker-compose.yml: Arquivo para orquestração dos containers.
Dockerfile: Arquivo de construção do backend.
Dockerfile-frontend: Arquivo de construção do frontend.

### Endpoints da API
POST /api/register: Registra um novo usuário.
Exemplo de Request:
{
  "username": "usuario",
  "password": "senha"
}
Exemplo de Response:
{
  "message": "Usuário registrado com sucesso"
}
POST /token: Autentica um usuário e retorna um token JWT.
Exemplo de Request:
{
  "username": "usuario",
  "password": "senha"
}
Exemplo de Response:
{
  "access_token": "token_jwt",
  "token_type": "bearer"
}

### Frontend
A aplicação cliente possui as seguintes rotas:

/login: Página de login.
/register: Página de registro.
/: Página principal, exibindo uma lista de Pokémons (protegida por autenticação).

### Tecnologias Utilizadas
Backend: FastAPI, PostgreSQL
Frontend: Vue.js
Containerização: Docker, Docker Compose
Observações
Certifique-se de que as portas 5432, 8000, e 80 estejam livres antes de rodar os containers.
O frontend só estará acessível após o processo de build, que pode levar alguns minutos.