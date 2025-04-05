# ELK

- `aws eks update-kubeconfig --region eu-west-1 --name ELK-Stack-v2`
- `aws eks --region eu-west-1 update-kubeconfig  --name ELK-Stack-v2`
- `aws eks --region eu-west-1  describe-cluster --name ELK-Stack-v2`
- `kubectl get svc`
- `kubectl get all`
- `kubectl get pods`
- `kubectl get ns`
- `kubectl get nodes --watch`
- `kubectl get nodes`
- `kubectl get storageclass`
- `kubectl get pv`
- `kubectl get pvc --namespace=default`
- `kubectl get ingress --namespace=default`
- `helm help`
- `helm repo update`
- `helm repo add elastic https://helm.elastic.co`
- `helm show values elastic/filebeat > values.yml`
- `helm show values elastic/logstash > values.yml`
- `helm show values elastic/elasticsearch > values.yml`
- `helm show values elastic/kibana > values.yml`
- `helm install elasticsearch elastic/elasticsearch -f values.yml -n elk`
- `helm install filebeat elastic/filebeat -f values.yml -n elk`
- `helm install logstash elastic/logstash -f values.yml -n elk`
- `helm install kibana elastic/kibana -f values.yml -n elk`
- `kubectl get secret elasticsearch-master-credentials -o jsonpath="{.data.username}" | base64 --decode`
- `kubectl get secret elasticsearch-master-credentials -o jsonpath="{.data.password}" | base64 --decode`

## Amazon EBS CSI driver

- Create IAM OIDC provider for cluster > create Amazon EBS CSI driver IAM role > add Amazon EBS CSI driver add-on.
- <https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html>
- <https://docs.aws.amazon.com/eks/latest/userguide/csi-iam-role.html>
- <https://docs.aws.amazon.com/eks/latest/userguide/managing-ebs-csi.html>
- <https://docs.aws.amazon.com/eks/latest/userguide/ebs-sample-app.html>
