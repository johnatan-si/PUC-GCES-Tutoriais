# Introdução ao Docker Compose para um site JavaScript com Express

Você aprenderá como usar o Docker e o Docker **Compose** para criar um ambiente de desenvolvimento para um site em JavaScript usando o framework Express. Vamos criar um contêiner Docker para executar o servidor Express e usar o Docker Compose para orquestrar a configuração do nosso ambiente.

## Passo 1: Configurando o projeto

1.  Crie uma pasta para o seu projeto e navegue até ela no terminal.
2.  Execute o seguinte comando para inicializar um novo projeto Node.js:
````
npm init -y
````

3.  Isso criará um arquivo `package.json` com as configurações padrão.
## Passo 2: Instalando as dependências

Vamos instalar o framework Express como dependência do projeto. No terminal, execute o seguinte comando:

````
npm install express
````

## 2.1 Diretório 
Agora queremos rodar todos os scripts que estão no em um determinado diretório. Crie um diretório chamado public. 
Dentro de public adicione: 

index.html 
````
<!DOCTYPE  html>

<html>

<head>

<title>Meu Site</title>

<script  src="arquivo1.js"></script>

<script  src="arquivo2.js"></script>

<script  src="index.js"></script>

</head>

<body>

<h1>Exemplo de Integração com JavaScript</h1>

<div  id="resultado1"></div>

<div  id="resultado2"></div>

</body>

</html>
````


index.js
````
// Chama as funções diretamente, sem usar require

document.addEventListener('DOMContentLoaded', function() {

funcao1();

funcao2();

});
````

arquivo1.js
````
function  funcao1() {
document.getElementById('resultado1').textContent  =  'Função 1 chamada!';
}
````

arquivo2.js

````
function  funcao2() {
document.getElementById('resultado2').textContent  =  'Função 2 chamada!';
}
````





## Passo 3: Configurando o servidor Express

1.  Crie um arquivo chamado `server.js` na raiz do seu projeto.
2.  Abra o arquivo `server.js` em um editor de texto e adicione o seguinte código para configurar um servidor Express básico:
````
const express = require('express');
const app = express();
const path = require('path');

// Define a rota para servir o arquivo index.html
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

// Configura o servidor para servir arquivos estáticos
app.use(express.static('public'));

// Inicia o servidor
app.listen(3000, () => {
  console.log('Servidor está rodando na porta 3000');
});
````

## Passo 4: Criando o arquivo Dockerfile

1.  Na raiz do seu projeto, crie um arquivo chamado `Dockerfile`.
2.  Abra o arquivo `Dockerfile` em um editor de texto e adicione o seguinte código para definir as instruções de construção da imagem Docker:
````
# Imagem base

FROM  node:14
# Diretório de trabalho dentro do contêiner

WORKDIR  /usr/src/app

# Copia os arquivos de configuração e dependências do projeto

COPY  package*.json  ./

RUN  npm  install

  
# Copia o restante do código do projeto

COPY  .  .

  

# Copia os arquivos JavaScript para o diretório public

COPY  public  public

  

# Porta em que o servidor Express estará escutando

EXPOSE  3000

  

# Comando para iniciar o servidor

CMD  [  "node",  "server.js"  ]
````



## Passo 5: Criando o arquivo docker-compose.yml

1.  Na raiz do seu projeto, crie um arquivo chamado `docker-compose.yml`.
2.  Abra o arquivo `docker-compose.yml` em um editor de texto e adicione o seguinte código para definir a configuração do Docker Compose:
````
version: '3'
services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - '3000:3000'
````

## Passo 6: Executando o contêiner Docker

1.  Abra o terminal na pasta raiz do seu projeto.
2.  Execute o seguinte comando para construir a imagem Docker e iniciar o contêiner: docker-compose up

Isso irá criar a imagem Docker com base no `Dockerfile` e iniciar o contêiner com o servidor Express em execução.


## Passo 7: Testando o servidor Express

1.  Abra um navegador da web e acesse `http://localhost:3000`.
2.  Você deverá ver a mensagem "Olá, mundo!" exibida no navegador, indicando que o servidor Express está funcionando corretamente.
3. Deverá aparecer a mensagem que os script js também estão executando. 
