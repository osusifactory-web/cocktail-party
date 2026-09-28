# Cocktail Party 公式Web説明書

GitHub Pages 用の静的サイトです。

## ファイル構成

- `index.html`：ページ本体
- `assets/css/style.css`：デザインCSS
- `assets/img/`：メインビジュアル・説明書画像・動画サムネイル
- `assets/video/`：圧縮済みルール動画
- `.nojekyll`：GitHub Pagesでそのまま配信するための空ファイル

## 更新方法

1. GitHubの該当リポジトリを開く
2. `cocktail-party` フォルダの中身をこのフォルダの内容で置き換える
3. `index.html` と `assets` フォルダをアップロード
4. 反映後、以下にアクセスして確認
   `https://osusifactory-web.github.io/cocktail-party/`

## 注意

元動画は100MB超でしたが、GitHubに置きやすいように720pで圧縮しています。
画質を優先する場合は、YouTube限定公開などにアップし、`index.html` の video タグを iframe に差し替えるのがおすすめです。
