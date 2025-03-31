# K8S - Lista de Tarefas

## 1.0 Descrição

O objetivo deste projeto é colocar no ar uma aplicação de lista de tarefas. Para fazer isso criei um Cluster Kubernetes local com o **Minikube** para fins de testes.

A aplicação contém um frontend, que irá rodar em um pod. Na aplicação poderemos fazer atividades básicas de CRUD. 

O backend da aplicação contém uma API que desenvolvi com Java. Para mais detalhes da API acesse a docuemntação dela.

- Link: [Lista de Tarefas - Backend](https://github.com/paulo-fabiano/lista_tarefas)

## 2.0 Requisitos

Os requisitos para montar esse ambiente foram:

- Docker
- Minikube
- Kubectl

## 3.0 Configuração do Cluster

Após instalar o **Minikube** em nosso ambiente usamos o comando para iniciar o cluster:

```
minikube start
```

Você verá uma saída parecida com está:

```
😄  minikube v1.35.0 on Ubuntu 22.04 (kvm/amd64)
✨  Using the docker driver based on existing profile
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.46 ...
🔄  Restarting existing docker container for "minikube" ...
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
🔎  Verifying Kubernetes components...
    ▪ Using image registry.k8s.io/ingress-nginx/controller:v1.11.3
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v1.4.4
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v1.4.4
🔎  Verifying ingress addon...
🌟  Enabled addons: default-storageclass, storage-provisioner, ingress
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

Com o Cluster criado, apliquei os arquivos **.yaml** para criar os Pods e os services.

- Criando Pods
  
```
kubectl apply -f deployment.yaml 
```

- Criando Services

```
kubectl apply -f services.yaml
```

Podemos ver se os Pods e os Services foram criados:

- Checando Pods
  
```
kubectl get pods
```

```
NAME                        READY   STATUS    RESTARTS   AGE
backend-6b849bbd5b-tptxn    1/1     Running   0          84m
frontend-5fd4c5dbd7-7skq8   1/1     Running   0          84m
```

- Checando Services
  
```
kubectl get services
```

```
NAME               TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)          AGE
backend-service    LoadBalancer   10.98.129.88   10.98.129.88   8080:31192/TCP   80m
frontend-service   LoadBalancer   10.99.48.25    10.99.48.25    80:32311/TCP     80m
kubernetes         ClusterIP      10.96.0.1      <none>         443/TCP          95m
```

## 4.0 Configuração da Aplicação

O Frontend da aplicação é bem simples. Contém somente um HTML com algumas poucas informações que foi desenvolvido somente para ser utilizado em conjunto com a API do projeto  [Lista de Tarefas](https://github.com/paulo-fabiano/lista_tarefas). Para fazer utilizei o **Express** do **NODE.js** para subir um servidor que irá servir o arquivo `.html` com as funções que estão no arquivo `app.js` dentro do diretório frontend da aplicação.

## 5.0 Configuração das Imagens Docker

Há dois arquivos Dockerfiles que foram utilizados para gerar as respectivas imagens Docker que foram utilizadas nesse projeto.

Como o Kubernetes utiliza o registre do Docker Hub, enviei as imagens para o meu repositório público. Consulte as imagens através dos links abaixo:

- Imagem Frontend -> [pfabianofilho/front-lista-tarefas:v1]()
- Imagem Backend -> [pfabianofilho/back-lista-tarefas:v1]()

## 6.0 Funcionamento

![Aplicação Rodando](/images/image.png)

Como podemos verificar, é possível realizar as operações básicas de CRUD. Perdoem o Frontend da aplicação (rsrs), eu sou bom em muitas coisas. Porém o Frontend não é meu ponto forte. O importante é que funciona né!? rsrs

## 7.0 Aprendizado

O **Minikube** não expõe endereços IPs externos quando utilizamos o Service do tipo **LoadBalancer**, para que ele exponha endereços IPs para testarmos a aplicação localmente é necessário utilizar o comando:

```
 minikube tunnel & disown
```

Outro problema interessante que percebi é que eu estava configurando no arquivo **index.html** a URL do backend como:

```
  <script>
    const BACKEND_URL = "http://backend-service:8080"; 
  </script>
```

Aí comecei a enfrentar alguns erros relacionados a DNS, fiquei um tempo sem entender até compreender que quando eu clicava em `Adicionar` a tarefa o navegador enviava uma requisição para um domínio que não existia, e não para o Pod do backend. Para consertar isso modifiquei o tipo do Service do backend para LoadBalancer para ele ser acessível também fora do Cluster. Após isso modifiquei a variável no frontend para:

```
  <script>
    const BACKEND_URL = "http://10.98.129.88:8080"; 
  </script>
```

E "vualá" (rsrs), como num passe de mágica minha aplicação começou a funcionar corretamente.

O aprendizado é constante! **#rumoaelite**

## 8.0 Dúvidas e Sugestões?

Entre em contato comigo via:

- [Linkedin](https://www.linkedin.com/in/paulo-fabiano)
- [Email](mailto:pfabianof@gmail.com)


