# istio get started

## config gke
    export https_proxy="http://127.0.0.1:1087"
    gcloud components install kubectl
    gcloud container clusters get-credentials cluster-1 --zone us-central1-c --project valued-lyceum-341108

    kubectl get all

## install istio
    cd _course_files/warmup-exercise && \
    kubectl apply -f 1-istio-init.yaml
    k apply -f 2-istio-minikube.yaml
    k apply -f 3-kiali-secret.yaml

## enable default namespace for istio to inject sidecar
    kubectl label namespace default istio-injection=enabled
    kubectl describe ns default

## install the demo application
    kubectl apply -f 4-application-full-stack.yaml

## verify sidecar injection
    k get po -> there is 2 container for each pod now, sidecar injected ok

## access GKE nodeport service from internet
    gcloud compute firewall-rules create myservice --allow tcp:30080
    gcloud compute instances list
    http://34.69.253.8:30080/

## access kiali monitoring
    gcloud compute firewall-rules create kiali --allow tcp:31000
    http://34.69.253.8:31000/
    https://kiali.io/

## access Jaeger UI
    gcloud compute firewall-rules create jaeger --allow tcp:31001