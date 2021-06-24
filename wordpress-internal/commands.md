cloud_user@linuxraja-kubemaster:~/code/wordpress$ kubectl get storageclass \
NAME             PROVISIONER                    RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
wordpress-disk   kubernetes.io/no-provisioner   Delete          Immediate           true                   7h43m

cloud_user@linuxraja-kubemaster:~/code/wordpress$ kubectl get pv \
NAME           CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                   STORAGECLASS     REASON   AGE \
mysql-pv       2Gi        RWO            Recycle          Bound    default/wordpress-pvc   wordpress-disk            7h41m \
wordpress-pv   1Gi        RWO            Recycle          Bound    default/mysql-pvc       wordpress-disk            7h41m 

cloud_user@linuxraja-kubemaster:~/code/wordpress$ kubectl get pvc \
NAME            STATUS   VOLUME         CAPACITY   ACCESS MODES   STORAGECLASS     AGE \
mysql-pvc       Bound    wordpress-pv   1Gi        RWO            wordpress-disk   7h41m \
wordpress-pvc   Bound    mysql-pv       2Gi        RWO            wordpress-disk   7h41m 

cloud_user@linuxraja-kubemaster:~/code/wordpress$ kubectl get secrets \
NAME                  TYPE                                  DATA   AGE \
mysql                 Opaque                                1      7h37m 

cloud_user@linuxraja-kubemaster:~/code/wordpress$ kubectl get deployments \
NAME        READY   UP-TO-DATE   AVAILABLE   AGE \
mysql       1/1     1            1           7h34m \
wordpress   1/1     1            1           7h28m 

cloud_user@linuxraja-kubemaster:~/code/wordpress$ kubectl get services \
NAME                TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE \
mysql-service       ClusterIP   None          <none>        3306/TCP       7h32m \
wordpress-service   NodePort    10.96.93.25   <none>        80:30081/TCP   7h14m 

cloud_user@linuxraja-kubemaster:~/code/wordpress$ kubectl get pods \
NAME                                READY   STATUS      RESTARTS   AGE \
mysql-6fd995b675-nkp55              1/1     Running     1          7h35m \
wordpress-5f747657d4-g4wgs          1/1     Running     2          7h29m 

Verification

1. Check conditions: 

kubectl describe deployments wordpress \
kubectl describe deployments mysql 

2. Check Pod Logs 

kubectl logs pod_name 

