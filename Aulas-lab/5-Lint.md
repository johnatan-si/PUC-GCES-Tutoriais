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
