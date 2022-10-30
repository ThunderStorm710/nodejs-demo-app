# Create and monitor a mongodb app with Kubernetes, Prometheus and Grafana
## 1. Criar cluster minikube

	minikube start

## 2. Adicionar todos os repositórios

	helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
	helm repo add stable https://charts.helm.sh/stable

## 3. Procurar atualizações dos repositórios

	helm repo update

## 4. Instalar o chart promtheus no minikube - 28.08.2022

	helm install prometheus prometheus-community/kube-prometheus-stack

## 5. Criar um configmap mongodb e guardar como mongodb.yaml

	nano
## (Usar o ficheiro mongodb.yaml do repositório e copiar o conteúdo)	

## 6. Aplicar o configmap ao minikube
	
	kubectl apply -f mongodb.yaml


## 7. Criar outro ficheiro configmap para fazer o override de algumas configurações do mongodb exporter e guardar como values.yaml
#### (Usar o ficheiro values.yaml e mongodb.yaml do repositório e copiar o conteúdo)	
	nano 
		

## 8. Instalar o mongodb exporter juntamente com o values.yaml

	helm install mongodb-exporter prometheus-community/prometheus-mongodb-exporter -f values.yaml

## 9. Verificar e analisar os dados/metrics usando o prometheus ou a grafana

	kubectl port-forward service/prometheus-kube-prometheus-prometheus 9090
	kubectl port-forward deployment/prometheus-grafana 3000
	kubectl port-forward service/mongodb-exporter-prometheus-mongodb-exporter 9216  

## Para apagar e limpar tudo
	minikube delete
