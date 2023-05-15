

# Hoje vamos aprender a criar um Docker Compose com Múltiplos Arquivos JavaScript

Se liga aí, aprenderemos como criar um **Docker Compose** para executar múltiplos arquivos **Javascript** em contêineres isolados*. Usaremos o Docker Compose para orquestrar a execução de vários serviços e garantir que eles possam se comunicar entre si. 

## 1. Configuração do Ambiente

Certifique-se de ter o Docker e o Docker Compose instalados em seu sistema. Você pode baixá-los e instalá-los a partir do site oficial do Docker: [https://www.docker.com/get-started](https://www.docker.com/get-started)
Após a instalação, verifique se o Docker e o Docker Compose estão funcionando corretamente executando os seguintes comandos no terminal:

    docker --version
    docker-compose --version
Isso deve exibir as versões do Docker e do Docker Compose instaladas em seu sistema.

## 2. Criando os arquivos de código

Vamos começar criando os arquivos de código JavaScript que desejamos executar em nossos contêineres.

Crie os arquivos de código JavaScript que você deseja incluir no Docker Compose. Por exemplo, criaremos dois arquivos: `script1.js` e `script2.js`.

Abra o seu editor de código e crie os arquivos `script1.js` e `script2.js`. Dentro de cada arquivo, adicione o seguinte código:

**script1.js**

    console.log("Codigo script1.js em execucao!");
    
**script2.js**
    let a = 3;
    let b = 4;
    console.log(`A SOMA E: ${a + b}`);
Ei, presta atenção, você deve salvar os dois arquivos no mesmo diretório. 

## 3. Criando o arquivo Dockerfile para cada serviço

Agora, vamos criar um arquivo Dockerfile para cada serviço que desejamos executar no Docker Compose. Cada arquivo Dockerfile será responsável por definir a configuração de um serviço específico.

Crie um arquivo chamado `Dockerfile.service1` e adicione o seguinte conteúdo:

    # Imagem base para o Node.js
    FROM node:14-alpine
    
    # Definindo o diretório de trabalho
    WORKDIR /app
    
    # Copiando os arquivos de código para o diretório de trabalho
    COPY script1.js .
    
    # Executando o primeiro arquivo de código
    CMD ["node", "script1.js"]


Em seguida, crie um arquivo chamado `Dockerfile.service2` e adicione o seguinte conteúdo:

    # Imagem base para o Node.js
    FROM node:14-alpine
    
    # Definindo o diretório de trabalho
    WORKDIR /app
    
    # Copiando os arquivos de código para o diretório de trabalho
    COPY script2.js .
    
    # Executando o segundo arquivo de código
    CMD ["node", "script2.js"]


Nesses exemplos, utilizamos a imagem base do Node.js para cada serviço e definimos o diretório de trabalho como `/app`. Em seguida, copiamos o arquivo de código correspondente para o diretório de trabalho e, por fim, executamos o arquivo de código usando o comando `CMD`.

## 4. Criando o arquivo docker-compose.yml

Agora, vamos criar o arquivo `docker-compose.yml`, que será responsável por definir e gerenciar os serviços do Docker Compose. Crie um arquivo chamado `docker-compose.yml` e adicione o seguinte conteúdo:

    version: '3'
    services:
      service1:
        build:
          context: .
          dockerfile: Dockerfile.service1
        volumes:
          - ./script1.js:/app/script1.js
        command: node script1.js
      service2:
        build:
          context: .
          dockerfile: Dockerfile.service2
        volumes:
          - ./script2.js:/app/script2.js
        command: node script2.js
**LEIA COM ATENÇÃO PARA QUE VOCÊ ENTENDA O QUE O CÓDIGO ESTÁ FAZENDO..**
Neste arquivo, definimos dois serviços: `service1` e `service2`. Para cada serviço, especificamos a construção da imagem a partir do respectivo arquivo Dockerfile. Também mapeamos o volume do arquivo de código correspondente, para que as alterações no arquivo sejam refletidas no contêiner. Por fim, especificamos o comando para executar o arquivo de código.

## 5. Executando o Docker Compose
Agora que temos todos os arquivos configurados, podemos executar o Docker Compose. No terminal, navegue até o diretório onde estão os arquivos `docker-compose.yml`, `Dockerfile.service1` e `Dockerfile.service2`.

Execute o seguinte comando para iniciar os serviços definidos no arquivo `docker-compose.yml`:

    docker-compose up
O Docker Compose começará a construir as imagens e iniciar os contêineres para cada serviço. Você verá a saída dos arquivos de código Javascript sendo exibida no terminal.

Para parar a execução do Docker Compose, pressione `Ctrl + C` no terminal.

UFAAA, terminamos. Agora você criou um Docker Compose com múltiplos arquivos JavaScript. Você pode adicionar mais serviços ao arquivo `docker-compose.yml` e estendê-lo para atender às suas necessidades específicas. O Docker Compose é uma ferramenta para orquestrar e gerenciar aplicativos em contêineres, facilitando o desenvolvimento e o ambiente de execução.

-----------------------------------------------------
## 1. Ei prof, mas como faço se tenho vários arquivos .js ? 

Agora vamos resolver esse problema. 

## 2 Docker Compose com vários arquivos JavaScript (*.js)

Vamos aprender como criar um Docker Compose para executar vários arquivos JavaScript simultaneamente. Usaremos um exemplo simples de uma aplicação Node.js que possui múltiplos arquivos JavaScript.

### Passo 1: Estrutura do projeto

1.  Crie uma nova pasta para o projeto.
2.  Coloque todos os arquivos JavaScript (*.js) que deseja executar no diretório `app` dentro da pasta do projeto.
3.  Certifique-se de que a estrutura do projeto seja semelhante a esta:

    projeto/
      ├── app/
      │   ├── script1.js
      │   ├── script2.js
      │   ├── script3.js
      │   └── ...
      └── docker-compose.yml


Por favor, presta atenção, certifique-se de que todos os arquivos JavaScript que deseja executar estejam presentes no diretório `app`.

### Passo 2: Escrevendo o arquivo docker-compose.yml

Agora, vamos criar o arquivo `docker-compose.yml` para configurar o Docker Compose.

1.  Crie um arquivo chamado `docker-compose.yml` na pasta do projeto.
2.  Abra o arquivo `docker-compose.yml` em um editor de texto.

Adicione o seguinte conteúdo ao arquivo `docker-compose.yml`:

    version: '3'
    services:
      app:
        build:
          context: .
          dockerfile: Dockerfile
        volumes:
          - ./app:/app
        command: node /app/*.js

Neste arquivo, definimos um serviço chamado `app`. Configuramos a construção da imagem usando o arquivo `Dockerfile`. Mapeamos o diretório `app` para o diretório `/app` dentro do contêiner usando volumes. E, por fim, definimos o comando para executar todos os arquivos JavaScript (*.js) presentes no diretório `/app` do contêiner.

### Passo 3: Escrevendo o Dockerfile

Agora, vamos criar o arquivo `Dockerfile` para construir a imagem Docker.

1.  Crie um arquivo chamado `Dockerfile` na pasta do projeto.
2.  Abra o arquivo `Dockerfile` em um editor de texto.

Adicione o seguinte conteúdo ao arquivo `Dockerfile`:

    FROM node:14-alpine
    
    WORKDIR /app
    
    COPY package.json .
    RUN npm install
    
    COPY . .
    
    CMD ["node", "/app/*.js"]


Neste arquivo, usamos a imagem base do Node.js, definimos o diretório de trabalho como `/app`, copiamos o arquivo `package.json` e executamos o comando `npm install` para instalar as dependências (você prestou atenção no seu diretório de trabalho? Ele se chama app, né?). Em seguida, copiamos todos os arquivos do projeto para o diretório de trabalho do contêiner. Por fim, usamos o comando `node /app/*.js` para executar todos os arquivos JavaScript (*.js) presentes no diretório `/app` do contêiner.

### Passo 4: Executando o Docker Compose

Agora que tudo está configurado, podemos executar o Docker Compose e iniciar a execução dos arquivos JavaScript.

1.  Abra um terminal ou prompt de comando na pasta do projeto.

2. Certifique-se de que o Docker e o Docker Compose estejam instalados e em execução.
    
3.  Execute o seguinte comando no terminal para iniciar o Docker Compose:

    docker-compose up
Isso iniciará a construção da imagem e a criação do contêiner com base nas configurações definidas no arquivo `docker-compose.yml`.
4.  O Docker Compose executará todos os arquivos JavaScript (*.js) presentes no diretório `app` e exibirá a saída no terminal.


### Observações importantes:

-   Certifique-se de que todos os arquivos JavaScript que deseja executar estejam presentes no diretório `app` antes de iniciar o Docker Compose.
    
-   Se você adicionar ou remover arquivos JavaScript após iniciar o Docker Compose, será necessário parar e reiniciar o contêiner para que as alterações sejam refletidas.
    
-   Certifique-se de que todas as dependências necessárias estejam listadas corretamente no arquivo `package.json` do projeto.
    
-   Caso necessário, você pode ajustar outras configurações no arquivo `docker-compose.yml` ou `Dockerfile` conforme as necessidades do seu projeto.
    

Agora você tem um Docker Compose configurado para executar vários arquivos JavaScript de uma só vez. Isso facilitará a execução e o gerenciamento de projetos que possuem vários arquivos JavaScript.

*Lembre-se de adaptar esse exemplo ao seu projeto, adicionando outras configurações ou serviços conforme necessário.*
