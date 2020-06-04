# kubernetes-bootstrapper
Bootstrap kubernetes with a few resources for monitoring and meshing

This repo serves as the source for https://medium.com/@chris_linguine/how-to-monitor-your-kubernetes-cluster-with-prometheus-and-grafana-2d5704187fc8  

Follow the link to get everything up and running if you have helm version less 3.


* 		An existing Kubernetes Cluster.
* 		kubectl & helm binaries locally installed ( For Helm version 3 or above)

Commands for Prometheus(Monitoring Tool) using Helm 

    # helm repo update 

    # helm repo add stable https://kubernetes-charts.storage.googleapis.com 

    # helm repo add incubator https://kubernetes-charts-incubator.storage.googleapis.com

Create namespace namely: monitoring
 
    # kubectl create namespace monitoring

Install Prometheus     

    # helm install prometheus stable/prometheus --namespace monitoring
    
Port Forwarding to Port 8000 (Use --> 127.0.0.1:8000 or localhost:8000 to access Prometheus Server) 
 
    # kubectl port-forward svc/prometheus-server -n monitoring 8000:80

Commmands for Grafana(Visualization Tool) using Helm

    # kubectl apply -f monitoring/grafana/config.yml
    
    # helm install grafana stable/grafana     -f monitoring/grafana/values.yml   --namespace monitoring
    
Password would be revealed by using the following command 
 
    # kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo


Locate the pod name of grafana
 
    # kubectl get pods -n monitoring
    
Copy the grafana pod as follow to port forward to 3000 
 
    #  kubectl --namespace monitoring port-forward {GRAFANA POD NAME} 3000
 
Alternatively, you may use instead of command encouraged in previous line.

    # export POD_NAME=$(kubectl get pods --namespace monitoring -l "app=grafana,release=grafana" -o jsonpath="        {.items[0].metadata.name}")
    
Voila, you will be able to use Prometheus and Grafana using 127.0.0.1:8000 and 127.0.0.1:3000, respectively. 




    
    

 
   
    
    
    
