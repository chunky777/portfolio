# index.html の変更を GitHub にコミットして公開URLを更新する

以下の手順を **コマンドプロンプト** または **PowerShell** で実行してください（Cursor のターミナルや、Windows の「cmd」でも可）。

---

## ⚠️ 「git は認識されません」と出る場合（Git のインストール）

**「'git' は、内部コマンドまたは外部コマンド…」** と出る場合は、PC に Git が入っていません。次の手順でインストールしてください。

### 1. Git for Windows をダウンロード

- ブラウザで **https://git-scm.com/download/win** を開く  
- ダウンロードが自動で始まります（64bit の「Click here to download」など）

### 2. インストールを実行

- ダウンロードした **Git-2.x.x-64-bit.exe** をダブルクリックして実行
- 基本的には **「Next」** のまま進めてOKです
- **「Adjusting your PATH environment」** の画面では、  
  **「Git from the command line and also from 3rd-party software」** を選ぶ（上から2番目。PATH に追加されるので、コマンドで `git` が使えるようになります）
- あとは **Next** → **Install** で完了

### 3. ターミナルを開き直す

- **いま開いているコマンドプロンプトや PowerShell は一度閉じてください**
- 新しく **コマンドプロンプト** または **PowerShell** を開く
- 次のコマンドでバージョンが表示されればOKです：

```bash
git --version
```

例: `git version 2.43.0.windows.1` のように出れば成功です。  
このあと、下の「パターンA」または「パターンB」の手順に進んでください。

---

## パターンA: すでにこのフォルダで GitHub と連携済みの場合

（以前に `git init` と `git remote add origin ...` を実行している場合）

```bash
cd "c:\Users\rikuT\Downloads\ポートフォリオ"

git add index.html
git add .
git commit -m "index.html を更新"
git push origin main
```

※ ブランチ名が `master` の場合は `git push origin master` にしてください。

---

## パターンB: まだ Git を初期化していない場合

### 1. GitHub でリポジトリを用意する

- https://github.com/new で新しいリポジトリを作成（例: 名前は `portfolio`）
- **「Add a README file」はチェックしない**（ローカルに既にファイルがあるため）
- 作成後、表示される **リポジトリのURL** をコピー（例: `https://github.com/あなたのユーザー名/portfolio.git`）

### 2. ローカルで Git を初期化してプッシュ

```bash
cd "c:\Users\rikuT\Downloads\ポートフォリオ"

git init
git add .
git commit -m "ポートフォリオ公開"
git branch -M main
git remote add origin https://github.com/あなたのユーザー名/portfolio.git
git push -u origin main
```

※ `あなたのユーザー名` と `portfolio` は、作成したリポジトリに合わせて書き換えてください。

### 3. GitHub Pages を有効にする（公開URLを出すため）

1. GitHub のリポジトリページで **Settings** → **Pages**
2. **Source** で「Deploy from a branch」を選択
3. **Branch** で `main`、フォルダで **/ (root)** を選んで **Save**
4. 数分後、次のURLで表示されます:  
   `https://あなたのユーザー名.github.io/portfolio/`

---

## 公開URLの画面を変えるには

**index.html を修正したあと、次の3つを実行すれば公開URLの内容が更新されます。**

```bash
cd "c:\Users\rikuT\Downloads\ポートフォリオ"

git add index.html
git commit -m "index.html を修正"
git push origin main
```

プッシュ後、GitHub Pages は自動で再デプロイされるので、**1〜2分待ってから** 公開URLを再読み込みすると変更が反映されています。

---

## うまくいかないとき

- **「git が認識されない」**  
  → このファイルの **一番上の「Git のインストール」** の手順に従って Git for Windows を入れ、**ターミナルを開き直してから** もう一度 `git init` などを実行してください。

- **「Permission denied」や「Authentication failed」**  
  → GitHub にログインし直す必要があります。  
  - コマンド: `git push origin main` のあと、ブラウザまたは「Sign in with your browser」で GitHub 認証を完了してください。  
  - または GitHub の **Settings** → **Developer settings** → **Personal access tokens** でトークンを作成し、パスワードの代わりにそのトークンを入力する方法もあります。

- **「remote origin already exists」**  
  → すでにリモートが追加されています。`git remote -v` でURLを確認し、そのまま `git add` → `git commit` → `git push origin main` を実行すれば大丈夫です。
