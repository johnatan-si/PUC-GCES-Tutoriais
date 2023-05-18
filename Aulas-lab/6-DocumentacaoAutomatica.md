
## Documentação Automática com JSDoc e [Sphinx](#sphinx)

Nessa aula você vai aprender a documentar de maneira automática código JAVASCRIPT. Para gerar documentação automática em projetos JavaScript, uma das ferramentas populares é o JSDoc. O JSDoc permite adicionar anotações de documentação ao código-fonte JavaScript e, em seguida, gerar uma documentação estruturada automaticamente com base nessas anotações.  Siga os passos a seguir para  usar o JSDoc:

### Passo 1: Instalação do JSDoc

Abra o terminal e navegue até o diretório raiz do seu projeto JavaScript. Em seguida, execute o seguinte comando para instalar o JSDoc como uma dependência de desenvolvimento:

````
npm install --save-dev jsdoc
````

### Passo 2: Adição de anotações JSDoc

Mano, pelo amor de Deus, preste atenção para não fazer caca. No código JavaScript que deseja documentar, adicione anotações JSDoc acima das funções, classes, métodos e propriedades que você deseja documentar. Aqui está um exemplo simples:

````
/**
 * Calcula a soma de dois números.
 * @param {number} a - O primeiro número.
 * @param {number} b - O segundo número.
 * @returns {number} A soma dos dois números.
 */
function soma(a, b) {
  return a + b;
}
````

As anotações JSDoc são adicionadas como comentários acima da declaração da função. Elas descrevem os parâmetros, o tipo de retorno e outras informações relevantes. No exemplo acima, as anotações JSDoc estão presentes acima da função `soma()`. Elas descrevem os parâmetros `a` e `b`, especificando seus tipos (`number`), e também descrevem o retorno da função como `number`, indicando que a função retorna a soma dos dois números. As anotações JSDoc seguem o padrão `@tag {tipo} nome - descrição`. É importante adicionar essas anotações JSDoc corretamente acima das declarações das funções, classes, métodos e propriedades que você deseja documentar.


### Passo 3: Geração da documentação

Com as anotações JSDoc adicionadas, você pode gerar a documentação executando o seguinte comando no terminal:

````
npx jsdoc -c jsdoc.json
````

Isso instrui o JSDoc a usar o arquivo de configuração `jsdoc.json` **(que você criará no próximo passo)** para gerar a documentação.

### Passo 4: Configuração do JSDoc (opcional)

Você pode criar um arquivo `jsdoc.json` no diretório raiz do seu projeto para configurar o processo de geração da documentação JSDoc. Aqui está um exemplo básico:

````
{
  "source": {
    "include": ["./src"],
    "exclude": ["./node_modules"]
  },
  "opts": {
    "destination": "./docs"
  },
  "plugins": [],
  "templates": {
    "cleverLinks": false,
    "monospaceLinks": false
  }
}

````

Neste exemplo, o diretório `./src` é incluído como fonte para a documentação e o diretório `./node_modules` é excluído. O diretório de destino para a documentação é `./docs`.

### Passo 5: Visualização da documentação

Após a geração da documentação, você pode abrir o diretório de destino especificado (no exemplo, `./docs`) para acessar os arquivos HTML da documentação gerada. Abra o arquivo `index.html` em um navegador para visualizar a documentação.


# Sphinx

### Passo 1: Instalação do Sphinx

Abra o terminal e execute o seguinte comando para instalar o Sphinx:

````
pip install sphinx
````


### Passo 2: Inicialização do projeto Sphinx
No diretório raiz do seu projeto Python, execute o seguinte comando para iniciar o projeto Sphinx:

````
sphinx-quickstart
````

Você será solicitado a fornecer algumas informações sobre o projeto, como nome do projeto, autoria, idioma etc. Você pode selecionar as opções que melhor se adequar ao seu projeto ou pressionar Enter para usar as configurações padrão.

### Passo 3: Configuração do Sphinx

Após a inicialização do projeto Sphinx, você pode personalizar a configuração no arquivo `conf.py` no diretório raiz do projeto. Este arquivo contém várias opções de configuração, como extensões a serem usadas, tema do layout, entre outros. Você também pode adicionar os caminhos para os módulos que deseja documentar ao `sys.path` no arquivo `conf.py`:

````
import os
import sys

sys.path.insert(0, os.path.abspath('..'))
````

Isso permitirá que o Sphinx encontre seus módulos durante a geração da documentação.

### Passo 4: Adição de documentação aos módulos

Para adicionar a documentação aos módulos do seu projeto, você pode criar arquivos `.rst` (reStructuredText) na pasta `source` do seu projeto Sphinx. Por exemplo, se você deseja documentar um módulo chamado `meu_modulo.py`, crie um arquivo `meu_modulo.rst` na pasta `source` e adicione a documentação usando o formato reStructuredText. Aqui está um exemplo básico de um arquivo `.rst` para documentar um módulo:

````
.. module:: meu_modulo
   :synopsis: Módulo de exemplo.

.. automodule:: meu_modulo
   :members:
````

No exemplo acima, o primeiro bloco define o nome e uma breve descrição do módulo. O segundo bloco, `automodule`, instrui o Sphinx a documentar automaticamente todos os membros do módulo.

### Passo 5: Geração da documentação

Após adicionar a documentação aos módulos, você pode gerar a documentação executando o seguinte comando no terminal, no diretório raiz do projeto Sphinx:

````
sphinx-build -b html source build
````
Isso instrui o Sphinx a gerar a documentação HTML na pasta `build`.

### Passo 6: Visualização da documentação

Após a geração da documentação, você pode abrir a pasta `build/html` e encontrar os arquivos HTML da documentação gerada. Abra o arquivo `index.html` em um navegador para visualizar a documentação.

