# Nullvoida

WordPressの最新仕様に準拠した、開発者向け・最小構成のフルサイト編集（FSE / Full Site Editing）対応オリジナルブロックテーマです。

余分な装飾やレガシーなPHPコードを削ぎ落とし、Gutenbergのブロックマークアップ構文と `theme.json`（version 3）による厳密なデザイントークン設計を主軸に構築されています。

---

## 特徴

- **Pure Block Theme**: PHPテンプレート（`index.php` 等）を必要とせず、完全なGutenbergブロックHTMLと `theme.json` でレンダリング。
- **Theme.json Version 3**: WordPress 6.6 / 6.7 以降の最新仕様に準拠したデザイントークン定義。
- **Developer-focused Minimal Dark Mode**:
  - 深いチャコールブラック（Base: `#0d0f12`）とハイコントラストな本文色（Contrast: `#f3f4f6`）。
  - エッジの効いたアクセントカラー（Primary: `#00f0ff`）。
  - 等幅フォント（Monospace）とシステム・サンセリフのタイポグラフィ構成。
- **ホスト環境を汚さない開発基盤**: `@wordpress/env`（Dockerコンテナ）を活用し、PC本体にWordPressやMySQLを直接インストールすることなくワンコマンドで開発・破棄が可能。WSL2からの利用にも完全対応。

---

## ディレクトリ構造

```text
nullvoida/
├── .gitignore          # 依存関係、OS生成ファイル、一時キャッシュ等の除外定義
├── .wp-env.json        # @wordpress/env 開発用Dockerコンテナ設定
├── README.md           # プロジェクト説明書（本ファイル）
├── style.css           # テーマメタデータヘッダー定義
├── theme.json          # デザイントークン（カラー、フォント、余白、スタイル）定義 (v3)
└── templates/
    └── index.html      # FSE基本テンプレート（ブログ一覧レイアウト）
```

---

## 開発環境の起動と管理（npm scripts）

本プロジェクトには、ホスト（Windows）および WSL2 の双方から統一して操作できるよう `package.json` を用意しています。

```bash
# 起動
npm run start

# テーマ「Nullvoida」の有効化
npm run activate

# 一時停止
npm run stop

# 完全削除（Dockerボリュームを含めてリセット）
npm run destroy
```

---

## 2つの起動方式

### 方式 A: ホスト側（Windows）で起動する（推奨・セッション切れなし）
Windowsホスト側でターミナル（PowerShell等）を閉じてもバックグラウンドで起動し続けたい場合は、ホスト側に **Docker Desktop**（WSL2バックエンド）を導入して起動します。

1. Docker Desktop を起動
2. リポジトリ直下の PowerShell で以下を実行：
   ```powershell
   npm run start
   npm run activate
   ```
- **メリット**: セッションやVS Codeを閉じてもコンテナが落ちず、最も安定して常駐稼働します。

---

### 方式 B: ホストを汚さず WSL2 ネイティブで起動する
Windows側にDocker Desktopをインストールせず、WSL2（Arch Linux）内のDockerデーモンのみで完結させる軽量方式です。

1. WSL2ターミナルを開く（※WSL2はすべてのターミナルを閉じると自動休止するため、作業中はターミナルを開いたままにしてください）
2. プロジェクトディレクトリで起動：
   ```bash
   cd /mnt/c/Users/user/repos/nullvoida
   npm run start
   npm run activate
   ```
- **メリット**: Windowsホスト側が一切汚れず、メモリ消費が極めて軽量です。

---

## テーマの拡張指針

今後さらにテンプレートを拡充する場合は、以下の構造でファイルを追加してください：

- **テンプレートパーツの分割**:
  - `parts/header.html`
  - `parts/footer.html`
- **個別ページ・投稿テンプレート**:
  - `templates/single.html`（個別投稿ページ）
  - `templates/page.html`（固定ページ）
  - `templates/404.html`（Not Foundページ）
- **パターン（Patterns）**:
  - `patterns/` 配下にブロックパターンを定義可能。

---

## ライセンス

GPL-2.0-or-later
