
# Lint

No contexto da integração contínua, o termo "Lint" refere-se a uma prática de análise estática de código. O Lint é um tipo de verificação automática realizada por ferramentas de análise de código que identificam e reportam potenciais problemas, violações de estilo, erros ou más práticas no código-fonte. O objetivo do Lint em integração contínua é detectar problemas no código-fonte o mais cedo possível durante o processo de desenvolvimento, antes que eles sejam integrados ao repositório principal e causem impacto negativo no desenvolvimento e na qualidade do software.  As ferramentas de Lint analisam o código-fonte em busca de problemas como formatação incorreta, uso de variáveis não utilizadas, falta de comentários, identação inconsistente, potenciais vulnerabilidades de segurança, uso inadequado de APIs, entre outros. Elas aplicam regras pré-definidas ou personalizadas para verificar o código em busca de conformidade com as melhores práticas de desenvolvimento.


# Essa aula ensina ESLint para JavaScript. No final da página tem para [Python](#pylint-para-python)

### Passo 1: Instalação do ESLint

O primeiro passo é instalar o ESLint globalmente no seu sistema. Abra o terminal e execute o seguinte comando:

````
npm install -g eslint
````


### Passo 2: Configuração do projeto

Agora, vamos configurar o ESLint para o seu projeto. Abra o terminal e navegue até o diretório raiz do seu projeto. Execute o seguinte comando para inicializar a configuração do ESLint:

````
eslint --init
````

Você será apresentado a uma série de perguntas para configurar o ESLint. Aqui estão algumas opções comuns:

-   How would you like to use ESLint? **To check syntax, find problems, and enforce code style**
-   What type of modules does your project use? **JavaScript modules (import/export)**
-   Which framework does your project use? **None of these**
-   Does your project use TypeScript? **No**
-   Where does your code run? **Node**
-   How would you like to define a style for your project? **Use a popular style guide**
-   Which style guide do you want to follow? **Airbnb**
-   What format do you want your config file to be in? **JSON**


Após responder às perguntas, o ESLint instalará as dependências necessárias e criará um arquivo de configuração `.eslintrc.json` no diretório raiz do seu projeto.

### Passo 3: Executando a análise de código

Agora que o ESLint está configurado, você pode executar a análise de código no seu projeto. No terminal, navegue até o diretório raiz do seu projeto e execute o seguinte comando:

````
eslint your-file.js
````

Substitua `your-file.js` pelo caminho do arquivo JavaScript que deseja analisar. O ESLint irá verificar o código e exibirá os problemas encontrados no terminal. Por exemplo:

````
your-file.js
  5:9  error  'x' is assigned a value but never used  no-unused-vars
````

### Passo 4: Corrigindo problemas

O ESLint também pode ajudar a corrigir automaticamente alguns problemas. Para corrigir os problemas automaticamente, execute o seguinte comando:

````
eslint --fix your-file.js
````

Isso corrigirá os problemas que o ESLint puder resolver automaticamente e exibirá os problemas restantes no terminal para correção manual.

### Passo 5: Personalização da configuração

O arquivo `.eslintrc.json` no diretório raiz do seu projeto contém a configuração do ESLint para o seu projeto. Você pode personalizar essa configuração de acordo com as necessidades do seu projeto. Consulte a documentação do ESLint para saber mais sobre as opções de configuração disponíveis.

````
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": "eslint:recommended",
  "parserOptions": {
    "ecmaVersion": 12
  },
  "rules": {
    // Aqui você pode adicionar ou modificar regras do ESLint
  }
}
````



## Pylint para Python

### Passo 1: Instalação do Pylint

O primeiro passo é instalar o Pylint no seu ambiente Python. Abra o terminal e execute o seguinte comando:

````
pip install pylint
````


### Passo 2: Configuração do projeto
Agora, vamos configurar o Pylint para o seu projeto. Abra o terminal e navegue até o diretório raiz do seu projeto. Execute o seguinte comando para gerar um arquivo de configuração do Pylint:

````
pylint --generate-rcfile > .pylintrc
````

