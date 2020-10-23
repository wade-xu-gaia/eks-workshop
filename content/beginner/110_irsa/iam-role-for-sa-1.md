---
title: "為服務帳戶建立IAM角色"
date: 2018-11-13T16:36:24+09:00
weight: 30
draft: false
---
---
title: "Creating an IAM Role for Service Account"
date: 2018-11-13T16:36:24+09:00
weight: 30
draft: false
---

### 用eksctl建立服務帳號的IAM角色
### To create an IAM role for your service accounts with eksctl

您必須建立IAM政策指定權限給pod裡面的container。在這個工作坊，我們會用AWS的代管政策"**AmazonS3ReadOnlyAccess**"，允許取得以及列出所有的S3資源。
You must create an IAM policy that specifies the permissions that you would like the containers in your pods to have. In this workshop we will use AWS managed policy named "**AmazonS3ReadOnlyAccess**" which allow get and list for all S3 resources.

在關聯到服務帳戶前，您也需要為您的服務帳戶建立角色。然後幫pod裡面的container角色附加IAM政策。
You must also create a role for your service accounts to use before you associate it with a service account. Then you can then attach a specific IAM policy to the role that gives the containers in your pods the permissions you desire.

##### 取得AmazonS3ReadOnlyAccess的ARN：
##### Get ARN for AmazonS3ReadOnlyAccess:

```
aws iam list-policies --query 'Policies[?PolicyName==`AmazonS3ReadOnlyAccess`].Arn'
```

{{< output >}}
"arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess"
{{< /output >}}

##### 為服務帳號建立IAM角色：
##### Create an IAM role for your service accounts:

```
eksctl create iamserviceaccount --name iam-test --namespace default --cluster eksworkshop-eksctl --attach-policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess --approve --override-existing-serviceaccounts
```

{{< output >}}
[ℹ]  using region {AWS_REGION}
[ℹ]  1 iamserviceaccount (default/iam-test) was included (based on the include/exclude rules)
[!]  metadata of serviceaccounts that exist in Kubernetes will be updated, as --override-existing-serviceaccounts was set
[ℹ]  1 task: { 2 sequential sub-tasks: { create IAM role for serviceaccount "default/iam-test", create serviceaccount "default/iam-test" } }
[ℹ]  building iamserviceaccount stack "eksctl-eksworkshop-eksctl-addon-iamserviceaccount-default-iam-test"
[ℹ]  deploying stack "eksctl-eksworkshop-eksctl-addon-iamserviceaccount-default-iam-test"
[ℹ]  created serviceaccount "default/iam-test"
{{< /output >}}


{{% notice info %}}
如果您連上[CloudFormation控制台](https://console.aws.amazon.com/cloudformation/)，您會發現"**eksctl-eksworkshop-eksctl-addon-iamserviceaccount-default-iam-test**"已經為您的服務帳戶建立了一個角色。
If you go to the [CloudFormation in IAM Console](https://console.aws.amazon.com/cloudformation/), you will find the stack "**eksctl-eksworkshop-eksctl-addon-iamserviceaccount-default-iam-test**" has been created a role for your service account
{{% /notice %}}
