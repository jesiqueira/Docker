# Instalar docker
- sudo apt install docker.io
- Obs: Se tiver problema seguir procedimento da documentação docker

# Conceito de imagem e Container
- Images é o arquivo docke_file que representa a imagem com instrução para executar o container
- Programamos uma imagem para executar por meio de um container

# Imagem disponível para docker
[Hub Docher](https://hub.docker.com/)


# Executar uma imagem
- docker run nome_da_imagem
  - ex: docker run debian
- Obs: executar imagem oficiais disponível no site docker hub

# Executar imagem em modo interativo
- docker run -it nome_da_image
  - Ex; docker run -it debian
- Sair e finalizar docker em execução
  - exit

# Verificar se uma imagem está rodando
- docker ps ou docher container ls
  - Irá listar as imagem em execução

# Verificar container já executador 
- add a flag -a
  - ex: docker ps -a

# Executar container em background
- usar a flag -d (detached)
- Ex: docker run -d nginx
  
# Parar um conteiner em execução
- docker stop nome_do_container ou ID

# Iniciando / Reiniciando Container
- docker start <id_do_container>
- OBS: Comando start inicia o container sem recriar, o comando 'docker run' cria um container
- podemos parar um container com comando stop e com o start podemos voltar a trabalhar no container.

# Expor porta do container
- flag -p
- Ex; docker run -d -p 80:80 nginx
## Trocar a porta do container
- docker run -d -p 3000:80 nginx

# Definir nome para o container
- Comando: --name nome_do_container nome_da_imagem_a_executar
- EX: docker run -d -p 80:80 --name nginx_app nginx

# Verificar os logs do container
- docker logs <id_do_container>
- posso executar com paramentro -f para ficar em execução 

# Remover container
Comando: docker rm <id_do_container ou nome>
## Remover container que está executando
Comando: docker rm <id_do_container ou nome> -f