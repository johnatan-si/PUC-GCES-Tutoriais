# Criando Docker Container and Image com Múltiplos Arquivos de Código


## Introdução

Na aula de hoje vamos aprender  a executar várioas arquivos. Esse documento é dividindo em código [Python](#2criando-os-arquivos-de-código-py) e [JavaScript](#1-javascript). Escolha o que for mais conveniente para você. 
## 1. Configuração do ambiente


Antes de começarmos, certifique-se de ter o Docker instalado em seu sistema. Se você não tem instalado, então você está bem atrasado nas aulas, porque já fizemos isso antes.   Para saber a versão do seu Docker, rode o comando no terminal: 

    docker --version
Isso deve exibir a versão do Docker instalada em seu sistema. Execute o Docker via interface (sabe que para isso basta clicar no ícone, né?). 

## 2.Criando os arquivos de código-Py

Crie os arquivos de código em Python que desejamos executar no Docker Container.  Vamos criar dois arquivos: `script1.py` e `script2.py`. Tá ligado que você vai criar esses scripts no VSCode e em pasta apropriada, né? 

Dentro de cada arquivo, adicione o seguinte código:

**script1.py**

    def greet(name):
        print(f"Hello, {name} from script1!")
    
    greet("Alice")
**script2.py**

    def calculateSum(a, b):
        return a + b
    
    result = calculateSum(3, 4)
    print(f"A soma e: {result}")
Salve os arquivos no mesmo diretório (pelo amor de DEUS).

## 3. Criando o Dockerfile

Agora, vamos criar um Dockerfile para definir a configuração do nosso Docker Container. O Dockerfile é um arquivo de texto **sem extensão** que contém uma série de instruções para construir uma **Docker Image.**

Na pasta que você tem o seu código-fonte, crie um arquivo chamado `Dockerfile` e adicione o seguinte conteúdo:

    # Imagem base para o Python
    FROM python:3.9
    
    # Criando diretório de trabalho
    WORKDIR /app
    
    # Copiando os arquivos de código para o diretório de trabalho
    COPY script1.py .
    COPY script2.py .
    
    # Executando o primeiro arquivo de código
    CMD ["python", "script1.py"]
    
Neste exemplo, utilizamos a imagem base do Python e definimos o diretório de trabalho como `/app`. Em seguida, copiamos os arquivos de código `script1.py` e `script2.py` para o diretório de trabalho. Por fim, configuramos o Docker Container para executar o `script1.py` como o ponto de entrada padrão.

## 4. Construindo a Docker Image

Agora que temos o Dockerfile pronto, podemos usar o Docker para construir uma Docker Image que contém os arquivos de código Python. No terminal, navegue até o diretório onde você criou os arquivos de código e o Dockerfile. No comando docker build -t meu-container-python ., a opção -t é usada para especificar uma "tag" ou um nome para a imagem Docker que está sendo construída. A tag é uma maneira de nomear e identificar sua imagem de forma mais amigável e legível.

No exemplo, a tag "meu-container-python" está sendo atribuída à imagem que está sendo construída. Isso significa que, após a construção da imagem, você poderá fazer referência a ela pelo nome "meu-container-python" em vez de usar o ID da imagem, que é mais difícil de lembrar. Execute o seguinte comando para construir a Docker Image:

    docker build -t meu-container-python .
Isso irá construir uma Docker Image com base no Dockerfile e atribuir o nome `meu-container-python` a ela. Certifique-se de incluir o ponto (.) no final do comando para indicar o diretório atual como contexto para a construção da imagem (pelo amor de Deus. O ponto é necessário).

Aguarde até que a construção seja concluída. Isso pode levar alguns minutos, dependendo da velocidade da sua conexão com a internet e das especificações do seu sistema. Já sabemos que esse passo vai demorar, não é mesmo?

## 5. Executando o Docker Container

Agora que temos a Docker Image, podemos executar um Docker Container a partir dela. No terminal, execute o seguinte comando:

    docker run meu-container-python
    
Isso iniciará um novo Docker Container com base na imagem que construímos e executará o arquivo `script1.py`.

Você verá a saída no terminal:

    Hello, Alice from script1!


Agora, para executar o segundo arquivo de código, podemos passar um comando adicional para o Docker Container no momento da execução. No terminal, execute o seguinte comando:

    docker run meu-container-python python script2.py
Isso executará o segundo arquivo de código `script2.py` dentro do Docker Container.

Você verá a saída no terminal:

    A soma e: 7
    
Lembre-se de que o Docker oferece uma maneira conveniente de isolar e executar aplicativos em um ambiente consistente.

## 6. Agora vamos aprender a executar todos os arquivos por extensão

Para executar todos os arquivos de código fonte dentro do Docker Container, você pode fazer algumas alterações no Dockerfile. Vamos ajustar o comando `CMD` para executar todos os arquivos `.py` encontrados no diretório de trabalho.

Aqui está a modificação no Dockerfile:
````
# Use a imagem base Python
FROM python:3.8

# Copie todos os arquivos Python do diretório local para o diretório de trabalho no contêiner
COPY *.py /app/

# Defina o diretório de trabalho como /app
WORKDIR /app

# Execute todos os scripts Python no diretório de trabalho
CMD ["bash", "-c", "for script in *.py; do python $script; done"]
````
Nesse exemplo, utilizamos o comando `COPY . .` para copiar todos os arquivos do diretório atual para o diretório de trabalho dentro do Docker Container. Além disso, substituímos o comando `python script1.py` pelo comando `python -m pytest`, que irá executar todos os arquivos `.py` no diretório de trabalho usando o pytest. Agora, quando você construir e executar o Docker Container, todos os arquivos de código Python presentes no diretório serão executados. Certifique-se de ter o pytest instalado no seu ambiente de desenvolvimento para que o comando `pytest` funcione corretamente dentro do Docker Container.

Para executar o Docker Container com a modificação, utilize o seguinte comando:

    docker run meu-container-python
Isso executará todos os arquivos `.py` presentes no diretório de trabalho dentro do Docker Container.

Tenha em mente que você precisa garantir que todos os arquivos de código sejam adequados para execução contínua, pois eles serão executados em sequência. Certifique-se de que não há conflitos ou dependências que possam causar problemas na execução de vários arquivos simultaneamente (PELO AMOR DE DEUS, ISSO É IMPORTANTE).

## 1. JavaScript

Vamos começar criando os arquivos de código em Javascript que desejamos executar no Docker Container. Crie os arquivos de código Javascript que você deseja incluir no Docker Container. Por exemplo, vamos criar dois arquivos: `script1.js` e `script2.js`. Esses arquivos serão criados usando o VSCODE. Lembre de criar uma pasta para isso. Abra o seu editor de código e crie os arquivos `script1.js` e `script2.js`. Dentro de cada arquivo, adicione o seguinte código:

**script1.js**

    let a = 3;
    let b = 4;
    console.log(`A subtracao e: ${a - b}`);

**script2.js**

    let a = 3;
    let b = 4;
    console.log(`A soma e: ${a + b}`);
Salve os arquivos no mesmo diretório ( pelo amor de Deus, não salve em locais diferentes).

## 3. Criando o Dockerfile

Agora, vamos criar um Dockerfile para definir a configuração do nosso Docker Container. O Dockerfile é um arquivo de texto sem extensão que contém uma série de instruções para construir uma Docker Image.
Crie um arquivo chamado `Dockerfile` e adicione o seguinte conteúdo:

    # Imagem base para o Node.js
    FROM node:14-alpine
    
    # Criando diretório de trabalho
    WORKDIR /app
    
    # Copiando os arquivos de código para o diretório de trabalho
    COPY . .
    
    # Executando o primeiro arquivo de código
    CMD ["node", "script1.js"]

Neste exemplo, utilizamos a imagem base do Node.js e definimos o diretório de trabalho como `/app`. Em seguida, copiamos todos os arquivos do diretório atual para o diretório de trabalho dentro do Docker Container. Por fim, configuramos o Docker Container para executar o `script1.js` como o ponto de entrada padrão.

## 4. Construindo a Docker Image

Agora que temos o Dockerfile pronto, podemos usar o Docker para construir uma Docker Image que contém os arquivos de código Javascript. No terminal, navegue até o diretório onde você criou os arquivos de código e o Dockerfile. Execute o seguinte comando para construir a Docker Image (presta atenção no ponto final):

    docker build -t meu-container-javascript .

Isso irá construir uma Docker Image com base no Dockerfile e atribuir o nome `meu-container-javascript` a ela. Certifique-se de incluir o ponto (.) no final do comando.

## 5. Execução de todos os arquivos .JS

Modificação no Dockerfile:

    # Imagem base para o Node.js
    FROM node:14-alpine
    
    # Criando diretório de trabalho
    WORKDIR /app
    
    # Copiando os arquivos de código para o diretório de trabalho
    COPY . .
    
    # Executando todos os arquivos .js no diretório de trabalho
    CMD ["sh", "-c", "for file in *.js; do node \"$file\"; done"]

Nesse exemplo, utilizamos o comando `COPY . .` para copiar todos os arquivos do diretório atual para o diretório de trabalho dentro do Docker Container.  Além disso, ajustamos o comando `CMD` para executar todos os arquivos `.js` presentes no diretório de trabalho usando um loop em shell. Dessa forma, todos os arquivos `.js` serão executados sequencialmente dentro do Docker Container. Agora, quando você construir e executar o Docker Container, todos os arquivos de código JavaScript presentes no diretório serão executados. Certifique-se de que seus arquivos de código JavaScript não possuam conflitos ou dependências que possam causar problemas na execução de vários arquivos simultaneamente.

Para executar o Docker Container com a modificação, utilize o seguinte comando:

    docker run meu-container-javascript


Isso executará todos os arquivos `.js` presentes no diretório de trabalho dentro do Docker Container.
