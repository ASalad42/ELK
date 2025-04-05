# ELK

![image](https://github.com/user-attachments/assets/125e6eff-2137-4bca-979e-2cd74f1bc41f)


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

## Amazon EBS CSI driver

- Create IAM OIDC provider for cluster
- https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html
- create Amazon EBS CSI driver IAM role
- https://docs.aws.amazon.com/eks/latest/userguide/ebs-csi.html#csi-iam-role
- add Amazon EBS CSI driver add-on.
- https://docs.aws.amazon.com/eks/latest/userguide/creating-an-add-on.html
- ![image](https://github.com/user-attachments/assets/afe37cb8-2804-4ba9-b214-ef34610fd18e)
- kubectl get all -l app.kubernetes.io/name=aws-ebs-csi-driver -n kube-system
![image](https://github.com/user-attachments/assets/6e53f52b-36e4-47f1-9107-a184e05e72a0)

## Install ELK on EKS via Helm

- `kubectl create ns elk`
- `helm help`
- `helm repo update`
- `helm repo add elastic https://helm.elastic.co`
- `helm show values elastic/filebeat > values.yml`
- `helm show values elastic/logstash > values.yml`
- `helm show values elastic/elasticsearch > values.yml`
- `helm show values elastic/kibana > values.yml`
- kubectl get storageclass -n elk
- default StorageClass that comes with Amazon EKS.
- use this storage class in values.yml of elasticsearch before install to make sure pvc and pv are created dynamically. 
- kubectl get pvc -n elk
- kubectl describe pod elasticsearch-master-0 -n elk
- kubectl describe pvc elasticsearch-master-elasticsearch-master-0 -n elk
- ![image](https://github.com/user-attachments/assets/95e0cffc-fb1f-42ea-8bf5-4a3625713b2a)

```.yaml
volumeClaimTemplate:
  accessModes: ["ReadWriteOnce"]
  resources:
    requests:
      storage: 4Gi
  storageClassName: gp2
```

- `helm install elasticsearch elastic/elasticsearch -f values.yml -n elk`
- `helm upgrade --install elasticsearch elastic/elasticsearch -f values.yml -n elk`
- `kubectl get secret elasticsearch-master-credentials -n elk -o yaml`
- `helm install logstash elastic/logstash -f values.yml -n elk`
- `helm install filebeat elastic/filebeat -f values.yml -n elk`
- `helm install kibana elastic/kibana -f values.yml -n elk`
- ![image](https://github.com/user-attachments/assets/ce193588-e6d3-41d2-b638-50c4444d1437)
- ![image](https://github.com/user-attachments/assets/7e852f73-a80b-440f-a61c-b5e963ef6e3d)
- ![image](https://github.com/user-attachments/assets/efbad974-13ac-4d21-a0f2-ac9da67e8831)
- ![image](https://github.com/user-attachments/assets/76ec5001-d505-4806-b7ef-259e3f060236)
- ![image](https://github.com/user-attachments/assets/32807fc7-1e27-40f2-8f52-a5e35ee13b27)
- `kubectl get secrets -n elk  elasticsearch-master-credentials -o jsonpath="{.data.username}" | base64 --decode`
- `kubectl get secrets -n elk  elasticsearch-master-credentials -o jsonpath="{.data.password}" | base64 --decode`
- visit http://abb0b513aa08f472dbb613f95b94b98e-1226330087.eu-west-1.elb.amazonaws.com:5601
- login with username and password from secrets
- ![image](https://github.com/user-attachments/assets/586fa61b-2294-491e-8941-90ecac9b2a64)
- ![image](https://github.com/user-attachments/assets/be2a7682-b0ae-400a-a3e7-0a4478050e76)
- ![image](https://github.com/user-attachments/assets/b4b44859-e49f-4602-81e6-cbb7e5d0a147)





