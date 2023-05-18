

## Poetry: Gerenciador de Dependências Python

O Poetry é uma ferramenta de gerenciamento de dependências e ambiente para projetos Python. Ele facilita a criação, atualização e distribuição de pacotes Python, além de gerenciar ambientes virtuais. Neste tutorial, você aprenderá como instalar o Poetry e usar suas principais funcionalidades.

### Passo 1: Instalação do Poetry

Para instalar o Poetry, abra o terminal e execute o seguinte comando:

````
curl -sSL https://install.python-poetry.org | python -
````

Após a instalação, verifique se o Poetry foi instalado corretamente executando o comando:

````
poetry --version
````

Você verá a versão do Poetry instalada no seu sistema. Se não aparecer a versão do Poetry, então não foi instalado corretamente. Veja se não houve erro na instalação. 

### Passo 2: Inicialização de um novo projeto

No diretório raiz do seu projeto Python, execute o seguinte comando para inicializar um novo projeto com o Poetry:

````
poetry init
````

Você será solicitado a fornecer informações sobre o projeto, como nome, descrição, autor, entre outros. Preencha as informações conforme necessário ou pressione Enter para usar as configurações padrão.


### Passo 3: Adição de dependências

Para adicionar dependências ao seu projeto, você pode executar o seguinte comando:

````
poetry add pacote
````


Substitua "pacote" pelo nome do pacote Python que você deseja adicionar. O Poetry irá gerenciar a instalação e a inclusão da dependência no arquivo `pyproject.toml`, que é o arquivo de configuração do Poetry.

### Passo 4: Atualização de dependências

Se você deseja atualizar as dependências do seu projeto, execute o seguinte comando:

````
poetry update
````

Isso atualizará todas as dependências para suas versões mais recentes, de acordo com as restrições definidas no arquivo `pyproject.toml`.

### Passo 5: Criação de ambiente virtual

O Poetry permite criar e gerenciar ambientes virtuais para isolar as dependências do projeto. Para criar um novo ambiente virtual, execute o seguinte comando:

````
poetry shell
````

Isso ativará o ambiente virtual do Poetry e você poderá trabalhar com as dependências específicas do projeto.

### Passo 6: Execução de scripts e comandos


Você pode executar scripts e comandos diretamente no contexto do Poetry. Por exemplo, para executar um script Python, use o seguinte comando:

````
poetry run python script.py
````

Isso executará o script Python dentro do ambiente virtual do Poetry, garantindo que todas as dependências estejam corretamente configuradas.

### Passo 7: Exportação de dependências

O Poetry permite exportar as dependências do seu projeto em um formato adequado para distribuição. Para exportar as dependências em um arquivo `requirements.txt`, execute o seguinte comando:
````
poetry export -f requirements.txt --output requirements.txt
````


Isso criará um arquivo `requirements.txt` com as dependências e suas versões correspondentes.


## Exemplo de uso do Poetry

### Passo 1: Instalação do Poetry

Certifique-se de ter o Poetry instalado seguindo as instruções do passo 1 do tutorial anterior.

### Passo 2: Inicialização de um novo projeto

No diretório raiz do seu projeto, execute o seguinte comando para inicializar um novo projeto com o Poetry:

````
poetry init
````

Preencha as informações solicitadas, como nome, descrição e autor do projeto.

### Passo 3: Adição de dependências

Adicione algumas dependências ao projeto. Vamos adicionar as bibliotecas `requests` e `beautifulsoup4` como exemplo:

````
poetry add requests beautifulsoup4
````

O Poetry irá gerenciar a instalação das dependências e atualizar o arquivo `pyproject.toml` com as informações.

### Passo 4: Criação de um script Python

Crie um arquivo chamado `main.py` e adicione o seguinte código:

````
import requests
from bs4 import BeautifulSoup

response = requests.get("https://exemplo.com")

soup = BeautifulSoup(response.text, "html.parser")

print(soup.title.text)
````

Esse é apenas um exemplo simples para ilustrar o uso de dependências no seu projeto.

### Passo 5: Execução do script

No terminal, execute o seguinte comando para executar o script Python:

````
poetry run python main.py
````

O Poetry ativará o ambiente virtual do projeto e executará o script com as dependências corretamente configuradas.

### Passo 6: Exportação de dependências

O Poetry permite exportar as dependências do seu projeto em um formato adequado para distribuição. Para exportar as dependências em um arquivo `requirements.txt`, execute o seguinte comando:

````
poetry export -f requirements.txt --output requirements.txt
````

Isso criará um arquivo `requirements.txt` com as dependências e suas versões correspondentes. O arquivo `requirements.txt` é amplamente utilizado para gerenciar as dependências de projetos Python em diversos ambientes.

A exportação das dependências para o formato `requirements.txt` permite que outras pessoas possam instalar as mesmas versões das dependências do seu projeto de forma consistente.

Lembre-se de atualizar o arquivo `requirements.txt` sempre que adicionar, remover ou atualizar dependências no seu projeto.
