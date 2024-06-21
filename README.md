 Inicie um cluster do Kubernetes Engine

export MY_ZONE="Zone"
gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
kubectl version



kubectl create deploy nginx --image=nginx:1.17.10
kubectl get pods
kubectl expose deployment nginx --port 80 --type LoadBalancer
kubectl get services
kubectl scale deployment nginx --replicas 3
kubectl get pods
kubectl get services
