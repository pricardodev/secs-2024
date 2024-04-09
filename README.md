# secs-2024
IV Semana da Engenharia de Computação - Material de apoio

# Preparação Ambiente
## Instale
- Docker e Docker-compose (Linux)
- Wsl2 (Windows)

## Download Framework
- cd secs-2024
- composer create-project laravel/laravel:^10.0 crud
- copie todos os arquivos referente ao framework laravel, recorte da pasta /crud e cole na raiz do diretório /secs-2024

## Configurando base de dados
- abra o arquivo .env e altere a constante DB_CONNECTION=sqlite
- depois dos migrations criados execute o comando: php artisan migrate
- escolha a opção "YES" e ele criará um banco sqlite no diretório database com suas tabelas

