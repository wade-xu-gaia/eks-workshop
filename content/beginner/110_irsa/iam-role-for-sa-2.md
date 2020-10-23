---
title: "為服務帳戶指定IAM角色"
date: 2018-11-13T16:36:24+09:00
weight: 40
draft: false
---
---
title: "Specifying an IAM Role for Service Account"
date: 2018-11-13T16:36:24+09:00
weight: 40
draft: false
---

### 為服務帳戶指定IAM角色
### Specifying an IAM Role for your Service Account

在上一步驟， 我們在叢集中建立了IAM角色並且與**iam-test**這個服務帳戶。這早就在指定的服務帳戶建立角色時就已經幫您完成了。

In the previous step, we created the IAM role that associated with a service account named **iam-test** in the cluster and this has already been done for you with the service account you specified when creating the role.

##### 確認服務帳戶iam-test存在：
##### Be sure your service account iam-test exists:

```
kubectl get sa
```

| NAME | SECRETS | AGE |
| ---- | ------- | --- |
| default | 1 | 85m |
| **iam-test** | 1 | 44m |

##### 確認服務帳戶有ARN宣告的IAM角色：
##### Make sure your service account with the ARN of the IAM role is annotated:

```
kubectl describe sa iam-test
```
{{< output >}}

Name:                iam-test
Namespace:           default
Labels:              <none>
Annotations:         eks.amazonaws.com/role-arn: arn:aws:iam::14xxxxxxxx84:role/eksctl-eksworkshop-eksctl-addon-iamserviceac-Role1-1PJ5Q3H39Z5M9
Image pull secrets:  <none>
Mountable secrets:   iam-test-token-5n9cb
Tokens:              iam-test-token-5n9cb
Events:              <none>
{{< /output >}}
