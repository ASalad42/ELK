# ELK

## ELK infrastructure

- Deploy ELK infrastructure such as VPC, subnets, security group and EKS cluster via github actions (template.yaml)
- ![image](https://github.com/user-attachments/assets/ffeef627-3f94-4bbf-a3fc-23d1ec865289)
- ![image](https://github.com/user-attachments/assets/af70e43d-719d-448e-864a-df6f540aedca)
- `aws eks update-kubeconfig --region eu-west-1 --name ELK-Stack-v2`
- `aws eks --region eu-west-1  describe-cluster --name ELK-Stack-v2`

## Nodegroup infrastructure

- Deploy nodegroup stack (cloudformation.yaml)
- ![image](https://github.com/user-attachments/assets/954aff81-7ef9-4d85-abe1-6de55dce7774)
- ![image](https://github.com/user-attachments/assets/06d613fb-15cc-4d6b-9f86-66013707eeec)
- ![image](https://github.com/user-attachments/assets/b3f837a3-62b1-4a47-a5ed-5c5b17af9cd8)
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

## Install ELK on EKS via Helm

- `kubectl create ns elk`
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
- ![image](https://github.com/user-attachments/assets/ce193588-e6d3-41d2-b638-50c4444d1437)
- ![image](https://github.com/user-attachments/assets/7e852f73-a80b-440f-a61c-b5e963ef6e3d)
- ![image](https://github.com/user-attachments/assets/efbad974-13ac-4d21-a0f2-ac9da67e8831)




### Amazon EBS CSI driver

- Create IAM OIDC provider for cluster > create Amazon EBS CSI driver IAM role > add Amazon EBS CSI driver add-on.
- <https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html>
- <https://docs.aws.amazon.com/eks/latest/userguide/csi-iam-role.html>
- <https://docs.aws.amazon.com/eks/latest/userguide/managing-ebs-csi.html>
- <https://docs.aws.amazon.com/eks/latest/userguide/ebs-sample-app.html>
