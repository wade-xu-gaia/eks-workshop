---
title: "服務帳戶用的IAM角色"
date: 2018-11-13T16:32:30+09:00
weight: 110
pre: '<i class="fa fa-film" aria-hidden="true"></i> '
draft: false
tags:
  - intermediate
  - CON205
---
---
title: "IAM Roles for Service Accounts"
date: 2018-11-13T16:32:30+09:00
weight: 110
pre: '<i class="fa fa-film" aria-hidden="true"></i> '
draft: false
tags:
  - intermediate
  - CON205
---

### 服務帳戶用的細緻的IAM角色
### Fine-Grained IAM Roles for Service Accounts

{{< youtube lyMKskPXbEA >}}

在Kubernetes1.12版，支援了**ProjectedServiceAccountToken**這個功能，它是OIDC的JWT也含有服務帳戶的身份，也支援可以設定的audience。
In Kubernetes version 1.12, support was added for a new **ProjectedServiceAccountToken** feature, which is an OIDC JSON web token that also contains the service account identity, and supports a configurable audience.

Amazon EKS 現在為每個叢集託管公有OIDC探索端點，其中包含ProjectedServiceAccountToken JWT的簽署金鑰，讓外部系統（例如 IAM）可以驗證和接受Kubernetes發出的OIDC Token。
Amazon EKS now hosts a public OIDC discovery endpoint per cluster containing the signing keys for the ProjectedServiceAccountToken JSON web tokens so external systems, like IAM, can validate and accept the Kubernetes-issued OIDC tokens.

OIDC聯合存取讓您可以透過STS服務assume IAM role。方法是啟用OIDC的身份提供者認證同時接受JWT，換句話說可以做為assume IAM role的。另一邊來說，Kubernetes可以指定所謂的服務帳戶token，剛好符合給 pods用的OIDC JWT。我們設定讓每個pod都備有加密簽署過的Tokedn，可以被STS對OIDC提供者認證。

OIDC federation access allows you to assume IAM roles via the Secure Token Service (STS), enabling authentication with an OIDC provider, receiving a JSON Web Token (JWT), which in turn can be used to assume an IAM role. Kubernetes, on the other hand, can issue so-called projected service account tokens, which happen to be valid OIDC JWTs for pods. Our setup equips each pod with a cryptographically-signed token that can be verified by STS against the OIDC provider of your choice to establish the pod’s identity.

new credential provider ”<span style="color:orange">**sts:AssumeRoleWithWebIdentity**</span>”