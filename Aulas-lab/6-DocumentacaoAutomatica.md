
## Documentação Automática com JSDoc

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
