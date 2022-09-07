## Start minikube

    Cf. https://minikube.sigs.k8s.io/docs/start/

## Build the custom httpd image

    eval $(minikube docker-env)
    cd images/httpd
    docker build . -t custom-httpd

## Deploy httpd

    cd httpd
    kubectl apply -f namespace.yaml
    kubectl apply -f .

## Deploy ingress controller

    cd ingress
    kubectl apply -f namespace.yaml
    kubectl apply -f .


## Reproduce the issue

### Ack your host file

I simply update my `/etc/hosts` adding name "minikube" resolved to the minikube IP:

Get the minikube IP 

    minikube service -n opportal-pro-ingress nginx-np

Add entry (where the IP has to be replaced by the output of the minikube service command):

    192.168.49.2 minikube


### CURL

Execute multiple time if needed until it hangs

    curl -k --limit-rate 800k https://minikube:30443/data/ea4761d6-c7b4-11ec-b6f4-01aa75ed71a1.en.PDF.pdf  -o /dev/null

It should stop downloading:

    $ curl -k --limit-rate 800k https://minikube:30443/data/ea4761d6-c7b4-11ec-b6f4-01aa75ed71a1.en.PDF.pdf  -o /dev/null
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
    Dload  Upload   Total   Spent    Left  Speed
    0 23.7M    0  199k    0     0   2145      0  3:13:31  0:01:35  3:11:56     0
