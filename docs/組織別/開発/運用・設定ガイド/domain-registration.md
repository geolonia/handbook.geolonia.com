# DNS ドメイン登録方法

ドメインを登録する時には AWS を利用します。

## 事前に判断すること

* ドメイン名
* どのAWSアカウントで登録するか
    * 既存のアカウントで登録することが適切の場合は、既存のアカウントで登録する
    * 既存のアカウントが当てはまらない、新規プロジェクト、などの理由で登録が必要→新規アカウントを作り、登録する

[AWSアカウント運用は該当のページ](/組織別/開発/aws-account-policy.html)を確認ください。

## 登録方法

1. 該当のアカウントにログインする
1. Route 53 コンソールを開く
1. ドメイン登録の画面を開く
    * 新規アカウントの場合、ナビゲーターみたいな画面が出ることがある。そこから「新規ドメインを登録する」みたいなものを選択
    * 既に Route 53 使われているアカウントの場合、左側ナビゲーションから「Domains→Registered domains」にアクセスし、「Register domains」のアクションボタンをクリックする
1. 同時で５個のドメインまで登録可能。「Search..」から入力し、買い物カゴに追加します。
1. 完了したら、Checkout に進む
1. 期間を設定。こちらは適切な期間を設定してください。Auto-renewがonになっている場合はだいたい最短1年でも問題ありません。
1. Registrant contact 情報を入力してください。英字で入力する必要ある。下記「登録連絡情報」を参照にしてください。
1. 入力が終わったら、すべての情報を確認し、 Amazon Route 53 Domain Name Registration End User Agreement を承諾し Submit を押すと登録手続きが開始します。

登録手続きが開始後、通常5-15分後にドメインが使えるようになります。その時は Amazon Route 53 Hosted Zone が作られます。

**注意** AWS Route 53 Registrar でドメインを登録すると、最初から「Transfer lock」が無効の状態で登録します。当該AWSアカウントで使うことなく他のサービスに移管する場合はそのまま無効で移管作業をしてください。引き続きAWSで使う場合は、 **必ず** Transfer lock を有効にしてください。

### 登録連絡情報

| **項目**                     | 値                                 |
|----------------------------|-----------------------------------|
| **Contact type**           | Company                           |
| **Organization**           | Geolonia, Inc.                    |
| **First name**             | Takayuki                          |
| **Last name**              | Miyauchi                          |
| **Email**                  | dev@geolonia.com                  |
| **Phone number**           | +81 368244290                     |
| **Address 1**              | Dogenzaka 1-Chome, 10-8           |
| **Address 2**              | Shibuya Dogenzaka Tokyu Bldg 2F-C |
| **Country**                | Japan                             |
| **State / Province**       | Tokyo                             |
| **City**                   | Shibuya                           |
| **Zip code / Postal code** | 150-0043                          |
