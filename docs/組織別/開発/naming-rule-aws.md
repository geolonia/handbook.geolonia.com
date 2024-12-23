# AWS アカウント命名規則とOrganization管理

私たちは、AWSアカウントの管理を効率的に行うため、以下の命名規則とOrganization構造に従います。

## AWS Organization構造

### 管理アカウント
- アカウント名: `geolonia-rootacct`
- メールアドレス形式: `dev+rootacct@geolonia.com`
- 特徴：
  - OrganizationのRoot権限を持つアカウント
  - 請求の一元管理
  - セキュリティ上の理由から、日常的な運用では使用しない

### メンバーアカウント
すべてのプロジェクトアカウントとサンドボックスアカウントは、管理アカウントの配下に所属します。

## アカウント名の基本ルール

1. **プレフィックス規則**
   - `geolonia-`: 組織の正式なプロジェクト用
   - `sandbox-`: 個人の開発・検証用

2. **環境識別子**
   - `dev`: 開発環境
   - `v1`: プロダクション環境 バージョン1
   - `lab`: 実験環境

## カテゴリ別の命名規則

### 1. プロジェクトアカウント
形式：`geolonia-[プロジェクト名][-環境]`
```
例：
- geolonia-mlit-lab
- geolonia-takamatsu-project
- geolonia-gsijapan-project
```

### 2. サンドボックスアカウント
形式：`sandbox-[ユーザー名]`
```
例：
- sandbox-naoki
- sandbox-k.arai
- sandbox-himawari.chiba
```

### 3. プロダクトアカウント
形式：`[プロダクト名][-バージョン/環境]`
```
例：
- Geolonia Maps for SmartCity (V1)
- Geolonia Maps for SmartCity (Dev)
- Geolonia Geocoding (V1)
```

## メールアドレスの命名規則

### 1. 管理アカウント用
```
dev+rootacct@geolonia.com
```

### 2. プロジェクトアカウント用
```
dev+[プロジェクト識別子]@geolonia.com
例：
- dev+smartcity-v1@geolonia.com
- dev+geocoding-dev@geolonia.com
```

### 3. サンドボックスアカウント用
```
dev+aws_sandbox-[ユーザー名]@geolonia.com
```

## アカウント作成・管理ポリシー

1. **アカウント作成の申請**
   - 新規アカウントの作成は管理者に申請
   - 目的、用途、期間を明確にする
   - 適切な命名規則に従っているか確認

2. **セキュリティ設定**
   - MFAの有効化を必須とする
   - Root認証情報は厳重に管理
   - アカウント作成直後にセキュリティ設定を実施

3. **定期的なレビュー**
   - 不要なアカウントの特定
   - 使用状況の確認
   - コスト管理の実施

## 推奨プラクティス

1. **一貫性の維持**
   - プロジェクト内で統一された命名規則を使用
   - 既存のパターンを踏襲

2. **明確な目的の表現**
   - アカウントの用途が名前から推測可能
   - 環境が明確に区別可能


## 非推奨パターン


- スペースの使用（ハイフンを使用）
- 大文字と小文字の混在（特別な理由がある場合を除く）
- プロジェクト種別が不明確な命名
- 一般的でない略語の使用