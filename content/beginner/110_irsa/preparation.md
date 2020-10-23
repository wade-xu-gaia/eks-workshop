---
title: "準備環境"
date: 2018-11-13T16:36:24+09:00
weight: 10
draft: false
---
---
title: "Preparation"
date: 2018-11-13T16:36:24+09:00
weight: 10
draft: false
---

### 在您的叢集上啟用IAM角色的服務帳戶
### Enabling IAM Roles for Service Accounts on your Cluster

* 服務帳戶的IAM角色的功能在Amazon EKS Kubernetes 1.14版叢集上可用，叢集在2019年9月3日會從1.13升級到1.14版。
* The IAM roles for service accounts feature is available on new Amazon EKS Kubernetes version 1.14 clusters, and clusters that were updated to versions 1.14 or 1.13 on or after September 3rd, 2019.

{{% notice info %}}
如果您的EKS叢集版本較低或是與上面不符合，請參考使用教學中[更新Amazon EKS叢集版本](https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html)的段落。
If your EKS cluster version is lower or does not match with above, please read the [updating an Amazon EKS Cluster](https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html) section in the User Guide.
{{% /notice %}}

```bash
kubectl version --short
```

{{% notice info %}}
如果您的AWS CLI版本低於1.18.15，請參考使用教學中[安裝AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)的段落。
If your aws cli version is lower than 1.18.15, use [Installing the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) in the User Guide
{{% /notice %}}

```bash
aws --version
```

{{< output >}}
aws-cli/1.18.15 Python/2.7.16 Linux/4.14.133-88.112.amzn1.x86_64 botocore/1.12.228
{{< /output >}}



##### 取得OpenID Connect發行者的URL：
##### Retrieve OpenID Connect issuer URL:

```bash
aws eks describe-cluster --name eksworkshop-eksctl --query cluster.identity.oidc.issuer --output text
```

<div data-proofer-ignore>
{{< output >}}
https://oidc.eks.{AWS_REGION}.amazonaws.com/id/D48675832CA65BD10A532F59741CF90B
{{< /output >}}
</div>