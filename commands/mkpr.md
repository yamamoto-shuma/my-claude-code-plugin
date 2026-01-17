---
name: mkpr
description: ブランチとPRを新規作成する
allowed-tools: Bash(git switch:*), Bash(git pull:*), Bash(git commit:*), Bash(git push:*), Bash(gh pr create:*)
model: claude-haiku-4-5-20251001
---

# 手順

1. ユーザにブランチ名を聞く
    ```
    ブランチ名を入力してください。
    ```

2. ユーザにPRのタイトルを聞く
    ```
    PRのタイトルを入力してください。
    ```

3. 以下の順番でコマンドを実行する
    ```bash
    git switch main
    git pull origin main
    git switch -c {ブランチ名}
    git commit --allow-empty -m "$(cat <<'EOF'
    開発開始
    Co-Authored-By: Claude <noreply@anthropic.com>
    EOF
    )"
    git push origin {ブランチ名}
    gh pr create --base main --head {ブランチ名} --title "{PRのタイトル}" --assignee @me --draft --fill
    ```

# 注意点

* main, masterブランチにはpushしないこと
* コマンドの実行中にエラーが発生した場合、エラーの内容と原因をユーザに説明した上で対処法を提示すること
