# Comandos básicos:
- docker ps:
  - lista os contantiner em execução
- docker ps -a:
  - lista todas as imagens
# O São imagens?

- Imagens são originadas de arquivos que programamos para que o Docker crie uma estrutura que execute determinadas ações em containers;
- Elas contém informações como: imagens base, diretõrio base, comandos a serem executados, portas da aplicação e etc;
- Ao rofar um container baseado na imagem, as instruções serão executadas em camadas;

# Como escolher uma imagem?

- EScolher as imagens oficiais disponível no hub doc, e que seja especificas.

# Criando uma imagem

- Para criar uma imagem vamos precisar criar um arquivo Dockerfile em uma pasta que ficará o projeto;
- Este aquivo vai precisar de algumas instruções para poder ser executado;
- `FROM` : imagem base;
- `WORKDIR`: diretório da aplicação;
- `EXPOSE`: porta da aplicação;
- `COPY`: quais arquivos precisam ser copiados;

- Exemplo:

    > FROM node

    > WORKDIR /app

    > COPY package*.json /app/

    > RUN npm install

    > COPY . .

    > EXPOSE 3000

    > CMD [ "node","app.js" ]

# Executando uma imagem

- Para executar uma imagem primeiramente `vamos precisar fazer o build`;
- O comando é `docker buil <diretório da imagem>`;
  - Ex: docker build .
- Depois vamos utilizar o `docker run <imagem> para executá-la`;

# Alterando uma imagem

- Semore que alterar o código de uma imagem `vamos precisar fazer o build novamente;`
- Para o Docker é como se fosse `uma imagem completamente nova`;
- Após fazer o build vamos executá-la por outro id único criado com docker run;

# Downlaods das imagens
docker pull `<imagem>`

# Aprender mais sobre os comandos
docker run --help;

# Alterando o nome da image e tag
- docher tag id_imagem nome_da_imagem
- Ex: docker tag cfc6e6dac357 minhaimagem

# Iniciando imagem com o nome
- docker buil -t nome_da_imagem .
- docker buil -t nome_da_imagem:nome_da_tag .

# Reiniciar imagem com container interativo
docker start -i nome_da_imagem

# Remover imagens
- docker rmi `<id ou nome_da_imagem>` opção de usar flag -f

# Remover imagens e container
Como o comando `docker system prune`
Podemos remover imagens, container e networks

# Copiando arquivos entre container
docker cp nome_da_imagem:caminho_do_arquivo_a_ser_copiado diretorio_para_onde_copiar


# Verificar processamento do container
docker top nome_do_container

# Verificar dados de um container
docker inspect `<container>`

# Vericar processamento
- para verificar os processos que estão sendo executados em um container, utilizamos o comando: `docker stats`
- Desta mmaneira temos acesso ao andamento do processameto e  memória gasta pelo mesmo.

# Autenticação no Docker Hub
- Precisa ter conta no hub.docker.com
- Autenticar via terminal vamos utlizar o comando: `docker login`
- entã enviar imagem para HUB!

# Logout do Docker HUb
- Comando: `docker logout`

# Enviando imagem
- COmando: `docker push <imagem>`
- OBS: o nome da imagem local tem que ter o mesmo nome do repositório criado para subir.

# Baixar a imagem
- comando: `docker pull nome_da_imagem`


# Enviando atualização de imagem
- Para enviar uma atualização vamos primeiramento fazer o build
- Trocando a tag da imagem para a versão atualizada
- Depois vamos fazer um push novamente para o repositório
- Assim todas as versões estarão disponíveis para serem utilizadas.
- comando: docker build nome_da_imagem:tag_na_imagem .
- comando: docker push nome_da_imagem:tag_na_image

# Volumes
- ## Tipos de volumes:
  - Anônimos (anonymous): criado pela flag -v, com nome aleatório
  - Nomeados (named): São volumes com nome, podemos nos referir a estes facilmente e saber para que são utilizados n nosso ambiente.
  - Bind mounts: Uma forma de salvar na nossa máquina, sem o gerenciamento do Docker, informamos um diretório para o fim.


# Problema da persistência
- Se criarmos um container com alguma image, `todos os arquivos que geramos dentro dele serão do container`
- Quando o container for removido, perdemos estes arquivos
- Por isso precisamos dos `volumes`


# Volumes anônimos

- Podemos criar um volume anônimo (`anonymous`) da seguinte maneira: `docker run -v /data`
- Onde `/data` será o diretõrio que contém o volume anônmo;
- E este container estará atrelado ao volume anônimo;
- Com o comando `docker volume ls`, podemos ver todos os volumes do nosso ambiente.
  - ## Criando o container anonymous
    -` docker run -d -p 80:80 --name nome_do_container --rm -v /data nome_da_imagem`
    -` obs: `--rm é para remover o container após parar o mesmo, dever ser usado somente para teste.

# Volumes nomeados
- Podemos criar um volume nomeado (`named`) da seguinte maneira: `docker run -v nome_do_volume:/data`
- Agora o volume tem um nome e pode ser facilmente referenciado.
- Em `docker volume ls` podemos verificar o container nomeado criado
- Da mesma maneira que o anônimo, este volume tem como função armazenar arquivos.
  - Exemplos:
  - `docker run -d -p 80:80 --name nome_do_container -v nome_do_volume:mesmo_nome_WORKDIR/local_a_salvar --rm nome_imagem`
    - exemplo:
    - `docker run -d -p 80:80 --name phpmessages_container -v phpvolume:/var/www/html/messages --rm phpmessages`

# Bind Mounts
- `Bind mount` também é um volume, porém ele fica em um diretório quie nós especificamos
- Então não criamos um volume e sim, `apontamos um diretório`
- O comando para criar um bind mount é: `docker run /dir/data:/data`
- Desta maneira o diretório `/dir/data` no nosso computador, será o volume desde container
- Exemplo:
  - `docker run -d -p porta_host:porta_container --name -v nome_do_container diretório_host:diretorio_container --rm nome_imagem`
  - Exemplo:
    - `docker run -d -p 80:80 --name phpmessages_container -v /home/edmar/Documentos/Desenvolvimento/curso_docker/2_volumes/messages:/var/www/html/messages --rm phpmessages`
