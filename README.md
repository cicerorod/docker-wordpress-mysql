# docker-wordpress-mysql
Exemplo de criação de ambiente (wordpress/mysql) utilizando dockerfile e dockercompose

## ![](https://img.icons8.com/metro/20/000000/run-command.png) Execução

### Clone

1. Clonar via prompt de comando o projeto em uma pasta de sua preferência: `git clone https://github.com/cicerorod/docker-wordpress-mysql.git`
2. Acessar a pasta principal do projeto via prompt de comando. Ex: `cd docker-mysql-php`;

**1)** Criar a arquivo Dockerfile com a definição da imagem que precisamos:
Exemplo:
 
```

FROM ubuntu

MAINTAINER Jackson Araujo de Lima

RUN apt-get update

RUN apt-get install -y nginx && apt-get clean

ADD ./configs/nginx.conf /etc/nginx/sites-enabled/default

RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

EXPOSE 8080

CMD service nginx start -g

``` 


**2)** Execuatar o comando `$ docker build -t cicerorod/nginx:v1 .` para criar a imagem contida no arquivo

**3)** Para testar `$ docker run -d -p 8089:8080 --name myNginx1 cicerorod/nginx:v1`


ou `$ docker run -it --rm cicerorod/nginx:v1 bash` para acessar o bash o linux

**4)** Para acessar o servido do nginx via navegador: `http://localhost:8089`


**5)** Criar o arquivoa docker-compose.yml que coném os serviços a serem criados

```

version: '2'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8010:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
volumes:
    db_data:

```

**6)** Executar o comando `$ docker-compose.exe up -d` para criação de todos os containers

**7)** Para acessar o servido do nginx via navegador: `http://localhost:8010`

**8)** Para finalizar os containers e remover-los `$ docker-compose down`


## ![](https://img.icons8.com/ios-glyphs/20/000000/pull-request.png) Contribuições

1. Faça o _fork_ do projeto (<https://github.com/cicerorod/docker-mysql-php/fork>)
2. Crie uma _branch_ para sua modificação (`git checkout -b feature/[nome]`)
3. Faça o _commit_ (`git commit -am 'Add files [nome]'`)
4. _Push_ (`git push origin feature/[nome]`)
5. Crie um novo _Pull Request_

## ![](https://img.icons8.com/windows/20/000000/regular-document.png) Licença

Este projeto está sob a licença do MIT. Consulte [LICENSE](https://github.com/cicerorod/docker-wordpress-mysql/blob/master/LICENSE) para obter mais informações.

## ![](https://img.icons8.com/ios-glyphs/22/000000/code-file.png) Desenvolvedor

<img src="https://avatars.githubusercontent.com/cicerorod" width=115>

[![](https://img.icons8.com/fluent/30/000000/github.png)](https://github.com/cicerorod)
[![](https://img.icons8.com/metro/25/000000/linkedin.png)](https://www.linkedin.com/in/c%C3%ADcero-rodrigues-89623784/)
[![](https://img.icons8.com/metro/25/000000/facebook.png)](https://www.facebook.com/cicero.rodrigues.90834)
[![](https://img.icons8.com/material-rounded/29/000000/instagram-new.png)](https://www.instagram.com/cicero_rod/)
[![](https://img.icons8.com/metro/26/000000/email.png)](mailto:cicerorod@gmail.com)

<p align="center">
  <img src="https://img.icons8.com/wired/32/000000/icons8-new-logo.png" >
  </br>
  <a href="https://icons8.com/icon/">Icons by Icons8</a>
</p>



