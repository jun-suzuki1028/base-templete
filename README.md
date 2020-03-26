# アカウント取得したらやっておこうテンプレート

新規アカウントを取得した場合にやっておいた方がいいセキュリティ周りのあれこれをテンプレート化したもの

ここ見ながらざっくり作成  
[⇒AWSアカウントを作ったら最初にやるべきこと ～令和元年版～](https://dev.classmethod.jp/articles/aws-1st-step-new-era-reiwa/)

この記事も参考になるので、需要があれば参考にしたい  
(マルチリージョン対応ではなく、使うリージョン個別の対応のため、今回の主旨とは若干ずれる)  
[⇒「セキュアで堅牢なAWSアカウント」を実現する CloudFormationテンプレート - ①サービスの有効化](https://qiita.com/eijikominami/items/53f3a1d83df31981ad86)

## 1.IAM

### IAM Group
IAMユーザーを作成したら、必ず入るグループ
以下のポリシーをアタッチして、セキュリティを担保

### IAM Policy
以下2つのポリシーをアタッチ
* IP制限
* MFA強制化

## 2.CloudTrail
* マルチリージョン適用
* ロギング有効化
  * S3バケット


## 3.GuardDuty

以下の記事をほぼそのまま使用。

[CloudFormation一撃でGuardDutyを有効にして、通知をLambdaでイイ感じに編集してSNSへ通知するテンプレート作った](https://dev.classmethod.jp/articles/cloudformation-guardduty-lambda-sns-publish/)

**使う場合はマルチリージョン想定のため、StackSetsで全リージョンに適応させること**

こんな人向け
* SNSトピックをリージョンごとに作成したくない
* Lambdaでいい感じに整形して通知して欲しい  

### 注意
SNSトピックは事前に作成しておくこと。
SNSトピックを作成するテンプレートも一応作成済み

### sns_topic.yaml
GuardDutyに通知するためのテンプレート  
GuardDuty側のスタックのSNSトピック部分を編集するか、手入力でトピックARNを入力  
使わなくてもいい


