# aula03

## 1. Prepare o seu ambiente de desenvolvimento

Pode relembrar a aula 1 através dos slides disponiveis [aqui](https://github.com/ULHT-BD/aula03/blob/main/Aula01%20-%20Apresentacao%20-%20BD%20-%20Docker.pdf)

### 1.1 Instale e configure o Docker exemplo
a. Comece por descarregar e instalar o docker em https://www.docker.com/products/docker-desktop/

b. Descarregue o ficheiro zip [docker_db_aula03.zip](https://github.com/ULHT-BD/aula03/blob/main/docker_db_aula03.zip) disponibilizado neste repositório. Descomprima e examine o conteúdo.
* O Dockerfile permite criar uma imagem docker com uma instância do MariaDB e uma base de dados exemplo.

c. Para criar a imagem docker que será usada nesta aula, abra uma linha de comandos (terminal, powershell, ...) e navegue até à pasta que extraiu em c. Execute o comando 
  ```docker build -t db .```
  
  (relembre: a flag ```-t db``` atribui a tag db à imagem criada para futuras utilizações)
  
  Pode verificar as imagens criadas utilizando o comando ```docker images```
  
d. Pode agora instanciar um novo container baseado na imagem que acabou de criar. Utilize o comando ```docker run --name mysgbd -p 3306:3306 -d db```
  
  (relembre: a flag ```-p 3306:3306``` mapeia o porto do host para o container, ```-d``` especifica que o docker vair correr em background)
  
  Pode verificar que o docker está em execução utilizando ```docker ps```. Para parar o docker use ```docker stop mysgbd``` e para iniciar ```docker start mysgbd```
  
  
### 1.2 Instale e configure o cliente
a. Descarregue e instale o cliente DBeaver Community em https://dbeaver.io/download/

b. Crie uma nova ligação para aceder ao MariaDB a correr no seu docker
<img width="1007" alt="image" src="https://user-images.githubusercontent.com/32137262/193685274-c7175ac4-881a-4b59-b019-273713ca8633.png">
* host: ```localhost```
* port: ```3306```
* user: ```admin```
* password: ```admin```

<img width="699" alt="image" src="https://user-images.githubusercontent.com/32137262/193685385-ecf08920-1726-4919-bc93-6569b8b9a127.png">

c. Explore visualmente a Base de Dados exemplo hr
<img width="890" alt="image" src="https://user-images.githubusercontent.com/32137262/193685718-b4bacf95-d66d-4b1d-9b13-848a1f8cf54e.png">

