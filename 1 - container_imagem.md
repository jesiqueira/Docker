# O São imagesn?

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
-
