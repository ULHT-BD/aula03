# aula03
Nesta aula começamos a trabalhar a linguagem SQL. Começamos por configurar o ambiente de trabalho com Docker, Base de Dados exemplo e cliente. Introduzimos a linguagem SQL começando com utilização do SELECT para obtenção de dados simples da BD, introduzimos a sintaxe INSERT para inserir tuplos, UPDATE para modificar dados e DELETE para remover tuplos. O conjunto de exercícios propostos permitem praticar e validar aprendizagem. Bom trabalho!

[1. Prepare o seu ambiente de trabalho](#1-prepare-o-seu-ambiente-de-trabalho)

[2. Comando Select](#2-comando-select)

[3. Comando Insert](#3-comando-insert)

[4. Comando Update](#4-comando-update)

[5. Comando Delete](#5-comando-delete)

[Bibliografia e Referências](#bibliografia-e-referencias)

[Outros](#outros)

## 1. Prepare o seu ambiente de trabalho

Pode relembrar a aula 1 através dos slides disponiveis [aqui](https://github.com/ULHT-BD/aula03/blob/main/Aula01%20-%20Apresentacao%20-%20BD%20-%20Docker.pdf)

### 1.1 Instale e configure o Docker exemplo
a. Comece por descarregar e instalar o docker em https://www.docker.com/products/docker-desktop/
* NOTA: A instalação em Windows requer a instalação do [Windows System for Linux](https://docs.microsoft.com/en-us/windows/wsl/)

b. Descarregue o ficheiro zip [docker_db_aula03.zip](https://github.com/ULHT-BD/aula03/blob/main/docker_db_aula03.zip) disponibilizado neste repositório. Descomprima e examine o conteúdo.
* O Dockerfile permite criar uma imagem docker com uma instância do MariaDB e uma base de dados exemplo hr com a seguinte estrutura.
<img width="872" alt="image" src="https://user-images.githubusercontent.com/32137262/193691701-47c51106-73dd-4f88-b319-49c910e9ef5c.png">


c. Para criar a imagem docker que será usada nesta aula, abra uma linha de comandos (terminal, powershell, ...) e navegue até à pasta que extraiu no ponto b, onde encontrará o ficheiro Dockerfile. Execute o comando 
  ```docker build -t db .```
  
  (relembre: a flag ```-t db``` atribui a tag db à imagem criada para futuras utilizações)
  
  ``` sh
  cd ~\Desktop\docker_db_aula03
  docker build -t db .
  ```
  
  Pode listar as imagens criadas utilizando o comando ```docker images```
  
  
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

c. Navegue e explore visualmente a Base de Dados exemplo hr
<img width="890" alt="image" src="https://user-images.githubusercontent.com/32137262/193685718-b4bacf95-d66d-4b1d-9b13-848a1f8cf54e.png">


## 2. Comando Select
O comando SQL ```SELECT``` permite obter ou consultar os tuplos existentes numa relação. A sintaxe é
``` sql
SELECT atributo1, atributo2, ...
FROM relacao;
```
NOTA:
* ```*``` é um wildcard que representa todas as colunas/atributos

Exemplos:
* obter atributos nome e idade da relação/tabela estudante:
``` sql
SELECT nome, idade FROM estudante;
```
* obter todos os atributos da relação/tabela estudante:
``` sql
SELECT * FROM estudante;
```

### Exercícios
Para cada uma das alíneas seguintes, escreva a query que permite obter:
1. Obtenha a lista de todos os nomes de países existentes na relação Countries

2. Obtenha a lista de todos os códigos e nomes de países existentes na relação Countries

3. Obtenha o primeiro nome, último nome e salário de todos os empregados

4. Obtenha todos os tuplos e respetivos atributos sobre regiões

5. Pesquise empregados cujo primeiro nome é 'John'

6. Pesquise empregados cujo salário é superior a 6000

## 3. Comando Insert
O comando SQL ```INSERT``` permite inserir tuplos numa relação. Após inserir cada uma das alíneas seguintes lembre-se de verificar que o conteúdo foi corretamente inserido utilizando o comando ```SELECT```. A sintaxe é
``` sql
INSERT INTO relacao (atributo1, atributo2, ...)
VALUES (valor-atribut1, valor-atributo2, ...);
```

Caso queira inserir um tuplo completo pode omitir o nome dos atributos ter atençao de respeitar a ordem pela qual foram criados, a sintaxe é
``` sql
INSERT INTO relacao
VALUES (valor-atribut1, valor-atributo2, ...);
```

Em qualquer um dos formatos anteriores pode inserir varios tuplos de uma so vez separando-os por virgula, por exemplo
``` sql
INSERT INTO relacao
VALUES 
  (t1-valor-atribut1, t1-valor-atributo2, ...),
  (t2-valor-atribut1, t2-valor-atributo2, ...),
  (t3-valor-atribut1, t3-valor-atributo2, ...);
```
###Exercícios
Para cada uma das alíneas seguintes, escreva a query que permite obter:
1. Utilize o comando insert para inserir o País Portugal na tabela countries
* ```COUNTRY_ID = 'PT'```
* ```COUNTRY_NAME = 'Portugal'```
* ```REGION_ID = 1``` (Europe)

2. Utilize o comando insert para inserir tuplos para os países Áustria (AT), Hungria (HU), Peru (PE) e Tailândia (TH)

3. Crie um novo cargo DB Administrator (IT_DBA) com salário compreendido entre 6000 e 12000

## 4. Comando Update
O comando SQL ```UPDATE``` permite modificar valores de tuplos numa relação. Lembre-se de utilizar o comando ```SELECT``` antes e após alterar o conteúdo indicado em cada uma das alíneas seguintes para verificar que o conteúdo foi corretamente alterado. A sintaxe é
``` sql
UPDATE relacao
SET atributo1 = valor-atribut1, atributo2 = valor-atributo2, ...
WHERE condição;
```

### Exercícios
Para cada uma das alíneas seguintes, escreva a query que permite obter:
1. Utilize o comando update para alterar o nome da região ```Europe``` para o nome português ```Europa```. Atualize as restantes regiões também para português

2. Utilize o comando update para alterar o salário do ```Michael Rogers``` para ```3300``` e o apelido do ```John Chen``` para ```Smith```

3. Atualize o salário mínimo de todas as funções para ```3500```

## 5. Comando Delete
O comando SQL ```DELETE``` permite remover tuplos de uma relação. Lembre-se de utilizar o comando ```SELECT``` antes e após remover o conteúdo indicado em cada uma das alíneas seguintes para verificar o comportamento pretendido. A sintaxe é
``` sql
DELETE FROM relacao
WHERE condição;
```

### Exercícios
Para cada uma das alíneas seguintes, escreva a query que permite obter:
1. Utilize o comando delete para remover o país Hungria da relação countries

2. Remova da relação emp o empregado cujo nome é ```Adams```

3. Remova da relação emp os empregados cujo salário é inferior a ```1000```

4. Remova a região Europa e verifique o comportamento?

## Bibliografia e Referências
Recorde a história das Bases de Dados Relacionais, introduzida nas aulas através da infografia e vídeo anexos (fontes: peterjamesthomas.com e www.computerhistory.org) 

## Outros
Para dúvidas e discussões pode juntar-se ao grupo slack da turma através do [link](https://join.slack.com/t/ulht-bd/shared_invite/zt-1h783xcc2-eRQlIYSqFkDeOAqGC045Rw)
