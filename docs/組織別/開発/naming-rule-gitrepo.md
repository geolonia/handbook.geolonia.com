# Git リポジトリ命名規則

このドキュメントでは、私たちのGit リポジトリ命名規則についてのガイドラインを説明します。

## 基本ルール

私たちは、以下の原則に従ってリポジトリの命名を行います。

1. **ケバブケースの使用**
   - 単語間はハイフン（-）で区切る
   - すべて小文字を使用する
   - 例：`coord-picker`、`area-app`

2. **シンプルな命名**
   - 不要な単語を省略する
   - 一般的な英単語を使用する
   - 略語は必要な場合のみ使用する（例：`csv`、`json`）

## プレフィックス規則

### 1. プロダクト関連

#### Mapbox GL関連 (`mbgl-`)
```
mbgl-export-control    # エクスポート機能の実装
mbgl-circle-marker     # 円形マーカーの実装
```

#### スマートシティ関連 (`smartcity-`)
```
smartcity-data-upload-template
smartcity-data-platform-upload-action
```

### 2. 地域関連

#### 特定都市向け
```
takamatsu-*  # 高松市関連の実装
```

### 3. データ種類関連

#### 日本のデータ (`japanese-`)
```
japanese-addresses     # 住所データの実装
japanese-prefectures   # 都道府県データの実装
```

#### データセット (`data-`)
```
data-jp-railroads    # 日本の鉄道データ
data-png-tools       # PNG関連ツール
```

## サフィックス規則

### 1. ツール関連 (`-tool`)
```
gsi-mbtiles-tool     # 地理院タイル変換ツール
pmtiles_tool         # PMTiles操作ツール
mbtiles_tool         # MBTiles操作ツール
```

### 2. GitHub Actions (`-action`)
```
excel-to-csv-action           # Excel→CSV変換
convert-to-geojson-action     # GeoJSON変換
```

## ドメイン名規則

### 1. Geoloniaドメイン
```
*.geolonia.com
例：
- maps.geolonia.com
- cdn.geolonia.com
```

### 2. TileCloudドメイン
```
*.tilecloud.io
例：
- geojson.tilecloud.io
```

## ベストプラクティス

私たちは、以下の点に注意してリポジトリの命名を行います。

1. **一貫性の維持**
   - 同じカテゴリには同じプレフィックス/サフィックスを使用する
   - 既存の命名パターンを踏襲する

2. **明確な目的の表現**
   - リポジトリ名から主な機能や目的を推測できるようにする
   - 汎用的すぎる名前を避ける

3. **検索性への配慮**
   - 関連するリポジトリが検索で見つけやすい命名を行う
   - カテゴリごとに一貫したプレフィックスを使用する

## 非推奨パターン

私たちは、以下のような命名を避けます：

- 大文字の使用（`MyRepo`）
- アンダースコアの使用（`my_repo`）
- 過度に短い略語（`rd`ではなく`road`を使用）
- 一般的でない略語の使用
- スペースや特殊文字の使用

## 例外的なケース

以下の場合は、標準的な命名規則から外れることを許容します：

1. **外部システムとの連携**
   - 外部システムの命名規則に合わせる必要がある場合
   - 例：`AWS-*`、`GCP-*`

2. **歴史的な理由**
   - 既存の広く使用されている名前を継続使用する場合
   - 互換性維持が必要な場合