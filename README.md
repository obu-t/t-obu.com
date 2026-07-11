# t-obu.com

大府市スポーツ協会 硬式テニス部 公式サイト <https://obu-t.com> のソースコードです。
このリポジトリは GitHub Pages でそのまま配信されているので、**`main` ブランチに push した内容がそのまま `https://obu-t.com` に反映されます**。

- 公開 URL: <https://obu-t.com>
- リポジトリ: <https://github.com/obu-t/t-obu.com>
- 配信方法: GitHub Pages（カスタムドメイン `obu-t.com`）
- 反映されるブランチ: `main`

---

## ディレクトリ構成

サイト全体が静的 HTML でできています。トップのフォルダを大まかに書くとこんな感じです。

| 場所 | 中身 |
| --- | --- |
| `index.html` ほか各 `*.html` | 各ページ本体 |
| `css/` | スタイルシート |
| `image/` `back_pic/` | ロゴ・背景・写真 |
| `d_youkou/<年>/` | 大会要項の PDF |
| `draw/<年>/` | ドロー表・参加選手一覧の PDF |
| `entry_sheet/<年>/` | 大会申込書 (xlsx) |
| `result/<年>/` | 試合結果の PDF |
| `ranking/` | ランキング表 |
| `members/` | 部員便り |
| `school/` | テニス教室 |
| `rule/` | ルール関連 |

新しい資料を追加するときは、**種類ごとのフォルダの中の年フォルダ**（例: `entry_sheet/2026/`）に置いてください。

---

## デプロイ手順（Git を触るのが初めての方向け）

Git のコマンドはコワいので、**GitHub Desktop**（無料のクリックだけで使える公式アプリ）を使う手順を先に書きます。コマンド派の方はさらに下の「コマンドラインで操作したい方」を見てください。

### 0. 最初の 1 回だけ準備するもの

1. **GitHub アカウント**を作る（<https://github.com/signup>）。
2. アカウントができたら、部の管理者（＝いま README を書いた人）に GitHub のユーザー名を伝えて、`obu-t/t-obu.com` の Collaborator に追加してもらってください。追加されないと push（アップロード）ができません。
3. **GitHub Desktop** をインストール（<https://desktop.github.com/>）。起動して GitHub アカウントでサインインします。

### 1. リポジトリを自分の PC に持ってくる（clone）

初回だけの作業です。

1. GitHub Desktop を開き、上メニューの **File → Clone repository...** を選ぶ。
2. `obu-t/t-obu.com` を選んで、保存先（例: `ドキュメント/GitHub/t-obu.com`）を決めて **Clone** を押す。
3. 完了するとその保存先フォルダに、このリポジトリと同じファイル一式ができます。

以降は、そのフォルダの中身を **普通のファイル操作（コピペ・上書き・削除）** で編集すれば OK です。

### 2. ファイルを更新する

よくある作業は次の 2 種類です。

**A. 「what's new」（トップページのお知らせ）を追加する場合**

1. clone したフォルダの `index.html` をテキストエディタ（メモ帳・秀丸・VS Code など）で開く。
2. `what's new` 直下にある `<div class="divTable">` ブロックの中の、**一番上の `<div class="divTableRow">` の上**に、同じ形式で 1 行足す。

   例:
   ```html
   <div class="divTableRow">
       <a href="entry_sheet/2026/202601_Senshuken_singles.xlsx">2026.03.12　第45回大府市テニス選手権大会の申込書をアップしました</a><br />
   </div>
   ```

3. 保存する。

**B. 大会要項・ドロー・結果の PDF を差し替える／追加する場合**

1. 該当のフォルダ（`d_youkou/2026/` など）に PDF や xlsx を置く。
2. 上の A のやり方で `index.html` の「what's new」に告知の行を追加する。

### 3. GitHub Desktop で公開する

1. GitHub Desktop に戻ると、変更したファイルが左に一覧で出ています。中身のプレビューで意図した変更になっているか確認。
2. 左下の **Summary** 欄に、後から見てわかる短いメッセージを書きます（例: `第45回選手権大会の申込書を追加`）。
3. **Commit to main** ボタンを押す。
4. 上部の **Push origin** ボタンを押す。（これで GitHub にアップロードされます）

**Push が完了して 1〜2 分すると <https://obu-t.com> に反映されます。**

### 4. 反映されたか確認する

ブラウザで <https://obu-t.com> を開き、Ctrl+F5（Mac は ⌘+Shift+R）で再読み込みして、変更した箇所が見えれば OK。

数分待っても変わらないときは、GitHub のリポジトリ画面上部の **Actions** タブで、`pages-build-deployment` が緑チェックになっているか確認してください。赤 × のときは下の「よくあるトラブル」へ。

---

## コマンドラインで操作したい方

Git がインストール済み・SSH または PAT の認証が通っている前提です。

```sh
# 初回だけ
git clone https://github.com/obu-t/t-obu.com.git
cd t-obu.com

# 毎回の作業
git pull origin main            # 最新を取ってから編集を始める
# ... ファイルを編集 ...
git add -A
git commit -m "第45回選手権大会の申込書を追加"
git push origin main
```

push が通れば `https://obu-t.com` に自動反映されます（通常 1〜2 分）。

---

## よくあるトラブル

- **Push できない / 権限エラーが出る**
  Collaborator に追加されていない可能性があります。管理者に GitHub ユーザー名を伝えて追加してもらってください。
- **反映されない**
  ブラウザキャッシュで古い画面が表示されているだけのことが多いです。Ctrl+F5（Mac は ⌘+Shift+R）で強制再読み込み。
  それでもダメなら GitHub 上で **Actions** タブを見て、失敗しているワークフローがないか確認してください。
- **編集中に別の人が更新してしまい、push が拒否された**
  GitHub Desktop なら上部の **Pull origin** を押すと最新を取り込めます。コマンドの場合は `git pull --rebase origin main` してから再度 `git push`。
- **間違えて commit してしまった**
  push 前なら GitHub Desktop の **History** タブから該当コミットを右クリック → **Revert** で戻せます。push した後で消したい場合は管理者に相談してください（履歴に残るので、次の commit で修正する方が安全なことも多いです）。

---

## 部内向けメモ

- `main` ブランチが本番なので、実験的な変更を試したいときは新しいブランチを切って作業してください。誰かのレビューが欲しい場合は Pull Request を出せます。
- ドメイン (`obu-t.com`) は GitHub Pages のカスタムドメインとして GitHub のリポジトリ設定 (Settings → Pages) で紐付けています。DNS は別途、ドメイン管理者が設定済み。ドメイン切替の予定があるときは管理者に一声かけてください。
