# kubernetes-bootstrapper
Bootstrap kubernetes with a few resources for monitoring and meshing

This repo serves as the source for https://medium.com/@chris_linguine/how-to-monitor-your-kubernetes-cluster-with-prometheus-and-grafana-2d5704187fc8

Follow that arrticle to get everything up and running. 

If you have any issues, don't hesitate commenting or opening an issue.

USING HELM 3 or ABOVE. 

Commands are as follows for Prometheus(Monitoring Tool) and Grafana(Visualization Tool) 

    # helm repo update 

    # helm repo add stable https://kubernetes-charts.storage.googleapis.com 

    # helm repo add incubator https://kubernetes-charts-incubator.storage.googleapis.com

 Create namespace namely: monitoring
 
    # kubectl create namespace monitoring
    
Install Prometheus     

    # helm install prometheus stable/prometheus --namespace monitoring
    
 Port Forwarding to Port 8000 
 
    # kubectl port-forward svc/prometheus-server -n monitoring 8000:80
    
    
    
