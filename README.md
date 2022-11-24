## How to reproduce __ingress nginx__ issue [9222](https://github.com/kubernetes/ingress-nginx/issues/9222)

1. Setup a cluser with 2 nodes. We used Ubuntu 18.04 with Cilium CNI but don't know if that is important.
1. `helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ext-auth --create-namespace --version 4.1.4 -f ./ingress-nginx-values.yaml`
1. `kubectl apply -f ./ext-auth.yaml`
1. Perform GET requests to a specific node (for example GET http) while deleting the CoreDNS pods (`kubectl --namespace kube-system delete pods -l k8s-app=kube-dns`)
1. Performing this a couple of times causes the bug to happen
