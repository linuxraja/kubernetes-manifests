mkdir ghost
cd ghost
touch Chart.yaml
touch values.yaml
mkdir template
touch template/service.yaml
touch template/deployment.yaml

helm show values ghost

vi Chart.yaml
name: ghost
version: 1

helm show values ghost
helm install demo ghost --dry-run
helm install demo ghost
kubectl get svc
kubectl get deploy
kubectl get pods

helm status demo
helm delete demo
