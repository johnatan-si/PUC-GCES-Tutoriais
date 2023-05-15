
# Aplicação JavaScript com Nginx em um Contêiner

Você aprenderá como usar o **Nginx** para servir uma aplicação **JavaScript** em um contêiner Docker e como adicionar esse contêiner ao **Docker** Compose. Usaremos JavaScript como exemplo.


## Passo 1: Estrutura do projeto

1.  Crie uma pasta para o projeto em um local de sua preferência.
    
2.  Dentro dessa pasta, crie um arquivo `index.html` e um diretório `js`.
    
3.  Coloque seus arquivos JavaScript dentro do diretório `js`. Certifique-se de ter pelo menos um arquivo JavaScript principal que será carregado pelo `index.html`.
4. Crie o arquivo index.html
````
<!DOCTYPE html>
<html>
<head>
    <title>Minha Aplicação</title>
    <script src="js/script.js"></script>
</head>
<body>
    <h1>Minha Aplicação</h1>
    <p id="output"></p>
</body>
</html>

````
5. Conteúdo do arquivo `js/script.js`:
````
document.addEventListener("DOMContentLoaded", function() {
    var output = document.getElementById("output");
    output.textContent = "Olá, Mundo!";
});

````
 
6. A estrutura do projeto deve ser semelhante a esta:
````
projeto/
  ├── index.html
  └── js/
      └── script.js

````

## Passo 2: Configurando o Dockerfile

1. Crie um arquivo chamado `Dockerfile` na pasta do projeto.
    
2.  Abra o arquivo `Dockerfile` em um editor de texto.
    
3.  Adicione o seguinte conteúdo ao arquivo `Dockerfile`:
````
# Define a imagem base
FROM nginx

# Remove o arquivo de configuração padrão do Nginx
RUN rm /etc/nginx/conf.d/default.conf

# Copia o arquivo de configuração personalizado para o diretório correto no contêiner
COPY nginx.conf /etc/nginx/conf.d/

# Copia a aplicação para o diretório raiz do servidor Nginx
COPY . /usr/share/nginx/html

# Define a porta em que o contêiner Nginx será exposto
EXPOSE 80

# Comando para iniciar o servidor Nginx
CMD ["nginx", "-g", "daemon off;"]
````


Neste arquivo, usamos a imagem base oficial do Nginx disponível no Docker Hub. Removemos o arquivo de configuração padrão do Nginx e copiamos nosso arquivo de configuração personalizado `nginx.conf` para o diretório `/etc/nginx/conf.d/` no contêiner. Em seguida, copiamos todo o conteúdo do projeto para o diretório raiz do servidor Nginx dentro do contêiner. Definimos a porta `80` para expor o contêiner Nginx e usamos o comando `nginx -g "daemon off;"` para iniciar o servidor Nginx.

## Passo 3: Criando o arquivo de configuração Nginx

1.  No diretório do projeto, crie um arquivo chamado `nginx.conf`.
    
2.  Abra o arquivo `nginx.conf` em um editor de texto.
    
3.  Adicione o seguinte conteúdo ao arquivo `nginx.conf`:

````
server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }
}

````

Neste arquivo de configuração, definimos um servidor Nginx para escutar na porta `80` e responder a solicitações para o `localhost`. Configuramos o diretório raiz como `/usr/share/nginx/html`e definimos o arquivo`index.html` como o arquivo de índice padrão.

## Passo 4: Construindo a imagem Docker

1.  Abra um terminal ou prompt de comando.
    
2.  Navegue até a pasta do projeto onde estão localizados os arquivos `Dockerfile`, `index.html`, `js` e `nginx.conf`.
    
3.  Execute o seguinte comando para construir a imagem Docker:
````
docker build -t myapp .
````

Isso irá construir a imagem Docker com o nome `myapp` com base no `Dockerfile` e nos arquivos do projeto.

## Passo 5: Criando o arquivo Docker Compose

1.  No diretório do projeto, crie um arquivo chamado `docker-compose.yml`.
    
2.  Abra o arquivo `docker-compose.yml` em um editor de texto.
    
3.  Adicione o seguinte conteúdo ao arquivo `docker-compose.yml`:
````
version: '3'
services:
  app:
    image: myapp
    ports:
      - 80:80

````

Neste arquivo `docker-compose.yml`, definimos um serviço chamado `app` que usa a imagem `myapp` que construímos anteriormente. Mapeamos a porta `80` do host para a porta `80` do contêiner.

## Passo 6: Executando a aplicação

1.  No terminal ou prompt de comando, navegue até o diretório do projeto onde está localizado o arquivo `docker-compose.yml`.
    
2.  Execute o seguinte comando para iniciar a aplicação:
````
docker-compose up
````

Isso iniciará a construção da imagem e a criação do contêiner com base nas configurações definidas no arquivo `docker-compose.yml`.

3.  Após a inicialização bem-sucedida, você poderá acessar a aplicação em seu navegador da web usando o seguinte URL: http://localhost


Agora você tem uma aplicação JavaScript sendo servida pelo Nginx em um contêiner Docker. A aplicação estará disponível no `localhost` na porta `80`.

Você pode personalizar a aplicação adicionando mais arquivos JavaScript, estilos CSS ou outras dependências. Basta colocar os arquivos adicionais no diretório do projeto e ajustar a configuração do servidor Nginx, se necessário. Lembre-se de parar o Docker Compose quando não estiver mais usando a aplicação, usando o atalho `Ctrl+C` no terminal onde o Docker Compose está sendo executado.
