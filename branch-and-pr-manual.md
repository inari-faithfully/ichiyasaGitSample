# Git ブランチ作成〜プルリクエスト作成マニュアル

『いちばんやさしいGit&GitHubの教本』のサンプルリポジトリ（Fork済み）で、
ブランチを切って変更し、自分のリポジトリ内でプルリクエストを出すまでの手順。

---

## 0. 前提

- 自分のリポジトリ：`inari-faithfully/ichiyasaGitSample`
- これは `yasagit-3/ichiyasaGitSample`（教本の元リポジトリ）を **Fork したもの**
- 手元（ローカル）にクローン済み

---

## 1. ブランチを作って切り替える

```bash
git branch update-venue      # update-venue ブランチを作成
git branch                   # ブランチ一覧を確認（* が今いるブランチ）
git switch update-venue      # update-venue に切り替え
git status                   # 今の状態を確認
```

---

## 2. ファイルを変更してコミットする

`index.html` の会場名を変更した例。

```bash
git status                   # 変更ファイルを確認
git add index.html           # 変更をステージに上げる
git commit -m "変更"         # コミット
```

コミットメッセージは、後から見て分かる内容にするのがおすすめ
（例：`イベント会場名を修正`）。

---

## 3. 変更内容を確認する

```bash
git diff                     # まだコミットしていない差分（コミット後なら空）
git diff main                # main ブランチとの差分を比較
```

差分の例：

```diff
-                        <p>株式会社〇〇 イベントセミナー会場</p>
+                        <p>株式会社イン イベントセミナー会場</p>
```

---

## 4. GitHub に push する

```bash
git push origin update-venue
```

成功すると、こう表示される 👇

```
 * [new branch]      update-venue -> update-venue
```

`* [new branch]` ＝ GitHub 側に新しいブランチが作られた、という意味。

> 🔑 SSHキーのパスフレーズを聞かれたら入力する。

---

## ⚠️ よくあるつまずき：「ブランチが GitHub にない」

push は成功しているのに見当たらない場合、**見ているリポジトリが違う**ことが多い。

- 画面左上のリポジトリ名を必ず確認する
  - ❌ `yasagit-3 / ichiyasaGitSample` … 教本の元リポジトリ（他人のもの。Fork 1.4k・PR 253 が目印）
  - ✅ `inari-faithfully / ichiyasaGitSample` … 自分のリポジトリ
- 自分のリポジトリのブランチ一覧 URL：
  `https://github.com/inari-faithfully/ichiyasaGitSample/branches`
- ページを開いていた場合は **再読み込み** する

自分のリポジトリなら `2 Branches`（main と update-venue）が見えるはず。

---

## 5. プルリクエスト（PR）を作る

### ⚠️ 一番大事な注意点

Fork したリポジトリでは、PR の送り先（base）が **初期設定だと元リポジトリ（yasagit-3）**になっている。
そのまま作ると、教本の著者のリポジトリにPRを送ってしまう（PR 253 はこの間違いの山）。

**練習では「自分のリポジトリ内で update-venue → main」にPRを出すのが正解。**

### 手順

1. 自分のリポジトリで上部タブの **「Pull requests」** をクリック
2. 緑の **「New pull request」** をクリック
3. 上部の4つのドロップダウンを次のように設定する：

   | 項目 | 設定 |
   |------|------|
   | base repository | **`inari-faithfully/ichiyasaGitSample`**（元リポジトリから変更！） |
   | base | `main` |
   | head repository | `inari-faithfully/ichiyasaGitSample` |
   | compare | `update-venue` |

4. 差分（index.html の変更）が表示されることを確認
5. 緑の **「Create pull request」** をクリック
6. タイトル・説明を入力し、もう一度 **「Create pull request」**

---

## まとめ（コマンドだけ）

```bash
git branch update-venue
git switch update-venue
# ファイルを編集
git add index.html
git commit -m "イベント会場名を修正"
git diff main
git push origin update-venue
# → GitHub の自分のリポジトリで PR を作成（base を自分のリポジトリに変更）
```
