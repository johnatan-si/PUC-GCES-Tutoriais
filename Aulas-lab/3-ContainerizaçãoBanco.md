
# Containerização de Banco de Dados com Docker

Cocê aprenderá como **containerizar** um banco de dados usando o Docker. Usaremos o exemplo de um banco de dados **MongoDB** e o JavaScript como linguagem de programação.

## Pré-requisitos

Antes de começar, certifique-se de ter o seguinte instalado em seu sistema (já cansei de falar isso):

-   Docker: Verifique se o Docker está instalado corretamente e pode ser executado no seu sistema.

## Passo 1: Criando um diretório para o projeto

1. Crie um diretório para o projeto em um local de sua preferência.
    
2.  Abra um terminal ou prompt de comando e navegue até o diretório recém-criado.
3. 
## Passo 2: Criando o arquivo Dockerfile

1. No diretório do projeto, crie um arquivo chamado `Dockerfile`.
    
2.  Abra o arquivo `Dockerfile` em um editor de texto.
    
3.  Adicione o seguinte conteúdo ao arquivo `Dockerfile`:
````
# Define a imagem base
FROM mongo

# Copia o arquivo JavaScript para o diretório correto no contêiner
COPY script.js /docker-entrypoint-initdb.d/

# Define o comando a ser executado quando o contêiner for iniciado
CMD ["mongod"]
````

Neste exemplo, estamos usando a imagem base oficial do MongoDB disponível no Docker Hub. O arquivo JavaScript `script.js` será copiado para o diretório `/docker-entrypoint-initdb.d/` no contêiner MongoDB. O comando `mongod` é definido como o comando a ser executado quando o contêiner for iniciado.

## Passo 3: Criando o arquivo script.js

1.  No diretório do projeto, crie um arquivo chamado `script.js`.
    
2.  Abra o arquivo `script.js` em um editor de texto.
    
3.  Adicione o seguinte conteúdo ao arquivo `script.js`:
````
// Exemplo de código JavaScript para inicializar o banco de dados

use mydb;

db.createCollection("users");
db.users.insertOne({ name: "John Doe", email: "john@example.com" });
db.users.insertOne({ name: "Jane Smith", email: "jane@example.com" });

print("Dados inseridos com sucesso!");

````
Este é apenas um exemplo simples de código JavaScript para inicializar o banco de dados MongoDB. Você pode personalizar esse código de acordo com suas necessidades. Primeiro criamos uma coleção chamada "users" usando `db.createCollection()`. Em seguida, inserimos os dados na coleção "users".

## Passo 4: Construindo a imagem do Docker

1.  No terminal ou prompt de comando, execute o seguinte comando para construir a imagem Docker:
````
docker build -t mymongodb .
````

Isso irá criar a imagem Docker com o nome `mymongodb` com base no Dockerfile e nos arquivos do projeto.

## Passo 5: Executando o contêiner

1.  Agora, execute o seguinte comando para iniciar o contêiner MongoDB com base na imagem que acabamos de criar:
````
docker run -d -p 27017:27017 --name mymongo mymongodb
````

Isso iniciará o contêiner MongoDB com o nome `mymongo` e mapeará a porta `27017` do host para a porta `27017` do contêiner. Às vezes acontece de ter conflito com portas, pois outra aplicação poderá estar usando essa porta. Caso isso ocorra, pesquise sobre conflitos de portas. 

## Passo 6: Verificando o funcionamento do banco de dados
1.  Abra um navegador da web ou uma ferramenta de geração de banco de dados, como o MongoDB Compass.
2. Conecte-se ao banco de dados MongoDB usando as seguintes informações de conexão:
-   Host: `localhost`
-   Porta: `27017`
-
3.  Verifique se o banco de dados está funcionando corretamente e se os dados foram inseridos corretamente com base no código JavaScript no arquivo `script.js`.

Você **containerizou** com sucesso um banco de dados usando o **Docker**. Agora você pode distribuir e executar o banco de dados em qualquer ambiente compatível com o Docker, sem precisar configurar manualmente o ambiente de banco de dados. Você pode expandir esse exemplo personalizando o arquivo `script.js` para incluir mais operações de banco de dados, como consultas, atualizações ou exclusões. Além disso, você pode explorar outros bancos de dados e adaptar essa aula para o trabalho prático individual e em grupo.  Lembre-se de parar o contêiner quando não estiver mais usando-o usando o comando `docker stop mymongo` (onde `mymongo` é o nome do contêiner).
