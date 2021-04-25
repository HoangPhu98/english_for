sudo kubeadm init \
  --pod-network-cidr=198.198.0.0/16 \
  --control-plane-endpoint=13.212.201.132

Follow link:
https://rancher.com/docs/rancher/v2.x/en/installation/resources/advanced/air-gap-helm2/install-rancher/
 
## Install cert-manager

https://cert-manager.io/docs/installation/kubernetes/

Note cert version

helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.3.1 \
  
## Install rancher by template

Download tgz file

Then extract with helm template command


helm template ./rancher-2.5.7.tgz --output-dir . --name-template rancher \
 --namespace cattle-system \
 --set hostname=rancher.orsolution.tk \
 --set certmanager.version=v1.3.1 \
 --set useBundledSystemChart=true
 
Fuck God

kubectl -n cattle-system apply -R -f ./rancher
 
Can edit external ip or using node port

apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 9376
  externalIPs:
    - 80.11.12.10
