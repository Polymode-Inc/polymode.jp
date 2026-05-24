# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## コミュニケーションとワークフロー

- **会話は日本語で行うこと。** ユーザーとのやり取り、commit メッセージ、コード内コメントもすべて日本語に統一する。
- **push する前に必ずドキュメントの整合性を確認すること。** 何らかの変更を push する直前に、`CLAUDE.md` と `README.md` を見直し、現状の構造・方針と齟齬がないか検討する。差分が必要であれば修正を加え、`UPDATE: <更新内容>` という prefix を付けた commit を別途追加してから push する（実装の commit と doc 更新の commit は分ける）。
- commit メッセージの prefix は既存リポジトリの慣習に従う（`UPDATE:` / `FIX:` / 機能追加は prefix なしで簡潔に、など）。

## プロジェクト概要

株式会社Polymode（polymode.jp）のコーポレートサイト。Jekyll製の静的サイトで、GitHub Pagesから配信される（`CNAME` でカスタムドメイン設定）。`main` ブランチへの push で自動デプロイされる。

サイト・コード・コメント・コミットメッセージはすべて日本語。

## サイト構造（重要な前提）

このサイトには独立した2つの入り口がある。**両者は意図的に切り離されている** ので、どちらか一方を編集するときに他方への導線を足さないこと。

- **`polymode.jp/`（メインサイト）** — 顧客向け。他プラットフォームの会社紹介から流入する前提で、`index.html` / `about.html` / `services.html` の3ページ構成。共通の `_layouts/default.html` + ダークテーマで装飾。**IR への導線は持たない**（navbar・footer・CTA いずれにも IR リンクは置かない）。
- **`polymode.jp/ir/`（電子公告）** — 会社法上の電子公告専用。検索流入や宣伝対象ではない（`<meta name="robots" content="noindex">`）。`layout: null` でメインサイトのレイアウトを使わず、白背景・サンセリフの簡素な法務文書スタイルで完全に独立。メインサイトへの戻りリンクも持たない。連絡先は `site.contact.e_mail` のみ提示する。

## メインサイトのコンテンツ方針（重要な前提）

メインサイトは **「中小企業の AI 導入を一気通貫で支援する会社」** という単一のポジショニングで書かれている。"先進技術で何でもやります" 風の網羅型訴求は意図的に排除済み。文言を編集するときは以下の前提を崩さないこと。

- **顧客像**：業種不問、中小企業全般。"AI を使ってみたいが、社内に詳しい人材がいない" 状況の経営者・担当者が読者。
- **訴求軸**：診断 → PoC → 本番開発 → 運用伴走の **段階型** プロセス。「小さく試して、確かなものを大きく育てる」が共通フレーズ。
- **差別化メッセージ**：「既存システムを尊重し、業務に合わせて個別最適に AI を組み込む」。既製の AI SaaS を売る競合との区別ポイント。`index.html` / `services.html` / `about.html` に繰り返し登場するので、これらを薄めないこと。
- **専門領域**：LLM／AI エージェント／LLM を組み込んだ業務自動化。AI/LLM 以外の技術（汎用 Web 開発・クラウド・ブロックチェーン等）を services の前面に再度並べないこと（過去の網羅型訴求への逆戻り）。
- **価格表記のルール**：`index.html` / `services.html` に PoC 20万円〜・本番開発 80万〜500万円・運用 月額5万円〜 の **参考価格** が記載されている。価格を変更・追加する際は必ず「参考価格／要相談／個別お見積もり」のニュアンスを併記すること（ユーザーの明示要件）。
- **代表者の見せ方**：「現役学生」「22歳」など年齢・学生属性は前面に出さない方針（B2B フォーマル文脈での信頼維持）。**開始年（"2022年から" など）も明示しない**（経歴の薄さを連想させやすいため）。代わりに「早稲田大学」「LLM 開発に3年従事」のような年数ベースの記述で統一する。詳細は `about.html` の Representative セクションに集約。

## ローカル開発

GitHub Pages と同等の Jekyll ビルドで確認する場合:

```bash
bundle exec jekyll serve
```

Jekyll を入れずに静的ファイルだけ確認する場合（Liquid タグは未展開のまま表示される点に注意）:

```bash
python3 -m http.server 8000
# または
npx http-server
```

## アーキテクチャ

Jekyll の標準構成に従ったテンプレート駆動の静的サイト。

- **`_config.yml`** — サイト全体の設定と会社情報（`site.company.*`、`site.contact.*`）を一元管理。代表者名・住所・資本金などを変更する場合は必ずここを編集する（各 HTML にハードコードしない）。`ir/index.html` も Liquid 経由でここから値を引いている。
- **`_layouts/default.html`** — メインサイトの3ページ専用の外枠。`head` / `navbar` / `footer` を include した上で `{{ content }}` を差し込む。`ir/index.html` はこのレイアウトを使わない（`layout: null`）。
- **`_includes/`** — `head.html`（meta/CSS）、`navbar.html`（モバイルメニュー対応ナビ）、`footer.html`（サイトマップ + 年自動更新 + ナビ挙動の inline JS）。ナビゲーションのモバイルトグルとスクロール時の navbar 背景変更は `footer.html` 末尾のスクリプトで実装。
- **メインサイトのページ**（`index.html`, `about.html`, `services.html`）— front matter（`layout: default`, `title`, `description`）+ ボディ。`title` は head で `{{ page.title }} | Polymode Inc.` の形に整形される。
- **`ir/index.html`** — 完全独立の単一HTMLページ。`layout: null` を front matter に指定し、`<!doctype html>` から自前で書く。スタイルは外部 CSS を読まず inline `<style>` で完結（メインサイトのダークテーマ CSS Variables には依存しない）。
- **`css/style.css`** — メインサイト専用のデザインシステム CSS。冒頭の `:root` で定義された CSS Variables（`--color-*`, `--spacing-*`, `--shadow-*` 等）を使い回す前提。新しい色やスペーシングを足すときはハードコードせず変数を追加する。IR ページからは参照しない。

### コンテンツ編集時の注意

- **メインと IR を相互リンクしない**（[サイト構造](#サイト構造重要な前提) 参照）。ナビ／フッター／CTA に IR リンクを足さない。IR ページからメインへの戻りリンクも足さない。
- ナビ／フッターのリンクを増減する場合は `_includes/navbar.html` と `_includes/footer.html` の両方を更新する。
- ページ間リンクは Jekyll の `{{ site.baseurl }}` を前置すること（navbar/footer はこの方式）。
- 新しい決算公告 PDF を追加する際は、`ir/` 配下に PDF を置き、`ir/index.html` の `<tbody>` 内に行を追記する。
- `services.html` に書かれている事例（Case Studies）は **顧客名を伏せて業務軸で一般化** した記述。新事例を追加する際もこの粒度（業務カテゴリ＋作ったもの）を維持し、固有名詞は出さない。