Isso criará um arquivo `.pylintrc` no diretório raiz do seu projeto com as configurações padrão do Pylint.

### Passo 3: Executando a análise de código

Agora que o Pylint está configurado, você pode executar a análise de código no seu projeto. No terminal, navegue até o diretório raiz do seu projeto e execute o seguinte comando:

````
pylint your_file.py
````

Substitua `your_file.py` pelo caminho do arquivo Python que deseja analisar.

O Pylint analisará o código e exibirá os problemas encontrados no terminal. Por exemplo:

````
your_file.py:5:0: C0301: Line too long (83/80) (line-too-long)
````

### Passo 4: Corrigindo problemas

O Pylint também pode ajudar a corrigir automaticamente alguns problemas. Para corrigir os problemas automaticamente, execute o seguinte comando:

````
pylint --fix your_file.py
````

Isso corrigirá os problemas que o Pylint puder resolver automaticamente e exibirá os problemas restantes no terminal para correção manual.

### Passo 5: Personalização da configuração

O arquivo `.pylintrc` no diretório raiz do seu projeto contém a configuração do Pylint para o seu projeto. Você pode personalizar essa configuração de acordo com as necessidades do seu projeto. Consulte a documentação do Pylint para saber mais sobre as opções de configuração disponíveis.

````
[MASTER]
# Aqui você pode adicionar ou modificar regras do Pylint

[MESSAGES CONTROL]
# Aqui você pode personalizar a exibição e o controle de mensagens

[FORMAT]
# Aqui você pode definir a formatação das mensagens do Pylint
````


# Lint com Docker  JS
Já que agora aprendemos a usar o LINT, agora  vamos aprender como usar o Lint no JavaScript usando o Docker. 


## Passo 1: Configuração do ambiente

O primeiro passo é criar uma pasta para o seu projeto. Abra o terminal e execute o seguinte comando:

>mkdir lint-javascript
>cd lint-javascript

Acesse a pasta do projeto:
>cd lint-javascript

## Passo 2: Configurando o Docker

Agora, vamos configurar o ambiente do Docker para executar o Lint. Crie um arquivo chamado `Dockerfile` na pasta do projeto e adicione o seguinte conteúdo:

````
FROM node:latest
WORKDIR /app
COPY package.json package-lock.json /app/
RUN npm install
COPY . /app/
CMD ["npm", "run", "lint"]
````


Se eu não errei em nada, este arquivo Dockerfile define um contêiner baseado na imagem `node:latest` e configura o diretório de trabalho para `/app`. Em seguida, copia os arquivos `package.json` e `package-lock.json` para o diretório `/app/` no contêiner e instala as dependências usando o `npm install`. Por fim, copia todo o conteúdo do projeto para o contêiner e executa o comando `npm run lint`. Caso não exista o  `package-lock.json`, basta excluir. 

## Passo 3: Configurando as regras de Lint

Agora, precisamos configurar as regras de Lint para o seu projeto. Crie um arquivo chamado `.eslintrc.json` na pasta do projeto e adicione o seguinte conteúdo:

````
{
  "env": {
    "browser": true,
    "es6": true
  },
  "extends": "eslint:recommended",
  "parserOptions": {
    "ecmaVersion": 2018
  },
  "rules": {
    "no-console": "off",
    "semi": "error"
  }
}
````
Neste exemplo, estamos definindo algumas regras básicas de Lint. A regra `"no-console": "off"` permite o uso da função `console.log` em seu código. A regra `"semi": "error"` exige que você utilize ponto e vírgula no final de cada instrução.

Você pode adicionar mais regras ou personalizar as existentes de acordo com suas necessidades.

## Passo 4: Executando o Lint com o Docker

Agora que temos o ambiente Docker configurado e as regras de Lint definidas, vamos executar o Lint no seu código JavaScript. Crie um arquivo chamado `index.js` na pasta do projeto e adicione o seguinte conteúdo:

    function sayHello() {
      console.log('Hello, world!')
    }
    
    sayHello()
