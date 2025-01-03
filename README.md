# inicie-app-laravel-exam
Teste seletivo para Inicie

URL de acesso ao teste: http://ec2-3-16-13-189.us-east-2.compute.amazonaws.com/app

# Gerenciador de Tarefas

Este é um projeto de gerenciamento de tarefas desenvolvido com Laravel (backend) e Angular (frontend). 
Ele segue a arquitetura de API RESTful, usando o padrão de repositório (Repository Pattern) para a camada de acesso aos dados.


Os links da aplicação são:

Back-end: http://localhost:8080/api/

Front-end: http://localhost:4200/app/


## Pré-requisitos

Antes de começar, você precisará de alguns pré-requisitos:

- [Docker](https://www.docker.com/products/docker-desktop) (para criação de containers)
- [Docker Compose](https://docs.docker.com/compose/install/) (para orquestrar os containers)
- [Git](https://git-scm.com/downloads) (para trabalhar com o controle de versão)

Não vou dar explicações detalhadas sobre a instalação destes pre-requisitos, porque cada SO tem suas particularidades.

## Instalação

### 1. Clone o repositório

Primeiro, clone o repositório  e seus submódulos na sua máquina local em algum local aque ache apropriado:

```bash
git clone https://github.com/WilliamSantAna/inicie-exam.git
cd inicie-exam
sudo git config submodule.inicie-frontend-exam.url https://github.com/WilliamSantAna/inicie-frontend-exam.git
sudo git config submodule.inicie-backend-exam.url https://github.com/WilliamSantAna/inicie-backend-exam.git
```

### 2. Configuração do ambiente

Mude o nome do arquivo ```env``` para ```.env```

```bash
mv -i env .env
```

### 3. Construa os containeres

Agora, rode o seguinte comando para construir o ambiente:

```bash
docker compose up -d --build --remove-orphans --force-recreate
```

Se tiver erro de permissão, rode o comando com sudo:

```bash
sudo docker compose up -d --build --remove-orphans --force-recreate
```

Se der certo, o resultado final será algo do tipo:

```
✔ Network inicie_inicie-network   Created
✔ Container inicie-db             Started
✔ Container inicie-backend        Started
✔ Container inicie-frontend       Started
```

Rode os containeres:

```bash
docker compose up
``` 
OU com sudo 
```bash
sudo docker compose up
``` 

Entre no container back-end
```bash
docker exec -it inicie-backend bash
``` 
OU com sudo 
```bash
sudo docker exec -it inicie-backend bash
```

Rode dentro do container:

```bash
php artisan migrate:fresh
php artisan db:seed
php artisan config:cache
```

Pode sair com container com ```exit```

### 3. Teste a aplicação

Teste se a API Rest está funcionando. Acesse no navegador:
http://localhost:8080/api/check-api

O resultado deverá ser:

```{"status":"API working"}```

Teste se a aplicação Angular está funcionando. Acesse no navegador:
http://localhost:4200/app/check-app

O resultado deverá ser:

```{"status":"APP working"}```

Se quiser rodar os testes unitários da API:

Entre no container 

```bash
docker exec -it inicie-backend bash
``` 
OU com sudo 
```bash
sudo docker exec -it inicie-backend bash
```

Rode dentro do container:

```bash
php artisan test
```

### 4. Parar e destruir os containeres

Para parar os containers: 
Isso irá parar todos os containers que estão sendo executados pelo Docker Compose, mas os dados não serão removidos, e os volumes serão mantidos.

```bash
docker-compose down
```


Parar e destruir os containers e volumes: 
Este comando irá parar e remover todos os containers, redes e volumes associados ao projeto.

```bash
docker-compose down --volumes
```


