cluster:
	minikube start

deps:
	helm dependency build .

install:
	helm install fleetdm .


port-forward:
	kubectl -n default port-forward svc/fleetdm-fleet 8080:8080

logs:
	kubectl -n default logs -l app.kubernetes.io/name=fleet -f

uninstall:
	helm uninstall fleetdm

delete-cluster:
	minikube delete
