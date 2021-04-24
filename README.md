# kubernetes
minikube start
kubectl apply -f deployment.yml
kubectl apply -f service.yml 
kubectl apply -f hpa.yml

kubectl get pods
kubectl get svc appgrupo1-service
kubectl get hpa

curl -X GET 'http://localhost:8080/rest/mscovid/test?msg=testing'