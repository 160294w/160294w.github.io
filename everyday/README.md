# Jekyll GitHub Pages サイト

Minimal MistakesテーマとGitHub Pagesを使用したモダンなJekyllブログです。GitHub Pages互換の開発環境とDockerサポートを備えています。

## ✨ 特徴

- **モダンなテーマ**: レスポンシブデザインの美しいMinimal Mistakesテーマ
- **GitHub Pages互換**: シームレスなデプロイのための完全環境マッチング
- **Docker開発**: 一貫した開発のための複数のDockerオプション
- **日本語コンテンツ**: 日常生活をテーマにした日本語ブログ記事のサンプル
- **自動ビルドシステム**: カラーコード出力付きの包括的Makefile
- **ライブリロード**: 開発中のブラウザ自動更新

## 🚀 クイックスタート

### オプション1: GitHub Pages互換（推奨）
```bash
make github-pages-serve
```

### オプション2: ローカル開発
```bash
make serve
```

### オプション3: Docker開発
```bash
make serve-docker
```

サイトは [http://localhost:4000](http://localhost:4000) で利用できます

## 📁 プロジェクト構造

```
.
├── _config.yml                    # Jekyll設定
├── _posts/                        # ブログ記事
│   ├── 2025-07-24-welcome-to-jekyll.markdown
│   ├── 2025-07-25-morning-coffee-thoughts.markdown
│   ├── 2025-07-26-weekend-reading.markdown
│   ├── 2025-07-27-exploring-new-places.markdown
│   ├── 2025-07-28-monday-motivation.markdown
│   ├── 2025-07-29-cooking-experiment.markdown
│   ├── 2025-07-30-digital-detox.markdown
│   ├── 2025-07-31-monthly-reflection.markdown
│   └── 2025-08-01-new-month-new-goals.markdown
├── about.markdown                 # Aboutページ
├── hobby.md                       # 趣味ページ
├── index.markdown                 # ホームページ
├── 404.html                       # カスタム404ページ
├── Gemfile                        # Ruby依存関係
├── Makefile                       # ビルド自動化
├── Dockerfile                     # カスタムDockerイメージ
├── Dockerfile.github-pages        # GitHub Pages互換Docker
├── docker-compose.yml             # Docker Compose設定
├── docker-compose.github-pages.yml # GitHub Pages Docker Compose
├── CLAUDE.md                      # 開発ガイダンス
└── README.md                      # このファイル
```

## 🛠️ 開発コマンド

### クイックリファレンス

| コマンド | 説明 |
|---------|-------------|
| `make help` | 利用可能なコマンドをすべて表示 |
| `make github-pages-serve` | **推奨**: GitHub Pages互換環境 |
| `make serve` | ローカル開発サーバー |
| `make build` | サイトをローカルビルド |
| `make clean` | 生成されたファイルをクリーン |
| `make test` | サイトビルドをテスト |

### ローカル開発
```bash
# 依存関係をインストール
make install

# 開発サーバーを開始
make serve

# サイトをビルド
make build

# 生成されたファイルをクリーン
make clean

# ビルドをテスト
make test
```

### GitHub Pages開発（推奨）
```bash
# GitHub Pages互換Dockerイメージをビルド
make github-pages-build

# 完全なGitHub Pages環境でサーバーを開始
make github-pages-serve

# Docker Composeを使用
make github-pages-up
make github-pages-down

# GitHub Pages環境でシェルを開く
make github-pages-shell
```

### Docker開発
```bash
# カスタムDockerイメージでビルド・サーブ
make serve-docker

# 公式Jekyllイメージでクイックサーブ
make quick-serve

# Docker Compose
make compose-up
make compose-down

# Dockerでサイトをビルド
make build-docker

# Dockerシェルを開く
make docker-shell
```

### ショートカット
```bash
make dev                # = make serve
make docker-dev         # = make serve-docker
make compose-dev        # = make compose-up
make github-pages-dev   # = make github-pages-serve
```

## 🐳 Docker環境

### 1. GitHub Pages互換（推奨）
- **Ruby**: 3.3.4
- **Jekyll**: 3.10.0
- **依存関係**: GitHub Pagesと完全マッチ
- **使用方法**: `make github-pages-serve`

### 2. カスタムDocker
- **Ruby**: 3.3.4
- **Jekyll**: 最新互換版
- **使用方法**: `make serve-docker`

### 3. 公式Jekyllイメージ
- **Jekyll**: 4.x
- **高速セットアップ**: ビルド不要
- **使用方法**: `make quick-serve`

## 📝 コンテンツ管理

### ブログ記事の作成

`_posts/`に以下のファイル名形式で新しい記事を作成: `YYYY-MM-DD-title.markdown`

```yaml
---
layout: single
title: "記事のタイトル"
date: 2025-MM-DD HH:MM:SS +0900
categories: カテゴリ1 カテゴリ2
author_profile: true
---

ここにコンテンツを書きます...
```

### ページの作成

ルートディレクトリに新しいページを作成:

```yaml
---
layout: single
title: "ページタイトル"
permalink: /page-url/
author_profile: true
---

ページのコンテンツ...
```

## 🎨 テーマ設定

このサイトは[Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/)テーマを使用しています:

- **リモートテーマ**: `mmistakes/minimal-mistakes@4.26.2`
- **著者プロフィール**: すべてのページで有効
- **ソーシャルメディア**: `_config.yml`で設定
- **ナビゲーション**: 自動記事リスト
- **SEO**: 内蔵最適化

### テーマのカスタマイズ

`_config.yml`を編集してカスタマイズ:
- サイトタイトルと説明
- 著者情報
- ソーシャルメディアリンク
- ナビゲーション
- テーマ設定

## 🌐 デプロイ

### GitHub Pages（自動）
1. `gh-pages`ブランチに変更をプッシュ
2. GitHubが自動的にビルド・デプロイ
3. GitHub Pages URLでサイトが利用可能

### 手動デプロイ
```bash
# 本番用ビルド
make build

# `_site`ディレクトリにビルド済みサイトが含まれます
```

## 📊 GitHub Pages互換性

このプロジェクトは完全なGitHub Pages互換性のために設定されています:

- **Jekyllバージョン**: 3.10.0（GitHub Pagesと一致）
- **Rubyバージョン**: 3.3.4（GitHub Pagesと一致）
- **プラグイン**: GitHub Pages承認済みプラグインのみ
- **依存関係**: `github-pages` gemによる完全バージョンマッチング

## 🔧 要件

### ローカル開発
- Ruby 3.3.4または互換バージョン
- Bundler gem
- Git

### Docker開発
- Docker Desktop
- Docker Compose（オプション）

### 検証
```bash
make validate        # 環境チェック
make check-docker    # Dockerが動作しているか確認
make check-compose   # Docker Composeを確認
```

## 📚 サンプルコンテンツ

サイトには日本語のサンプルブログ記事が含まれています:

1. **朝のコーヒーと思考** - 朝の習慣について
2. **週末の読書時間** - 読書の習慣と効果
3. **新しい場所の探索** - 探索と発見の喜び
4. **月曜日のモチベーション** - 週始めの目標設定
5. **料理実験の日** - 新しいレシピへの挑戦
6. **デジタルデトックスの効果** - デジタル機器から離れる時間
7. **7月の振り返り** - 月末の振り返り
8. **8月の新しい目標** - 新月の目標設定

## 🔍 トラブルシューティング

### よくある問題

1. **Dockerが動作していない**
   ```bash
   make check-docker
   ```

2. **Bundleの問題**
   ```bash
   make clean
   make install
   ```

3. **テーマが読み込まれない**
   - インターネット接続を確認（リモートテーマ）
   - 一貫した環境のため`make github-pages-serve`を使用

4. **ポートが既に使用中**
   - 他のJekyllプロセスを停止
   - またはMakefileでポートを変更

### ヘルプの取得

- すべてのコマンドは`make help`で確認
- 開発ガイダンスは`CLAUDE.md`を確認
- `make validate`で環境を検証

## 🤝 貢献

1. リポジトリをフォーク
2. 機能ブランチを作成
3. 変更を行う
4. `make github-pages-serve`でローカルテスト
5. プルリクエストを送信

## 📄 ライセンス

このプロジェクトはオープンソースです。ライセンスの詳細はリポジトリを確認してください。

## 🔗 リンク

- [Jekyll ドキュメント](https://jekyllrb.com/docs/)
- [Minimal Mistakes テーマ](https://mmistakes.github.io/minimal-mistakes/)
- [GitHub Pages ドキュメント](https://pages.github.com/)
- [GitHub Pages バージョン](https://pages.github.com/versions/)

---

**Jekyll、Minimal Mistakes、Dockerで❤️を込めて構築**