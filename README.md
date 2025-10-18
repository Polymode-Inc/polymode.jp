# polymode.jp

株式会社Polymodeの公式ホームページリポジトリ

## 概要

このリポジトリは、GitHub Pagesでホスティングされる「polymode.jp」のソースコードです。
IT技術開発を中心とした事業を展開する株式会社Polymodeのコーポレートサイトとして、
ハイテク感のあるダークテーマデザインで構成されています。

## サイト構成

```
polymode.jp/
├── index.html          # トップページ
├── about.html          # 会社概要
├── services.html       # 事業内容
├── css/
│   └── style.css       # 共通デザインシステム
└── ir/
    └── index.html      # IR情報・電子公告
```

## デザイン特徴

- **ダークベース**: 深みのある濃紺色（#0a0e27）をベースカラーに採用
- **アクセントカラー**: 水色（#73c3dc）から紫色（#a665ea）へのグラデーション
- **レスポンシブデザイン**: モバイル、タブレット、デスクトップに完全対応
- **アクセシビリティ**: セマンティックHTML、ARIAラベル、適切なコントラスト比
- **モダンUI**: グラスモーフィズム、スムーズアニメーション、ホバーエフェクト

## 技術スタック

- HTML5
- CSS3（CSS Variables, Flexbox, Grid）
- Vanilla JavaScript（ES6+）
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

### IR情報（ir/index.html）
- 電子公告
- 決算公告テーブル
- IR関連情報

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
