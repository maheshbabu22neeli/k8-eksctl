# k8-eksctl
Create EKS Cluster

## Install Eks-Ctl in k8-workstation
Using eks-ctl we can create, delete and update EKS Cluster. 
```shell
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH
curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
sudo install -m 0755 /tmp/eksctl /usr/local/bin && rm /tmp/eksctl

Now, verify version

[ ec2-user@ip-172-31-18-254 ~ ]$ eksctl version
0.225.0
```

## k8-cluster config

```yaml
# spot-cluster.yaml

apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: roboshop
  region: us-east-1

managedNodeGroups:
  - name: spot
    instanceTypes: ["c3.large","c4.large","c5.large","c5d.large","c5n.large","c5a.large","m7i-flex.large","c7i-flex.large"]
    spot: true
    desiredCapacity: 2
```

## Create k8-cluster
```shell
eksctl create cluster --config-file=eksctl.yaml
```

## Delete k8-cluster
```shell
eksctl delete cluster --config-file=eksctl.yaml
or
eksctl delete cluster --region=us-east-1 --name=roboshop
```