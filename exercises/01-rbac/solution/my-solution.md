# my solution


```sh
mkdir cert && cd cert
openssl genrsa -out edib.key 2048
openssl req -new -key edib.key -out edib.csr -subj "/CN=edib/O=group1"

openssl x509 -req -in edib.csr -CA /etc/kubernetes/pki/ca.crt -CAkey /etc/kubernetes/pki/ca.key -CAcreateserial -out edib.crt -days 500

kubectl config set-credentials edib --client-certificate=edib.crt --client-key=edib.key

kubectl config set-context edib-context --cluster=cluster.local --user=edib

kubectl config use-context edib-context
kubectl config current-context

kubectl run nginx --image=nginx --port=80

kubectl config use-context kubernetes-admin@cluster.local
kubectl run nginx --image=nginx --port=80

kubectl create role  pod-reader --resource=pods --verb=get,watch,list 


k create rolebinding read-pods --user edib --role pod-reader

kubectl get roles,rolebindings

kubectl config use-context edib-context
kubectl run nginx1 --image=nginx --port=80

kubectl get pods

k auth can-i edib
k auth can-i list pods --as edib

kubectl config use-context kubernetes-admin@cluster.local
k auth can-i list pods --as edib
k auth can-i create pods --as edib


```
