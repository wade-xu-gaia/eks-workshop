---
title: "建立OIDC身份提供者"
date: 2018-11-13T16:36:24+09:00
weight: 20
draft: false
---
---
title: "Create an OIDC identity provider"
date: 2018-11-13T16:36:24+09:00
weight: 20
draft: false
---

### 用eksctl為叢集建立一個IAM OIDC身份提供者
### To create an IAM OIDC identity provider for your cluster with eksctl

為了在您的叢集使用服務帳戶的IAM角色，您需要在IAM控制台建立一個OIDC身份提供者。
To use IAM roles for service accounts in your cluster, you must create an OIDC identity provider in the IAM console

##### 檢查您的eksctl版本高於0.5.1
##### Check your eksctl version that your eksctl version is at least 0.5.1

```
eksctl version
```

{{< output >}}
[ℹ]  version.Info{BuiltAt:"", GitCommit:"", GitTag:"0.5.3"}
{{< /output >}}

{{% notice info %}}
假如您的eksctl的版本低於0.5.1，參照使用手冊中的[安裝或升級eksctl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html#installing-eksctl)。
If your eksctl version is lower than 0.5.1, use [Installing or Upgrading eksctl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html#installing-eksctl) in the user guide
{{% /notice %}}

##### 為您的叢集建立OIDC身份提供者
##### Create your OIDC identity provider for your cluster

```
eksctl utils associate-iam-oidc-provider --cluster eksworkshop-eksctl --approve
```

{{< output >}}
[ℹ]  using region {AWS_REGION}
[ℹ]  will create IAM Open ID Connect provider for cluster "eksworkshop-eksctl" in "{AWS_REGION}"
[✔]  created IAM Open ID Connect provider for cluster "eksworkshop-eksctl" in "{AWS_REGION}"
{{< /output >}}

假如您連上[IAM控制台的身份提供者](https://console.aws.amazon.com/iam/home#/providers)，您會發現OIDC提供者已經為您的叢集建立起來了。
If you go to the [Identity Providers in IAM Console](https://console.aws.amazon.com/iam/home#/providers), you will see OIDC provider has created for your cluster

![OIDC Identity Provider](/images/irsa/irsa-oidc.png)