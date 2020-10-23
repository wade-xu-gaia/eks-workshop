---
title: "部署範例Pod"
date: 2018-11-13T16:36:24+09:00
weight: 50
draft: false
---
---
title: "Deploy Sample Pod"
date: 2018-11-13T16:36:24+09:00
weight: 50
draft: false
---

為了用IAM角色執行Pod，我們完成了所有必要的設定。我們會在叢集中部署範例pod，然後執行測試命令來確認它會不會正常的執行。
Now that we have completed all the necessary configuration to run a Pod with IAM role. We will deploy sample Pod to the cluster, and run a test command to see whether it works correctly or not.

```
curl -LO https://eksworkshop.com/beginner/110_irsa/deploy.files/iam-pod.yaml
kubectl apply -f iam-pod.yaml
```

##### 確認您的pod在**Running**的狀態：
##### Make sure your pod is in **Running** status:

```
kubectl get pod
```

{{< output >}}
eks-iam-test-7fb8c5ffb8-fdr6c  1/1  Running  0  5m23s
{{< /output >}}

##### 進入pod：
##### Get into the Pod:

```
kubectl exec -it <place Pod Name> /bin/bash
```

##### 手動呼叫sts:AssumeRoleWithWebIdentity，如果設定正確的話，您會看到AccessKeyId、SecretAccessKey的資訊
##### Manually Call sts:AssumeRoleWithWebIdentity, and you will see AccessKeyId, SecretAccessKey information if configuration is set appropriately

```
aws sts assume-role-with-web-identity \
--role-arn $AWS_ROLE_ARN \
--role-session-name mh9test \
--web-identity-token file://$AWS_WEB_IDENTITY_TOKEN_FILE \
--duration-seconds 1000
```

##### 執行awscli看看是否能取得Amazon S3 buckets的列表：
##### Run awscli to see if it retrives list of Amazon S3 buckets:

```
aws s3 ls
```

##### 執行awscli確認是否能取得Amazon EC2實例的列表，這並沒有在IAM角色中被分派到權限：
##### Run awscli to see if it retrives list of Amazon EC2 instances which does not have privileges in the allocated IAM policy:

```
aws ec2 describe-instances --region us-west-2
```

##### 您會收到這個錯誤訊息：
##### You will get this error message:

{{< output >}}
An error occurred (UnauthorizedOperation) when calling the DescribeInstances operation: You are not authorized to perform this operation.
{{< /output >}}