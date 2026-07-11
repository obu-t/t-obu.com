# t-obu.com

大府市スポーツ協会 硬式テニス部 公式サイト <https://obu-t.com> のソースコードです。
このリポジトリは GitHub Pages でそのまま配信されているので、**`main` ブランチに push した内容がそのまま `https://obu-t.com` に反映されます**。

- 公開 URL: <https://obu-t.com>
- リポジトリ: <https://github.com/obu-t/t-obu.com>
- 配信方法: GitHub Pages（カスタムドメイン `obu-t.com`）
- 反映されるブランチ: `main`

反映までのタイムラグは通常 1〜2 分。GitHub リポジトリ画面の **Actions** タブで `pages-build-deployment` が緑チェックになれば公開完了です。

---

## ディレクトリ構成

サイト全体が静的 HTML でできています。

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

## デプロイ手順

### 0. 最初の 1 回だけ準備するもの

1. **GitHub アカウント**（<https://github.com/signup>）を作り、部の管理者にユーザー名を伝えて `obu-t/t-obu.com` の Collaborator に追加してもらう。追加されないと push できません。
2. ローカルに Git がインストール済みか確認。

   ```sh
   git --version
   ```

3. 認証方法をどちらか用意する。
   - **HTTPS + Personal Access Token（推奨、簡単）**: <https://github.com/settings/tokens> で `repo` スコープの Fine-grained token を発行。push 時にユーザー名と token を聞かれるので、token をパスワード欄に貼る。macOS のキーチェーンや Git Credential Manager を使えば毎回入力せずに済みます。
   - **SSH 鍵**: `ssh-keygen -t ed25519 -C "your@email"` → `~/.ssh/id_ed25519.pub` の中身を <https://github.com/settings/keys> に登録。

### 1. clone（初回だけ）

```sh
# HTTPS の場合
git clone https://github.com/obu-t/t-obu.com.git

# SSH の場合
git clone git@github.com:obu-t/t-obu.com.git

cd t-obu.com
```

### 2. 更新の流れ（毎回）

```sh
git pull origin main            # 最新を取ってから始める（重要）
# ... ここでファイルを編集 ...
git status                      # 何が変わったか確認
git diff                        # 変更内容を確認
git add -A                      # 変更ファイルを全部ステージ
git commit -m "第45回選手権大会の申込書を追加"
git push origin main
```

push が通れば 1〜2 分で <https://obu-t.com> に反映されます。

### 3. よくある編集例

**A. 「what's new」（トップページのお知らせ）を追加する**

`index.html` の `what's new` セクション、`<div class="divTable">` の中の一番上の `<div class="divTableRow">` の上に同じ形式で 1 行足す。

```html
<div class="divTableRow">
    <a href="entry_sheet/2026/202601_Senshuken_singles.xlsx">2026.03.12　第45回大府市テニス選手権大会の申込書をアップしました</a><br />
</div>
```

**B. 要項・ドロー・結果の PDF を追加／差し替える**

1. 該当フォルダ（例: `d_youkou/2026/`）に PDF を置く。
2. A の要領で `index.html` の「what's new」にリンク行を追加。

### 4. 反映確認

ブラウザで <https://obu-t.com> を開いて Ctrl+F5（Mac は ⌘+Shift+R）で強制再読み込み。
数分待っても変わらないときは GitHub の **Actions** タブでビルドが失敗していないか確認してください。

---

## よくあるトラブル

- **`Permission denied` / `403` で push できない**
  Collaborator になっていないか、認証情報が古い可能性。ユーザー名を管理者に伝えて追加してもらうか、PAT を発行し直してください。
- **`! [rejected] main -> main (fetch first)`**
  誰かが先に push しています。`git pull --rebase origin main` して conflict があれば解決 → `git rebase --continue` → 再度 `git push`。
- **サイトに反映されない**
  多くはブラウザキャッシュ。強制再読み込み。それでもダメなら **Actions** タブでワークフロー失敗を確認。
- **間違えた commit を push してしまった**
  履歴を書き換えるより、次の commit で修正するのが安全です。どうしても取り消したいときは `git revert <SHA>` で打ち消し commit を作って push。
- **CNAME が消えて obu-t.com が外れた**
  Settings → Pages のカスタムドメイン欄に `obu-t.com` を入れ直す。DNS 側は基本触らなくて大丈夫です。

---

## 部内向けメモ

- `main` ブランチが本番なので、実験的な変更を試したいときはブランチを切って PR を出してください。
- ドメイン (`obu-t.com`) は GitHub Pages のカスタムドメインとして Settings → Pages で紐付け済み。DNS はドメイン管理者が別途設定済み。ドメイン切替や DNS 変更の予定があるときは管理者に一声。
