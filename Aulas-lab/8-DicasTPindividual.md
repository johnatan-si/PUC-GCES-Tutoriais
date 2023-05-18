# Docker Front-end & Back-end

## Passo 1: Instalação do Docker

Acho que eu nem deveria falar mais disso, né ?  Precisamos ter o Docker instalado e rodando na máquina antes de tudo. 


## Passo 2: Criação do Dockerfile do Frontend
O Dockerfile é um arquivo de configuração usado para criar uma imagem Docker para a aplicação frontend. Vamos criar o Dockerfile na pasta do frontend. Siga as instruções abaixo:

1.  Crie um novo arquivo chamado `Dockerfile` na pasta do frontend.
    
2.  Abra o arquivo `Dockerfile` em um editor de texto e adicione o seguinte conteúdo:

````
# Usa uma imagem base do Node.js
FROM node:latest

# Define o diretório de trabalho dentro do contêiner
WORKDIR /app

# Copia o arquivo package.json para o diretório de trabalho
COPY package.json .

# Instala as dependências do projeto
RUN npm install

# Copia todo o conteúdo do diretório atual para o diretório de trabalho
COPY . .

# Expõe a porta 3000 para acesso externo
EXPOSE 3000

# Define o comando de inicialização do contêiner
CMD ["npm", "start"]

````

O Dockerfile acima usa uma imagem base do Node.js, instala as dependências do projeto, copia o código-fonte do frontend para o contêiner e define o comando de inicialização.


## Passo 3: Criação do Dockerfile do Backend

Agora vamos criar o Dockerfile para o backend em Python. Siga as instruções abaixo:

1.  Crie um novo arquivo chamado `Dockerfile` na pasta do backend.
    
2.  Abra o arquivo `Dockerfile` em um editor de texto e adicione o seguinte conteúdo:

````
# Usa uma imagem base do Python
FROM python:latest

# Define o diretório de trabalho dentro do contêiner
WORKDIR /app

# Copia o arquivo requirements.txt para o diretório de trabalho
COPY requirements.txt .

# Instala as dependências do projeto
RUN pip install --no-cache-dir -r requirements.txt

# Copia todo o conteúdo do diretório atual para o diretório de trabalho
COPY . .

# Expõe a porta 8000 para acesso externo
EXPOSE 8000

# Define o comando de inicialização do contêiner
CMD ["python", "app.py"]
````

O Dockerfile acima usa uma imagem base do Python, instala as dependências do projeto, copia o código-fonte do backend para o contêiner e define o comando de inicialização.


## Passo 4: Configuração do Docker Compose

O Docker Compose é uma ferramenta que nos permite definir e executar várias imagens Docker como um conjunto de serviços. Vamos criar um arquivo `docker-compose.yml` para definir os serviços para nossa aplicação e os bancos de dados. Siga as instruções abaixo:

1.  Crie um novo arquivo chamado `docker-compose.yml` na pasta raiz do projeto.
    
2.  Abra o arquivo `docker-compose.yml` em um editor de texto e adicione o seguinte conteúdo:
````
version: '3'
services:
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - '3000:3000'
    depends_on:
      - backend
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - '8000:8000'
    depends_on:
      - mongodb
      - postgres
  mongodb:
    image: mongo
    ports:
      - '27017:27017'
  postgres:
    image: postgres
    ports:
      - '5432:5432'
    environment:
      - POSTGRES_USER=myuser
      - POSTGRES_PASSWORD=mypassword
      - POSTGRES_DB=mydatabase
````

O arquivo `docker-compose.yml` acima define três serviços: frontend, backend, e os bancos de dados MongoDB e PostgreSQL. O frontend e o backend são criados a partir dos respectivos Dockerfiles, enquanto o MongoDB e o PostgreSQL são usados diretamente a partir das imagens oficiais. Também definimos as portas a serem expostas e as dependências entre os serviços.

* *Pode ser necessário adaptar o docker-compose.yml para o seu tipo de banco de dados.*


## Passo 5: Execução dos Contêineres

Agora que já criamos os arquivos necessários, vamos executar os contêineres da nossa aplicação usando o Docker Compose. Siga as instruções abaixo:

1.Abra o terminal e navegue até a pasta raiz do projeto onde o arquivo `docker-compose.yml` está localizado.
    
2.  Execute o seguinte comando para iniciar os contêineres:
````
docker-compose up
````


O Docker Compose irá construir as imagens necessárias, criar e iniciar os contêineres para cada serviço definido no arquivo `docker-compose.yml`. Você verá os logs dos contêineres sendo exibidos no terminal.

3.  Abra um navegador da web e acesse `http://localhost:3000` para ver o frontend da aplicação. O backend estará disponível em `http://localhost:8000`.
4. Lembre-se de usar o comando `docker-compose down` para parar e remover os contêineres quando não estiver mais utilizando-os.


Essa aula abrange os conceitos básicos para usar o Docker na contêinerização de uma aplicação com diferentes serviços e bancos de dados para o trabalho individual. Há muitas outras funcionalidades e opções disponíveis no Docker e Docker Compose.