Este é um exemplo simples de código JavaScript que imprime "Hello, world!" no console.

No terminal, execute o seguinte comando para construir a imagem Docker:
> docker build -t lint-javascript .

Após a construção da imagem, execute o seguinte comando para executar o Lint no código JavaScript:
> docker run -it --rm lint-javascript

O Lint será executado dentro do contêiner Docker e mostrará os erros ou avisos, se houver algum, com base nas regras definidas no arquivo `.eslintrc.json`. Se não houver erros ou avisos, nenhuma saída será exibida. Lembre-se de que você pode personalizar as regras de Lint de acordo com as necessidades do seu projeto, adicionando ou modificando as configurações no arquivo `.eslintrc.json`.


# Lint com Docker  PY


## Passo 1: Configuração do ambiente

O primeiro passo é criar uma pasta para o seu projeto. Abra o terminal e execute o seguinte comando:

bashCopy code

`mkdir lint-python
cd lint-python` 

Acesse a pasta do projeto:

bashCopy code

`cd lint-python` 

## Passo 2: Configurando o Docker

Agora, vamos configurar o ambiente do Docker para executar o Lint. Crie um arquivo chamado `Dockerfile` na pasta do projeto e adicione o seguinte conteúdo:

    FROM python:latest
    WORKDIR /app
    COPY requirements.txt /app/
    RUN pip install -r requirements.txt
    COPY . /app/
    CMD ["pylint", "main.py"]

Este arquivo Dockerfile define um contêiner baseado na imagem `python:latest` e configura o diretório de trabalho para `/app`. Em seguida, copia o arquivo `requirements.txt` para o diretório `/app/` no contêiner e instala as dependências usando o `pip install -r requirements.txt`. Por fim, copia todo o conteúdo do projeto para o contêiner e executa o comando `pylint main.py`.

## Passo 3: Configurando as regras de Lint

Agora, precisamos configurar as regras de Lint para o seu projeto. Crie um arquivo chamado `.pylintrc` na pasta do projeto e adicione o seguinte conteúdo:


    [MESSAGES CONTROL]
    disable = C0103, C0114, C0116, C0301, R0903
    
    [FORMAT]
    max-line-length = 120

Neste exemplo, estamos definindo algumas configurações básicas para o Lint usando o formato `.pylintrc`. A seção `[MESSAGES CONTROL]` desativa algumas mensagens de aviso específicas, como convenções de nomeação (`C0103`), falta de docstrings (`C0114`, `C0116`) e linhas muito longas (`C0301`). A seção `[FORMAT]` define o limite máximo de comprimento de linha como 120 caracteres.

Você pode adicionar mais regras ou personalizar as existentes de acordo com suas necessidades.

## Passo 4: Criando o arquivo `requirements.txt`

Crie um arquivo chamado `requirements.txt` na pasta do projeto e adicione as seguintes linhas:

>pylint

O arquivo `requirements.txt` é usado para especificar as dependências do projeto. Neste caso, estamos adicionando apenas a dependência do `pylint`, que é a ferramenta de Lint para Python.

## Passo 5: Criando o arquivo `main.py`

Crie um arquivo chamado `main.py` na pasta do projeto e adicione o seguinte conteúdo:

    def say_hello():
        print("Hello, world!")
    
    say_hello()

Este é um exemplo simples de código Python que imprime "Hello, world!" no console.

## Passo 6: Executando o Lint com o Docker

Agora que temos o ambiente Docker configurado, as regras de Lint definidas, o arquivo `requirements.txt` e o arquivo `main.py` criados, vamos executar o Lint no seu código Python. No terminal, execute o seguinte comando para construir a imagem Docker:

>docker build -t lint-python .

Após a construção da imagem, execute o seguinte comando para executar o Lint:

>docker run -it --rm lint-python` 

O Lint será executado dentro do contêiner Docker e mostrará os erros ou avisos, se houver algum, com base nas regras definidas no arquivo `.pylintrc`. Se não houver erros ou avisos, nenhuma saída será exibida.
