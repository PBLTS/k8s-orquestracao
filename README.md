# k8s-orquestracao

EXEMPLO DE ORQUESTRAÇAO USANDO O KUBERNETES

Executar o Deployment 
kubectl apply -f simpleApp.yaml  

Criar o Service 
kubectl apply -f simpleAppsvc.yaml  

Criar o HPA
kubectl apply -f simpleApphpa.yaml   


Com todos os pontos rodando pode se executar o teste de como o K8s pode orquestrar um ecossistema, com esse scripr abaixo podemos criar uma forma de executar requisições.
Essas requisições vão fazer com  que o HPA possa ser acionado e ocorrer o scalling dos pods e o control plane (Master) irá orquestrar o ecossistema e as requisiçoes.:

kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://hpa-demo-deployment; done"


PARA SUBIR UM NGINX E EXPOR UMA APP PARA EM UM IP E PORTA

Criar o deployment
kubectl create -f nginxdeployment.yaml

Criar o Service
kubectl create -f nginxservice.yaml

Criar o auto-scale
autoscale deployment nginxdeployment --cpu-percent=50 --min=1 --max=10
