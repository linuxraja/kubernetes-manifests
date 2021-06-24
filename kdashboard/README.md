![logo](https://cloudwwh.com/wp-content/uploads/2019/10/cropped-logo-3.png)

1) Install the Web UI Dashboard using the recommended yaml file provided by Kubernetes:

``` kubectl apply -f https://raw.githubusercontent.com/linuxraja/kubernetes-manifests/main/kdashboard/recommended.yaml```

    Source :  https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta4/aio/deploy/recommended.yaml
    This Create two services dashboard-metrics-scraper & kubernetes-dashboard```
        

2) Create Service Account (kadmin)

```
kubectl apply -f https://raw.githubusercontent.com/linuxraja/kubernetes-manifests/main/kdashboard/create-admin-sa-dashboard.yaml   
```

3) Create the Cluster Role Binding 

```
kubectl apply -f https://raw.githubusercontent.com/linuxraja/kubernetes-manifests/main/kdashboard/create-admin-rb-dashboard.yaml
```

4) Query the secret for the kadmin and get the token...

```
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep kadmin | awk '{print $1}')
```

5) The dashboard port will listen on localhost:8001. You need to run the Kubernetes proxy

```
$ kubectl proxy
```

6) Tunnel the proxy port into the server with ssh where you want to access the dashboard on the browser
In a terminal emulator window Mac OR Putty or Mobaxterm etc 

```
$ ssh -g -L 8001:localhost:8001 -f -N User@<Kubernetes_Master_IP>
```

7) Once the tunnel has been established, enter the following URL 

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/


Ref : 
```
https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md
```
