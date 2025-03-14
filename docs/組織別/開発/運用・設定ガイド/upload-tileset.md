# 配信用タイルセットのアップロード

Geolonia では管理者によるタイルセットを配信する基盤もあります。

Geolonia でタイルを配信する基盤は `tileserver.geolonia.com` (dev環境は `tileserver-dev.geolonia.com` ) から配信します。

タイルをアップロードする場合、 [`geolonia-admin`](https://github.com/geolonia/geolonia-admin) のCLIツールを使います。

## 事前準備

1. nodejs 環境整備
  Geolonia では [asdf](https://github.com/asdf-vm/asdf) を使ってnodejsバージョンを管理しているプロジェクトが多いので、おすすめします。
1. AWS 認証設定
    `geolonia-admin` は AWS の API を利用して動きますので、AWSのアクセスが必要となります。[AWSアカウント運用](/組織別/開発/aws-account-policy.html) を確認ください。

    認証がうまく行っているかを確認するために、 `aws sts get-caller-identity` を利用してください。もし成功している場合は、下記のような出力になります。

    ```
    $ aws sts get-caller-identity
    {
        "UserId": "...",
        "Account": "76XXXXXXXXX",
        "Arn": "arn:aws:sts::76XXXXXXXXX:assumed-role/AWSReservedSSO_..."
    }
    ```

    AWS SSO の認証情報が期限付き認証情報なので、切れた場合は `aws sso login` で再ログインしてください。
1. `go-pmtiles` のインストール **任意: 下記の注意を確認してください**
  [リリースページ](https://github.com/protomaps/go-pmtiles/releases) から対象OS・CPUのバイナリをダウンロードし、PATHにインストールしてください。mbtilesを指定した場合は、アップロード前にpmtilesに変換するために利用します。すでにpmtilesになっているファイルをアップロードする場合は不要です。
1. geolonia-adminのインストール
  [geolonia-admin](https://github.com/geolonia/geolonia-admin) の README に書かれている導入方法を確認してください。

## アップロード手順

`v1` 環境（本番環境）にアップロードする場合は下記となります。開発環境（ `tileserver-dev.geolonia.com` ）にアップロードする場合は、 `v1` を `dev` と置き換えてください。

**注意**: すでにアップロード先のタイルセット名が使われている場合は上書き保存されます。すでに使われているかを確認するために、 `geolonia-admin pmtiles list v1`  を実行してください。タイルセット名は `alias` 列と相当します。

1. mbtiles/pmtilesファイルを用意する  0️⃣
1. アップロード先のタイルセット名を確認する 1️⃣
1. `geolonia-admin pmtiles deploy 0️⃣ v1 1️⃣`

## 正しくアップロードされたか確認する
```curl -H "Origin: http://localhost:3000" "https://tileserver.geolonia.com/タイルセット名/tiles.json?key=YOUR-API-KEY"```

開発環境の場合は、`tileserver-dev.geolonia.com`

## タイルセットのダウンロード
以下でアップロードしたタイルセットのダウンロードができます。

```geolonia-admin pmtiles download v1 タイルセット名 output.pmtiles```
