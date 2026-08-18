# セットアップ手順

## 1. GitHubにリポジトリを作る

github.com → 右上の「+」→ New repository

- Repository name: 推測されにくい名前にする（例 `20261003trip`）
- **Public** を選ぶ（無料でPagesを使うために必要）
- 他は空のままで Create repository

## 2. このフォルダをアップロードする

ターミナルでこのフォルダを開いて、以下を順に実行する。
`yuto123456gj` と `20261003trip` は自分のアカウント名・リポジトリ名に置き換える。

```bash
cd ~/Desktop/サプライズ
git init
git add .
git commit -m "しおり公開"
git branch -M main
git remote add origin https://github.com/yuto123456gj/20261003trip.git
git push -u origin main
```

## 3. GitHub Pages を有効にする

リポジトリ → Settings → Pages

- Source: `Deploy from a branch`
- Branch: `main` / `/ (root)` → Save

1〜2分で以下のURLが公開される。**これをQRコードにする。**

```
https://yuto123456gj.github.io/20261003trip/
```

## 4. 写真アップロード用のトークンを作る

github.com → 右上のアイコン → Settings → Developer settings
→ Personal access tokens → **Fine-grained tokens** → Generate new token

- Token name: 何でもよい（例 `photo-upload`）
- Expiration: 期限（1年など。切れたら作り直す）
- Repository access: **Only select repositories** → 作ったリポジトリだけを選ぶ
- Permissions → Repository permissions → **Contents** を `Read and write` にする
- Generate token → 表示された `github_pat_…` をコピー（この画面を閉じると二度と見られない）

## 5. アップロードページにトークンを登録する

スマホで以下を開く。

```
https://yuto123456gj.github.io/20261003trip/upload.html
```

トークンを貼り付けて「保存する」を押すだけ。以後この端末では、
写真を選ぶだけでアップロードできる。トークンはその端末のブラウザ内にのみ保存され、
公開ファイルには一切書き込まれない。

彼女のスマホでも同じことをすれば、二人でアップロードできる。

## 6. 渡すもの

**しおりのURL（QRコード）** … `https://yuto123456gj.github.io/20261003trip/`

`upload.html` はQRに含めない。しおりからのリンクも張っていないので、
URLを直接知っている人しか開けない。

---

## 仕組みのメモ

- `photos/` に入れた画像が、そのままアルバムに並ぶ（一覧を書く必要はない）。
  ページを開いたときにGitHubのAPIでフォルダの中身を読んでいる。
- アルバムはDAY 2 の「16:00 サンセット＆解散」を解放すると表示される。
- 写真はアップロード時にブラウザ側で長辺1600pxへ縮小され、1枚200〜400KB程度になる。
- ファイル名は撮影日時（`20261003-154530-x9k2.jpg`）なので、自動的に時系列に並ぶ。

## 注意

- 公開リポジトリなので、URLを知っていれば誰でも見られる。
  `robots.txt` と `noindex` で検索避けはしてあるが、非公開ではない。
- トークンが漏れると、そのリポジトリに書き込まれる可能性がある。
  怪しいときは GitHub の設定画面からいつでも無効化できる。
