#Google Cloud introdução ao GKE.

Objetivos desse laboratório, aprender a fazer o seguinte.

* Provisionar um cluster do Kubernetes usando o Kubernetes Engine
* Implantar e gerenciar contêineres do Docker usando a kubectl.

* Criar um cluster do Google Kubernetes Engine com vários contêineres, e cada um deles terá um servidor da Web.

* Foi colocado um balanceador de carga na frente do cluster.

1. Na barra de ferramentas no canto superior direito do console do Cloud, clique no botão Ativar o Cloud Shell.

2. Clique em Continuar.

3. No prompt do Cloud Shell, digite o comando a seguir para exportar a variável de ambiente chamada MY_ZONE. 

export MY_ZONE="Zone" 

4. Inicie um cluster do Kubernetes gerenciado pelo Kubernetes Engine. Dê ao cluster o nome webfrontend e configure-o para executar dois nós.

gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

Obs.A criação de um cluster leva alguns minutos porque o Kubernetes Engine provisiona as máquinas virtuais.

5. Após a criação do cluster, verifique a versão instalada do Kubernetes com o comando kubectl version:

kubectl version

6. Confira os nós em execução no console do GCP. No Menu de navegação (Ícone do menu de navegação), clique em Compute Engine > Instâncias de VM.

O cluster do Kubernetes está pronto para ser usado.


 Execute e implante um contêiner

 1. No prompt do Cloud Shell, inicie uma única instância do contêiner nginx. O nginx é um servidor da Web bastante conhecido.

 kubectl create deploy nginx --image=nginx:1.17.10

 2. Verifique o pod que está executando o contêiner nginx.

kubectl get pods

 3. Exponha o contêiner nginx à Internet.

kubectl expose deployment nginx --port 80 --type LoadBalancer

 4. Veja o novo serviço.

# kubectl get services

Obs.Use o endereço IP externo exibido para testar e acessar o contêiner nginx remotamente.
Talvez leve alguns segundos para que o campo External-IP do seu serviço seja preenchido. Isso é normal. 

5. Abra uma nova guia do navegador da Web e cole o endereço IP externo do cluster na barra de endereço. A página inicial padrão do navegador Nginx é exibida.

6. Aumente o número de pods em execução no serviço.

kubectl scale deployment nginx --replicas 3

Obs. O escalonamento vertical de uma implantação é útil para aumentar os recursos disponíveis em um aplicativo que estiver atraindo mais usuários.

7. Confirme se o Kubernetes atualizou o número de pods.

kubectl get pods

8. Confirme se o endereço IP externo não mudou.

kubectl get services

9. Volte para a guia do navegador da Internet em que você viu o endereço IP externo do cluster. Atualize a página para confirmar se o servidor da Web nginx ainda está respondendo.

Parabéns!

Neste laboratório, você configurou um cluster do Kubernetes no Kubernetes Engine.
