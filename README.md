# t-obu.com

大府市スポーツ協会 硬式テニス部 公式サイト <https://obu-t.com> のミラーリポジトリで、`https://t-obu.com` として GitHub Pages から配信予定です。
リポジトリは GitHub Pages でそのまま配信されるため、**`main` ブランチに push した内容がそのまま `https://t-obu.com` に反映されます**。

- 公開 URL: <https://t-obu.com>（配信予定）
- ミラー元: <https://obu-t.com>
- リポジトリ: <https://github.com/obu-t/t-obu.com>
- 配信方法: GitHub Pages（カスタムドメイン `t-obu.com`）
- 反映されるブランチ: `main`

反映までのタイムラグは通常 1〜2 分。GitHub リポジトリ画面の **Actions** タブで `pages-build-deployment` が緑チェックになれば公開完了です。

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

push が通れば 1〜2 分で <https://t-obu.com> に反映されます。
