# polymode.jp

株式会社Polymodeの公式ホームページリポジトリ

## 概要

このリポジトリは、GitHub Pagesでホスティングされる「polymode.jp」のソースコードです。
本サイトは **独立した2つの入り口** で構成されています。

- **`polymode.jp/`（メインサイト）** — 顧客向けコーポレートサイト。ハイテク感のあるダークテーマ。
- **`polymode.jp/ir/`（電子公告）** — 会社法に基づく電子公告専用ページ。法務文書風の簡素な独立デザインで、メインサイトとは相互リンクしません。

## サイト構成

```
polymode.jp/
├── index.html          # トップページ（顧客向け）
├── about.html          # 会社概要（顧客向け）
├── services.html       # 事業内容（顧客向け）
├── css/
│   └── style.css       # メインサイト用デザインシステム
└── ir/
    └── index.html      # 電子公告（独立ページ・inline style）
```

## デザイン特徴（メインサイト）

- **ダークベース**: 深みのある濃紺色（#0a0e27）をベースカラーに採用
- **アクセントカラー**: 水色（#73c3dc）から紫色（#a665ea）へのグラデーション
- **レスポンシブデザイン**: モバイル、タブレット、デスクトップに完全対応
- **アクセシビリティ**: セマンティックHTML、ARIAラベル、適切なコントラスト比
- **モダンUI**: グラスモーフィズム、スムーズアニメーション、ホバーエフェクト

IR ページはこのデザインシステムを使わず、白背景・サンセリフの法務文書スタイルで完結しています（`noindex` 指定）。

## 技術スタック

- HTML5
- CSS3（CSS Variables, Flexbox, Grid）
- Vanilla JavaScript（ES6+）
- Jekyll（GitHub Pages 標準）
- GitHub Pages

## ページ詳細

### トップページ（index.html）
- ヒーローセクション
- 事業概要カード
- 強み・特徴の紹介
- CTA（Call to Action）

### 会社概要（about.html）
- ミッション・ビジョン
- 会社情報テーブル
- 事業目的の詳細
- コアバリュー

### 事業内容（services.html）
- IT技術開発事業
- 投資・資産管理事業
- 不動産事業
- コンテンツ制作事業

### 電子公告（ir/index.html）
- 商号・代表者・本店所在地
- 決算公告テーブル（PDF へのリンク）
- メインサイトへの導線は持たない独立ページ

## ローカル開発

GitHub Pagesと同じ環境で確認するには、シンプルなHTTPサーバーを起動してください：

```bash
# Python 3の場合
python3 -m http.server 8000

# Node.jsのhttpサーバーの場合
npx http-server
```

その後、ブラウザで `http://localhost:8000` にアクセスします。

## デプロイ

mainブランチへのpushにより、GitHub Pagesが自動的に更新されます。

## ライセンス

© 2025 Polymode Inc. All rights reserved.
