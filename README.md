# istio-namespace
Setting up Istio in a separate namespace 
The Istio documentation is pretty good to set up istio in a local cluster. 

Adding my notes here to set up istio in a separate kubernetes namespace if you don't want to pollute the main namespace.
Clone this repo and follow to set up istio in a different namespace. 

##### Download and install Istio
> curl -L https://istio.io/downloadIstio | sh -
> 
> cd istio-1.11.0
> 
> export PATH=$PWD/bin:$PATH
> 
> istioctl install --set profile=demo -y

##### Create Namespace and allow istio injection 
> kubectl create namespace istio-apps
> 
> kubectl label namespace istio-apps istio-injection=enabled

##### Deploy the app and Test
> kubectl apply -f bookinfo.yaml --namespace istio-apps
> 
> kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}' --namespace istio-apps)" --namespace istio-apps -c ratings -- curl -sS productpage:9080/productpage | grep -o "&lt;title&gt;.*&lt;/title&gt;"
> 

