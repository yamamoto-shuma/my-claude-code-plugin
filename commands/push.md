---
name: push
description: 変更をリモートにgit pushする
argument-hint: all
allowed-tools: Bash(git branch:*), Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*)
model: claude-haiku-4-5-20251001
---

# 手順

0. ユーザから引数(all)が渡されていない場合、変更されたファイルを`git status`で確認した上で以下を聞く
    ```
    現在以下のファイルが変更されています。どのファイルをpushしますか？(複数指定可)
    
    {git statusで確認した変更ファイル一覧}

    ※ 全ての変更をpushする場合は**all**と入力してください
    ```

1. push対象のファイルを`git diff`で確認する(後でコミットメッセージを生成するのに使います)

2. push対象のファイルを`git add`する

3. `git commit`する
    * このときコミットメッセージは`git diff`で確認した変更差分を踏まえて生成すること
    * コミットメッセージの最後に以下を追加すること
        ```
        Co-Authored-By: Claude <noreply@anthropic.com>
        ```

4. `git push origin {ブランチ名}`する

# 注意点

* main, masterブランチにはpushしないこと
* コミットメッセージは日本語で生成すること
* コミットメッセージにはprefixを付けること。使用可能なprefixと説明は以下の通り
    * add      : ちょっとしたファイル・コードの追加
    * change   : ちょっとしたファイル・コードの変更
    * feat     : 新機能の追加
    * fix       : バグ修正
    * remove   : ファイル・コードの削除
    * rename   : ファイル名・変数名の変更
    * refactor : リファクタリング
    * docs     : ドキュメント関連の変更
    * style    : フォーマット関連の変更
    * test     : テスト関連の変更
