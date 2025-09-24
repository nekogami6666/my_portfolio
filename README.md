# ポートフォリオサイト（静的サイト）

個人のポートフォリオを公開するための静的サイト一式です。  
HTML / CSS（Sass）で実装し、BEMベースのクラス設計とレスポンシブ対応（モバイル・タブレット・PC）を行っています。

> 本リポジトリには完成版（`complete/`）と作業版（ルート直下）が含まれます。GitHub公開時は通常、ルート直下の `index.html` 等を使用します。

---

## 主な機能

- **レスポンシブ対応**：ブレークポイントを `sass/_breakpoints.scss` で集中管理  
- **BEM設計**：`block__element--modifier` の命名で保守性を担保  
- **ハンバーガー / ドロワーナビ**：`#js-button-drawer` と `#js-drawer`  
  - `js/index.js` は jQuery 依存（CDN を `<script>` で読み込み必要）  
- **OGP / X(Twitter) カード**：`<meta property="og:*">` / `<meta name="twitter:*">`  
- **画像最適化**：PC / SP ディレクトリを分離（`img/` / `img/sp/`）  
- **リセットCSS**：`css/reset.css` を同梱  
- **SEO制御**：ドラフト環境では `meta name="robots" content="noindex"` を付与

---

## 技術スタック

- HTML5 / CSS3（Sass: SCSS 記法）
- JavaScript（jQuery 3.x 依存のスクリプトあり）
- Google Fonts（Noto Sans JP / Oswald）

---

## ディレクトリ構成

```
portfolio/
├── index.html
├── css/
│   ├── reset.css
│   └── style.css
├── js/
│   └── index.js            # ハンバーガー開閉（jQuery想定）
├── sass/
│   ├── style.scss          # エントリポイント
│   ├── _breakpoints.scss   # 画面幅などの定義
│   └── _color.scss         # カラーパレット
├── img/                    # PC向け画像
│   └── sp/                 # SP向け画像
├── complete/               # 完成版一式（参考）
└── LICENSE.txt
```

---

## ローカル起動

1. リポジトリをクローン  
   ```bash
   git clone <YOUR_REPO_URL>.git
   cd <YOUR_REPO_NAME>/portfolio
   ```

2. 任意の静的サーバで起動（例：`python`）  
   ```bash
   # Python 3.x
   python -m http.server 8000
   # → http://localhost:8000 にアクセス
   ```

> そのまま `index.html` をブラウザで開いても表示できますが、相対パスの検証にはローカルサーバを推奨します。

---

## Sass のビルド

本リポジトリは `css/style.css` をコミット済みですが、スタイル修正時は Sass を再ビルドしてください。

### 1) Dart Sass（推奨）
```bash
# グローバル導入
npm i -g sass
# ウォッチして自動ビルド
cd portfolio
sass --watch sass/style.scss css/style.css
```

### 2) Node プロジェクトで使う場合
```bash
# 例: プロジェクト直下に package.json を作成
npm init -y
npm i -D sass
# package.json に追加
# "scripts": { "dev:css": "sass --watch portfolio/sass/style.scss portfolio/css/style.css" }
npm run dev:css
```

---

## jQuery 読み込み（必要な場合）

`js/index.js` は `$` を使用しているため jQuery を読み込む必要があります。  
`</body>` 直前などで CDN を読み込んでください。

```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js" integrity="sha256-/JqT3SQfawRcv/BIHPThkBvs0OEvtFFmqPF/lYI/Cxo=" crossorigin="anonymous"></script>
<script src="./js/index.js"></script>
```

> もし jQuery に依存させたくない場合は、`index.js` をネイティブJSに書き換えてください。

---

## デプロイ（GitHub Pages）

1. `portfolio/` 配下をリポジトリのルートに置く（`index.html` がルートに来る構成にすると簡単）  
2. リポジトリ設定 → **Pages** → **Source** を `Deploy from a branch` に設定  
3. ブランチ: `main`、フォルダ: `/ (root)` を選択 → 保存  
4. 数分後、`https://<USERNAME>.github.io/<REPO>/` で公開されます

> 既存の構成のまま公開したい場合は、ビルド成果物を `docs/` へコピーし、Pages のフォルダを `docs` に変更してください。

---

## カスタマイズのポイント

- **色とフォント**：`sass/_color.scss` と Google Fonts の `link` を調整  
- **ブレークポイント**：`sass/_breakpoints.scss` を編集  
- **OGP画像**：`img/ogp.png` など任意のパスを用意し、`<meta property="og:image">` を差し替え  
- **セクション構成**：`index.html` の `#service`, `#about`, `#works`, `#flow`, `#contact` を必要に応じて編集

---

## ライセンス / クレジット

- 画像・アイコン等の権利は各著作権者に帰属します  
- `LICENSE.txt` に記載のとおり、一部コンポーネントは MIT / OFL 等のライセンスに基づき使用しています  
- 本テンプレート自体のライセンスは、特に指定がなければ MIT としてください（必要に応じて変更可）

---

## よくある質問

- **Q. スマホでメニューが開かない**  
  A. jQuery の読み込み順を確認してください（`jquery.min.js` → `js/index.js`）。

- **Q. 検索にヒットしない**  
  A. 開発用の `noindex` が残っている可能性があります。`<meta name="robots" content="noindex">` を削除してください。

- **Q. 画像がぼやける**  
  A. `img/` と `img/sp/` を端末幅で出し分けるか、適切な解像度へ差し替えてください。`srcset` の導入も有効です。

---

## 作者

- Okumura / cat-programmer.com（仮）  
  連絡先は `#contact` セクション、または GitHub Issues からどうぞ。
