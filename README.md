# Create and monitor a mongodb app with Kubernetes, Prometheus and Grafana
## 1. Create minikube cluster

	minikube start

## 2. Add all the neccessary repositories

	helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
	helm repo add stable https://charts.helm.sh/stable

## 3. Update all the added repositorioes 

	helm repo update

## 4. Install prometheus chart inside minikube cluster - 28.08.2022

	helm install prometheus prometheus-community/kube-prometheus-stack

## 5. Create a mongodb configmap and save it as mongodb.yaml

	nano
## (You can use the mongodb.yaml file from this repository and copy its content)	

## 6. Apply the configmap created into minikube cluster
	
	kubectl apply -f mongodb.yaml


## 7. Create another configmap in order to override some of the mongodb exporter configurations and save it as values.yaml
#### (You can use the values.yaml file from this repository and copy its content)	
	nano 
		

## 8. Install mongodb exporter and override its values with values.yaml

	helm install mongodb-exporter prometheus-community/prometheus-mongodb-exporter -f values.yaml

## 9. Verify and analise all the data/metrics using prometheus/grafana

	kubectl port-forward service/prometheus-kube-prometheus-prometheus 9090
	kubectl port-forward deployment/prometheus-grafana 3000
	kubectl port-forward service/mongodb-exporter-prometheus-mongodb-exporter 9216  

## In case you want to delete minikube cluster
	minikube delete
