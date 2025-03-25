# K8S - Lista de Tarefas

## 1.0 Descrição

O objetivo deste projeto é colocar no ar uma aplicação de lista de tarefas. Para fazer isso criei um Cluster Kubernetes local com o **Kind** para fins de testes.

A aplicação contém um frontend, que irá rodar em um pod com duas réplicas. Na aplicação poderemos fazer atividades básicas de CRUD. 

O backend da aplicação contém uma API que desenvolvi com Java. O backend terá somente uma réplica. Como a API salva os dados em um banco H2, não há necessidade de configurar um banco de dados. Para mais detalhes sobre a API, consulte sua documentação.

- Link: [Lista de Tarefas - Backend](https://github.com/paulo-fabiano/lista_tarefas)

## 2.0 Configuração do Cluster

Utilizei para criar um Cluster. Fiz algumas configurações bem básicas.

* Detalhes do Cluster
    
    1. Nome: k8s-lista-tarefas
    2. Nº de Control Planes: 3
    3. Nº Pods do Frontend: 2
    4. Nº Pods do Backend: 1

## 3.0 Configuração da Aplicação

O Frontend da aplicação é bem simples. Contém somente um HTML com algumas poucas informações que foi desenvolvido somente para ser utilizado em conjunto com a API do projeto  [Lista de Tarefas](https://github.com/paulo-fabiano/lista_tarefas). Para fazer utilizei o **Express** do **NODE.js** para subir um servidor que irá servir o arquivo `.html` com as funções que estão no arquivo `app.js` dentro do diretório frontend da aplicação.

## 4.0 Configuração das Imagens Docker

Há dois arquivos Dockerfiles que foram utilizados para gerar as respectivas imagens Docker que foram utilizadas nesse projeto.

Como o Kuberneter utiliza o registre do Docker Hub, enviei as imagens para o meu repositório público. Consulte as imagens atráves dos links abaixo:

- Imagem Frontend -> [pfabianofilho/front-lista-tarefas:v1]()
- Imagem Backend -> [pfabianofilho/back-lista-tarefas:v1]()

