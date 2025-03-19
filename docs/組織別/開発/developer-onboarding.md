# オンボーディング

## 共通
私たちは、新しく参加されるメンバーに以下の作業をお願いしています：

- 自己紹介の作成
  - Notionの[自己紹介ページ](https://www.notion.so/e90f93da63fe44c595b8f46d1e793eb3?v=8b4ea8bbed84474dba1fc07a5f47ed9b)にて
  - "New->自己紹介テンプレート"を使用してください

## 設定するアカウント・ソフト

私たちは以下のツールを使用しています

### Slack
主要なチャンネルとその用途：
- `#dev`: 開発部の基本的なやり取り
- `#dev-random`: 開発者専用の技術雑談
- `#esa-notifications`: esa記事の通知
- `#members-staff`: 社員専用の連絡
- `#members-all`: 社員＋業務委託メンバーの連絡
- `#member-status`: 日次の業務報告（Geekbotが自動で確認）
  - Geekbotへ「report」と送信することで、9時前でも報告可能
- その他、通知用・雑談用の各種チャンネル

### GitHub
設定手順：
1. アカウント名をSlackで登録
2. プロフィールの編集
3. 表示名とURLの設定
4. メールアドレスの登録

### その他のツール
- Notion: 社内ポータル、自己紹介などの情報サイト
- Esa: 議事録・共有・備忘録用の社内ブログ的ツール
- VS Code: GitHub連携でCopilotの利用や設定同期が可能

## 開発環境

私たちの開発環境について：

- 基本はnode.jsを使用
- `.tool-versions`ファイルでバージョン管理
- `asdf`によるバージョン管理を推奨

### 推奨インストールツール
- `xcode-select --install`（ビルドツール）
- homebrew
- asdf
- VS Code
- iTerm 2

## GitHubの組織構成

私たちは以下の組織で管理を行っています：

### 自社管理
- `geolonia`: メインの開発リポジトリ
- `geoloniamaps`: 地図スタイル管理

### 共同管理
- `unvt`: 国連ベクトルタイルツールキット
- `spatial-id`: 空間IDのSDK

### 顧客代行
- `takamatsu-city`

### リポジトリ命名規則
- 公開サイト: ドメイン名をそのまま使用（例：`blog.geolonia.com`）
- `-app`と`-api`のセット（例：`prop-id-api`と`prop-id-app`）
- インフラ管理： `infrastructure`
