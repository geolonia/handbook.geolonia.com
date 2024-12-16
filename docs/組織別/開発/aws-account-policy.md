# AWSアカウント運用

## 前提条件

Geolonia では、「最小権限の原則」（ Principle of Least Privilege ）を重要としています。必要以上に権限を付与すると、悪意を持った攻撃者だけではなく、間違いや勘違いなどを原因とする不具合を防ぐことができます。概ねのポリーしとしては下記となります：

* dev / prod 環境はそれぞれ、違うAWSアカウントで管理する
* AWSアカウントを使うときは、必ずルートアカウント経由で入ります（それぞれのアカウントでIAMユーザーを作らない - よっぽどな理由がなければIAMユーザーを作らない。）
* IAMロールを作るときは必要以上な権限を付与しない（例えば、S3 Bucketへのアクセスを付与するときは、全てのBucketにたいして asterisk で付与しないなど）
* 特権・通常業務の権限を分ける
    * 基本的なルールとしては、通常業務はAWSコンソールに入って操作することはしない。できるだけ、ツール（CLIツールでもあり）で操作します。
* クラウドインフラの管理は基本的に IaC (Infrastructure as Code) のツールを利用します
    * Terraform, AWS CDK, CloudFormation, Serverless Framework など

## ログイン方法

### マネジメントコンソールで使う場合

AWS にログインするときには、 AWS Identity Center 経由でログインを行います。

[https://geolonia.awsapps.com/start](https://geolonia.awsapps.com/start)

こちらにログインすると、アクセスできるアカウント一覧と、そのアカウントのロールを確認することができます。ロール名をクリックすると、そのアカウントの管理画面にログインされます。

### CLI で使う場合

#### 初期設定

まずは、 aws-cli v2 をインストールしましょう [English](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) / [日本語](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/getting-started-install.html)

そして、SSOを設定します。

```
> aws configure sso
SSO session name (Recommended): geolonia
SSO start URL [None]: https://geolonia.awsapps.com/start
SSO region [None]: ap-northeast-1
SSO registration scopes [sso:account:access]: sso:account:access
Attempting to automatically open the SSO authorization page in your default browser.
If the browser does not open or you wish to use a different device to authorize this request, open the following URL:

https://device.sso.ap-northeast-1.amazonaws.com/

Then enter the code:

XXXX-YYYY
There are XYZ AWS accounts available to you.
<ログインしたいアカウントを選ぶ>
<使いたいロールを選ぶ>
Using the role name "XXYYZZRole"
CLI default client Region [None]: ap-northeast-1 (または適切なリージョン名)
CLI default output format [None]: json
CLI profile name [...]: (短い、覚えやすい名前がおすすめ)

To use this profile, specify the profile name using --profile, as shown:

aws s3 ls --profile ...
```

`AWS_PROFILE` 環境変数として先ほど設定した `CLI profile name` を設定すると、 aws コマンドや他のAWSのAPIを利用するツールが、そのアカウントのロールで認証されます。例えば、Geoloniaメインアカウントは `gl` で設定して、認証がうまく行っているかを確認するために、 aws sts get-caller-identity を利用してください。もし成功している場合は、下記のような出力になります。

```
$ export AWS_PROFILE=gl
$ aws sts get-caller-identity
{
    "UserId": "...",
    "Account": "762706324393",
    "Arn": "arn:aws:sts::762706324393:assumed-role/AWSReservedSSO_..."
}
```

プロフィール名を変更したい場合は、 `~/.aws/config` の 該当の `[profile XXYYZZ-123123]` を `[profile <設定したい名>]` に変更しファイル保存すると、変更されます。

#### アカウントの追加

再び `aws configure sso` を実行します。`SSO session name` は以前入力した `geolonia` に設定すると、アクセスできるアカウント一覧が出ます。上記と同様に、別アカウントも設定できます。

## 新規AWSアカウントの作成方法

* `geolonia-rootacct` にログイン
* [AWS Organizations](https://us-east-1.console.aws.amazon.com/organizations/v2/home/accounts) に遷移
* "Add an AWS account" をクリック
    * アカウント名
    * メールアドレス
        * `dev+${account_name}-${env}@geolonia.com` (env = dev / v1 / ...)
    * IAM role name
        * `OrganizationAccountAccessRole` ←こちらを変えるとログインできなくなってしまう可能性があります。ご注意ください。
* 作成ボタンを押す
* 作成終わったら、一覧から選択して、ActionsからMoveを選択して、該当組織分類に移動できます。

## 権限の編集方法

* `geolonia-rootacct` にログイン
* [IAM Identity Center](https://ap-northeast-1.console.aws.amazon.com/singlesignon/home?region=ap-northeast-1) に遷移

ここから、左側の Users / Groups / AWS accounts で管理できます。

詳しくは [公式ドキュメンテーション](https://docs.aws.amazon.com/ja_jp/singlesignon/latest/userguide/what-is.html) を確認してください。
