# 開発用PC&データ取扱ルール

私たちは社用PC制度を設けていますが、各自の責任で適切に管理することをお願いしています。

現在私たちの開発者が使用しているPCは基本的に macOS (Apple) と Linux (クラウド又はPC) なので、この2つのOSを前提としたルールを定めています。

## データ扱いルール

- 危険なデータは基本的にローカルのマシンで扱わないこと
  - 例：案件ごとに作業用EC2を建ててそこで作業し、案件終了後はインスタンスとデータ丸ごと消去する

- 「危険なデータ」には以下が含まれます
  - 個人情報。個人を特定できる情報の組み合わせ
    - 住所と名前の組み合わせ
    - 位置情報と人物が紐づくようなデータ など
  - NDA（秘密保持契約）で結ばれている指定データ

- ローカルマシンで扱う場合は、確実な削除を確認し、削除日を記録すること

## PC自体の物理ルール

- 専有であること
  - 家族や他人がパソコンを触ったり、使用したりしないこと

- 安全な場所に保管すること
  - 自宅は基本的に問題なし
  - コワーキングスペースの荷物スペースのロッカーは鍵があってもNG
    - マスターキーやピッキングなどのリスクが高いため

- 外出での作業時は特に注意
  - パソコンは置いたままにしない
  - 後方からの覗き見に注意
  - 公共交通機関での使用時は特に注意

## OS設定などのルール

- 常に最新のバージョンを保持
- 記憶媒体の常時暗号化（Full Disk Encryption）
  - macOS: FileVaultを有効化
  - Linux: LVM & LUKSによる暗号化

- 画面ロックの設定
  - 不使用時は画面ロックし認証を要求
  - 10分以内の自動画面ロック

- パスワード要件
  - 10文字以上、記号と数字を含む
  - 他のサービスとの非共有
  - 本人のみが知るもの

- バックアップの暗号化
- マルウェア対策
  - macOS: XProtect
  - Linux: clamav等
  - 定義ファイルの定期更新（週1回以上）

## 利用にあたってのルール

- フリーWiFiや不明なネットワークへの接続禁止

- 以下のソフトウェアの利用禁止
  - 不特定多数の機器間でのファイル共有ソフト（P2P）
    - ただし安全性確認済み（SHA256以上のハッシュ値一致等）は可
  - 作成元不明・不審なベンダーのソフト
  - 非正規ライセンスのソフト

## 処分について

- 暗号化された記憶媒体
  - 処分前に完全消去（データの0での上書き等）

- 暗号化されていない記憶媒体
  - 物理的破壊
  - 複数回の0またはランダムデータでの上書き消去

参考: Linuxの Live CDを用いた記憶媒体の消去
- SSD: hdparmコマンド
- HDD: shredコマンドまたはddコマンド
  - SSDへのshred/dd使用は寿命を縮める可能性あり

不明点は社内のLinuxユーザーに相談してください。