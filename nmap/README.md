## nmap

### Scan a CIDR range

```bash

nmap 10.108.165.0/24

```

### Stealth scanning

```bash

sudo nmap -sS 10.108.165.96

```


### Samples with kubernetes/multipass

```bash



kubectl create namespace debug
kubectl run debug --image nginx --namespace debug

kubectl exec -it debug --namespace debug -- apt update 
kubectl exec -it debug --namespace debug -- apt install nmap -y 



kubectl exec -it debug --namespace debug -- bash

kubectl exec -it debug --namespace debug -- nmap

kubectl exec -it debug --namespace debug -- nmap -sS 10.244.0.0/24 10.244.1.0/24 10.244.2.0/24



kubectl delete namespace debug 

```

