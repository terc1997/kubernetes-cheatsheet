# Debugging Ingress
## 1. Clone the repository
```
git clone git@github.com:terc1997/kubernetes-cheatsheet.git
```
## 2. Set the environment variables
```
export $NAMESPACE=<namespace>
export $HOST=<host>
```
## 3. Apply the file
```
kubectl apply -f test.yaml
```
## 4. Check the Pod Health
```
kubectl get pod
kubectl describe pod test
```
## 5. Check the Pod connection with Service
Get the Pod IP in `kubectl get pod`, then
```
kubectl exec -it pod test -- /bin/bash
curl -kL http://<IP>:5678
```
Check if the result is `test`. If it is, it means that your service is running.
## 6. Check the Ingress
```
kubectl describe ing test-ingress
```
Verify if the endpoint IP of the Pod is the same of the Ingress. Then, verify the connection:
```
curl -kL http://$HOST/test
```
Check if the output is `test`.
If it is, it means that, maybe, the problem isn't the Ingress Controller. Execute the step 1 to 6 with the required Pod and Service to debug.
