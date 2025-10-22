# フレームワーク

jekyll+tailwind で構築しています

# 編集方法

- 通常の更新は アンダーバー付きのディレクトリ（\_news や \_projects など）内のファイル編集で行います。
- 新しいニュースやプロジェクトを追加する際は、既存の Markdown ファイルをコピーして内容を書き換えてください。
- それらの内容は、ルート直下の news.markdown や projects.markdown から自動的に読み込まれます。
- docs/ フォルダ内はビルド後の出力先なので、直接編集しないでください。
- 画像などは assets/images フォルダに配置してください。
  わからないことがあれば soyhayatomx[at]gmail.com まで。

# 実行手順

1. Tailwind CSS のビルド

Tailwind をウォッチモードで起動し、CSS を自動コンパイルします。

npx @tailwindcss/cli \
 -i ./assets/css/tailwind.css \
 -o ./assets/css/tailwind-output.css \
 --watch

2. Jekyll のローカルサーバを起動

別のターミナルで以下を実行し、ローカル環境でサイトを確認します。

bundle exec jekyll serve

3. 静的サイトのビルド

内容に満足したら以下コマンドでビルドし、GitHub の main ブランチで push してください。

bundle exec jekyll build

# ファイル-フォルダ構成

├── \_config.yml
├── \_data/
├── \_includes/
├── \_layouts/
├── \_news/  
├── \_projects/  
├── assets/  
├── docs/  
├── 404.html
├── about.markdown
├── contact.markdown
├── index.markdown # トップページ
├── members.markdown
├── news.markdown
├── posts.markdown
├── projects.markdown
├── Gemfile
├── Gemfile.lock
├── package.json
├── package-lock.json
├── ReadMe
└── node_modules/

- **\_config.yml**  
  Jekyll のサイト全体設定ファイル。

- **\_data/**  
  構造化データを配置するディレクトリ。テンプレートから `site.data` で参照します。

  - `members.json` など

- **\_includes/**  
  ページ共通の部品を配置します。`{% include %}` で読み込み。

  - `header.html`, `footer.html`, `title.html`, `button.html` など

- **\_layouts/**  
  ページのレイアウトテンプレート。各ページの Front Matter の `layout` で指定。

  - `default.html` など

- **\_news/**  
  ニュース記事の Markdown を格納するコレクション／カテゴリー用ディレクトリ。

- **\_projects/**  
  プロジェクト記事の Markdown を格納するコレクション／カテゴリー用ディレクトリ。

- **assets/**  
  画像や CSS、JavaScript などの静的アセット。ビルド時にそのまま配信されます。  
  ※ Tailwind などのツールを使う場合は、この中にエントリ CSS/JS を置きます。

- **docs/**  
  ビルド後の静的サイト一式（GitHub Pages で「/docs」から配信する構成向け）。  
  GitHub Pages を docs 配下で運用する場合はこちらを公開対象にします。

- **index.markdown / about.markdown / contact.markdown / members.markdown / news.markdown / posts.markdown / projects.markdown**  
  各ページ本体（Markdown）。Front Matter でレイアウトやパスを指定します。

- **404.html**  
  404 エラーページ。

- **Gemfile / Gemfile.lock**  
  Ruby（Jekyll）関連の依存関係定義。

- **package.json / package-lock.json**  
  フロントエンド（ビルドツール等）の依存関係定義。

- **node_modules/**  
  npm 依存パッケージ（自動生成／大量のため通常は Git 管理対象外）。

- **ReadMe**  
  このリポジトリの説明（本ドキュメント）。

### 運用メモ

- **ビルド出力先**  
  通常 Jekyll の出力先は \_site/ ですが、本プロジェクトでは GitHub Pages に対応させるため、\_config.yml で destination: docs と指定し、docs/ に静的サイトを出力しています。これにより、\_site/ は通常は使用しません。
