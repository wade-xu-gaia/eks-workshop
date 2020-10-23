---
title: "清理環境"
date: 2019-03-20T13:59:44+01:00
weight: 60
draft: false
---
---
title: "Cleanup"
date: 2019-03-20T13:59:44+01:00
weight: 60
draft: false
---

根據下列步驟清理環境。
To cleanup, follow the below steps.

移除範例的程式：
To remove sample application

```
kubectl delete -f iam-pod.yaml
```

從CloudFormation移除IAM角色以及服務帳戶的堆棧：
To remove IAM role and Service Account stack from cloudformation

```
eksctl delete iamserviceaccount --name iam-test --namespace default --cluster eksworkshop-eksctl
```