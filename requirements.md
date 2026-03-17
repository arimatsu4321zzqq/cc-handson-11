# ポートフォリオサイト 要件定義書

## 1. プロジェクト概要

個人ポートフォリオサイトを静的SPA（Single Page Application）として構築する。
GitHub Pages にデプロイし、公開する。

---

## 2. 技術スタック

| 分類 | 技術 |
|------|------|
| フレームワーク | React 18 |
| ビルドツール | Vite |
| スタイリング | TailwindCSS v3 |
| 言語 | JavaScript (JSX) |
| ホスティング | GitHub Pages |
| デプロイ | gh-pages パッケージ または GitHub Actions |

---

## 3. 機能要件

### 3.1 ページ構成（セクション）

| セクション | 内容 |
|-----------|------|
| Hero | 氏名・キャッチコピー・CTA ボタン |
| About | 自己紹介・経歴・写真 |
| Skills | 技術スタック一覧（アイコン + レベル表示） |
| Projects | 制作物カード（サムネイル・概要・リンク） |
| Contact | 問い合わせフォーム or SNS リンク集 |

### 3.2 ナビゲーション

- 固定ヘッダー（スクロール時も表示）
- セクションへのスムーズスクロール
- モバイル用ハンバーガーメニュー

### 3.3 ダークモード

- OS設定に応じた自動切替（`prefers-color-scheme`）
- 手動トグルボタンによる切替
- 選択状態を `localStorage` に保存し、再訪時も維持

---

## 4. 非機能要件

### 4.1 レスポンシブデザイン（モバイルファースト）

| ブレークポイント | 幅 |
|----------------|-----|
| モバイル（デフォルト） | ~ 767px |
| タブレット（`md`） | 768px ~ 1023px |
| デスクトップ（`lg`） | 1024px ~ |

### 4.2 パフォーマンス

- Lighthouse スコア 90 点以上（Performance / Accessibility / Best Practices / SEO）
- 画像は WebP 形式を使用し、`loading="lazy"` を付与

### 4.3 アクセシビリティ

- セマンティックな HTML 要素を使用（`<header>`, `<main>`, `<section>`, `<footer>`）
- 画像には `alt` テキストを設定
- キーボードナビゲーション対応
- カラーコントラスト比 WCAG AA 準拠

### 4.4 SEO

- `<title>` および `<meta name="description">` を設定
- OGP タグ（Twitter Card / OG Protocol）を設定

---

## 5. ディレクトリ構成

```
/
├── public/
│   ├── favicon.ico
│   └── og-image.png
├── src/
│   ├── assets/         # 画像・アイコン等
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Header.jsx
│   │   │   └── Footer.jsx
│   │   └── sections/
│   │       ├── Hero.jsx
│   │       ├── About.jsx
│   │       ├── Skills.jsx
│   │       ├── Projects.jsx
│   │       └── Contact.jsx
│   ├── hooks/
│   │   └── useDarkMode.js   # ダークモード管理カスタムフック
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── index.html
├── vite.config.js
├── tailwind.config.js
├── postcss.config.js
└── package.json
```

---

## 6. デプロイ要件

### 6.1 GitHub Pages 設定

- リポジトリ: `<username>.github.io` または `<username>/portfolio`
- 公開ブランチ: `gh-pages`
- ベースパス: `vite.config.js` の `base` にリポジトリ名を設定

### 6.2 デプロイフロー

```
main ブランチへの push
  → GitHub Actions が起動
  → npm run build
  → dist/ を gh-pages ブランチへデプロイ
```

### 6.3 GitHub Actions ワークフロー（`.github/workflows/deploy.yml`）

- トリガー: `main` ブランチへの push
- Node.js バージョン: 20
- キャッシュ: npm キャッシュを利用

---

## 7. 開発環境セットアップ手順

```bash
# 依存パッケージのインストール
npm install

# 開発サーバー起動（http://localhost:5173）
npm run dev

# 本番ビルド
npm run build

# ビルド結果のプレビュー
npm run preview
```

---

## 8. 受け入れ条件

- [ ] 全セクション（Hero / About / Skills / Projects / Contact）が表示される
- [ ] モバイル・タブレット・デスクトップで崩れなく表示される
- [ ] ダークモードの自動切替・手動切替が動作する
- [ ] ハンバーガーメニューが開閉できる
- [ ] セクションへのスムーズスクロールが動作する
- [ ] `npm run build` がエラーなく完了する
- [ ] GitHub Pages で正常に公開される
