# kubernetes
minikube start
kubectl apply -f configMap.yml
kubectl apply -f secret.yml
kubectl apply -f deployment.yml
kubectl apply -f service.yml 
kubectl apply -f hpa.yml
kubectl apply -f ingress.yml
kubectl logs -f deployment/appgrupo1 --all-containers=true --since=10m

kubectl get pods
kubectl get svc appgrupo1-service
kubectl get hpa
kubectl get ingress


A.-probando la ip local dentro de un pod:
kubectl get pods
kubectl exec --stdin --tty pod/appgrupo1-7c5f899b4b-flqz5 -- /bin/sh
dentro del pod se valida que el servicio esta ok: 
wget http://localhost:8081/rest/mscovid/test?msg=testing -O resultado
/usr/src/app # cat resultado 
{"deaths":0,"confirmed":0,"date":null,"mensaje":"Mensaje Recibido: testing","country":null,"recovered":0,"active":0}/usr/src/app # 

B.-probando la ip del servicio:
kubectl get svc appgrupo1-service
wget http://10.104.181.29:80/rest/mscovid/test?msg=testing -O resultadoServicio

C.-Ahora probando con la ip de ingress
kubectl get ingress
https://192.168.64.3/rest/mscovid/test?msg=testing


Si quiero borrar el deployment:
kubectl delete deployment/appgrupo1
