# kubernetes
minikube start
kubectl apply -f configMap.yml
kubectl apply -f secret.yml
kubectl apply -f deployment.yml
kubectl apply -f service.yml 
kubectl apply -f hpa.yml
kubectl apply -f ingress.yml

kubectl get pods
kubectl get svc appgrupo1-service
kubectl get hpa

curl -X GET 'http://localhost:8080/rest/mscovid/test?msg=testing'

kubectl get ingress

probando la ip local dentro de un pod:
kubectl exec --stdin --tty pod/appgrupo1-7c5f899b4b-flqz5 -- /bin/sh
dentro del pod se valida que el servicio esta ok: 
wget http://localhost:8081/rest/mscovid/test?msg=testing -O resultado
/usr/src/app # cat resultado 
{"deaths":0,"confirmed":0,"date":null,"mensaje":"Mensaje Recibido: testing","country":null,"recovered":0,"active":0}/usr/src/app # 

probando la ip del servicio:
wget http://10.104.181.29:80/rest/mscovid/test?msg=testing -O resultadoServicio

se valida viendo los logs en vivo de los dos pods creados para verificar que respondan los dos
kubectl logs appgrupo1-7c5f899b4b-flqz5 -f

Ahora probando con la ip de ingress
kubectl get ingress
https://192.168.64.3/rest/mscovid/test?msg=testing

kubectl logs -f deployment/appgrupo1 --all-containers=true --since=10m
kubectl delete deployment/appgrupo1
